# Transformer

• 下面按这节 notebook 的 seq2seq Transformer 来走一遍，假设：

  - B = batch_size
  - S = source 长度
  - T = target 长度
  - H = num_hiddens
  - Vsrc = source vocab size
  - Vtgt = target vocab size
  - h = num_heads

  在这节代码里典型参数是：

  - H = 256
  - h = 4

  所以每个 head 的隐藏维一般是：

  - d = H / h = 64

---------

  1. 原始输入数据

  先有两类序列：

  - source: (B, S)
  - target: (B, T)

  它们里面存的是 token id，不是向量。

  例如：

  - source[b] 是一条输入句子的词编号序列
  - target[b] 是对应输出句子的词编号序列

  还会有：

  - source valid_lens: (B,)
  - target valid_lens: (B,) 或训练时内部构造 mask 用

---------

  2. 训练时 target 会拆成两份

  训练 decoder 时不是直接拿完整 target 做输入，而是错开一位：

  - decoder input: (B, T)
  - y: (B, T)

  概念上：

  decoder input: <bos> x1 x2 x3
  y:             x1   x2 x3 <eos>

  所以：

  - decoder input 是喂给 decoder 的
  - y 是拿来算 loss 的真实标签

---------

## Encoder 部分

  3. Encoder embedding

  self.embedding(X)

  输入：

  - X: (B, S)

  输出：

  - (B, S, H)

  含义是：每个 token id 变成一个 H 维向量。

---------

  4. 乘以 sqrt(H) 再加位置编码

  X = self.pos_encoding(self.embedding(X) * math.sqrt(self.num_hiddens))

  输入输出形状都不变：

  - (B, S, H) -> (B, S, H)

  这里位置编码只是“加上去”，不会改 shape。

---------

  5. 进入一个 Encoder Block

  一个 TransformerEncoderBlock 输入：

  - X: (B, S, H)
  - valid_lens: (B,)

  输出：

  - (B, S, H)

  因为这一层不会改序列长度，也不会改隐藏维度。

---------

  6. Encoder Block 里的 Multi-Head Self-Attention

  调用：

  self.attention(X, X, X, valid_lens)

  所以：

  - queries: (B, S, H)
  - keys: (B, S, H)
  - values: (B, S, H)

  这是 self-attention，因为三者都来自同一个 X。

  多头内部可以这样理解：

  1. 线性投影后，仍可看作总 shape (B, S, H)
  2. 拆成多头后，相当于：
      - (B, h, S, d)，其中 d = H/h
  3. 每个 head 做注意力分数：
      - QK^T 得到 (B, h, S, S)
  4. 对 value 加权求和：
      - 输出 (B, h, S, d)
  5. 拼回去：
      - (B, S, H)

  所以多头注意力模块整体输入输出仍是：

  - (B, S, H) -> (B, S, H)

  注意力权重 shape 通常是：

  - (B*h, S, S) 或重排后 (B, h, S, S)

  这节可视化时最终整理成：

  - (num_layers, num_heads, S, S)

---------

  7. AddNorm 1

  Y = self.addnorm1(X, attention_out)

  其中：

  - X: (B, S, H)
  - attention_out: (B, S, H)

  输出：

  - Y: (B, S, H)

  因为是残差相加再 LayerNorm，不改 shape。

---------

  8. PositionWiseFFN

  self.ffn(Y)

  输入：

  - (B, S, H)

  中间过程：

  - 第一层线性：(B, S, H) -> (B, S, ffn_num_hiddens)
  - ReLU：形状不变
  - 第二层线性：(B, S, ffn_num_hiddens) -> (B, S, H)

  所以最终输出：

  - (B, S, H)

  注意：FFN 只改“每个位置自己的特征”，不混位置。

---------

  9. AddNorm 2

  输出仍然是：

  - (B, S, H)

---------

  10. 多层 Encoder 堆叠后

  如果有 L 个 encoder block，shape 一直不变：

  - (B, S, H)

  最终 encoder 输出：

  - enc_outputs: (B, S, H)

  这就是给 decoder 用的“源序列上下文化表示”。

---------

  ## Decoder 部分

  11. Decoder 输入 embedding

  decoder 输入的是右移后的目标序列：

  - X: (B, T)

  经过 embedding：

  - (B, T, H)

  加位置编码后仍是：

  - (B, T, H)

---------

  12. Decoder Block 输入

  一个 TransformerDecoderBlock 接收：

  - X: (B, T, H)
  - state[0] = enc_outputs: (B, S, H)
  - state[1] = enc_valid_lens: (B,)

  输出：

  - (B, T, H)

---------

  13. Decoder 第一层：masked self-attention

  这一步是：

  self.attention1(X, key_values, key_values, dec_valid_lens)

  训练时：

  - key_values = X
  - queries: (B, T, H)
  - keys: (B, T, H)
  - values: (B, T, H)

  mask 之后，每个位置只能看自己和前面。

  多头内部的权重 shape 可理解为：

  - (B, h, T, T)

  输出仍然：

  - (B, T, H)

---------

  14. AddNorm 1

  输出：

  - (B, T, H)

  记作 Y。

---------

  15. Decoder 第二层：encoder-decoder attention

  这一步很关键：

  self.attention2(Y, enc_outputs, enc_outputs, enc_valid_lens)

  所以：

  - queries: (B, T, H) 来自 decoder
  - keys: (B, S, H) 来自 encoder
  - values: (B, S, H) 来自 encoder

  注意力分数 shape 是：

  - (B, h, T, S)

  意思是：

  - 每个目标位置
  - 去看所有源位置

  输出 shape：

  - (B, T, H)

---------

  16. AddNorm 2

  输出：

  - (B, T, H)

  记作 Z。

---------

  17. FFN

  输入输出：

  - (B, T, H) -> (B, T, H)

---------

  18. AddNorm 3

  输出：

  - (B, T, H)

  所以一个 decoder block 结束后 shape 不变。

---------

  19. 多层 Decoder 堆叠后

  如果堆 L 层，shape 一直保持：

  - (B, T, H)

---------

  20. 最后一层线性映射到词表

  self.dense(X)

  输入：

  - (B, T, H)

  输出：

  - y_hat: (B, T, Vtgt)

  这是每个位置对目标词表的预测分布 logits。

---------

  ## Loss 部分

  21. 标签 y 的形状

  真实标签：

  - y: (B, T)

  里面每个元素是一个目标词 id。

---------

  22. 预测 y_hat 的形状

  模型输出：

  - y_hat: (B, T, Vtgt)

  对第 b 条样本、第 t 个位置：

  - y_hat[b, t] 是长度为 Vtgt 的向量
  - 表示该位置对整个词表的打分/概率

---------

  23. 计算交叉熵时的对应关系

  逐位置比较：

  - y_hat[b, t, :]
  - y[b, t]

  padding 位置通常会被 mask 掉，不参与损失。

---------

  ## 推理时的形状区别

  24. 训练 vs 推理

  训练时：

  - 一次把整个 decoder input 喂进去
  - shape 是 (B, T, H)

  推理时：

  - 每次只新生成一个 token
  - 当前步输入长度会逐步增长

  第 t 步时，decoder 当前可见部分大致是：

  - (B, t, H)

  不过代码里会通过 state[2][i] 缓存前面步的表示，避免每次完全重算。

---------

  ## 一条完整数据流总结

  如果从头到尾串起来：

  1. source: (B, S)
  2. encoder embedding: (B, S, H)
      - positional encoding: (B, S, H)
  4. encoder blocks 后：enc_outputs = (B, S, H)
  5. decoder input: (B, T)
  6. decoder embedding: (B, T, H)
      - positional encoding: (B, T, H)
  8. masked self-attention 后：(B, T, H)
  9. encoder-decoder attention 后：(B, T, H)
  10. FFN 后：(B, T, H)
  11. 多层 decoder 后：(B, T, H)
  12. final linear: y_hat = (B, T, Vtgt)
  13. 标签：

  - y = (B, T)

  14. loss：

  - 比较 y_hat 和 y

---------

  ## 你最该记住的 shape 规律

  Transformer 里最核心的规律其实就三条：

  - hidden 表示序列：(B, seq_len, H)
  - 输出到词表：(B, seq_len, vocab_size)

  attention 权重则常见为：

  - self-attention: (B, h, seq_len, seq_len)
  - cross-attention: (B, h, target_len, source_len)

  如果你愿意，我下一条可以直接按这节代码里的具体超参数，给你画一个 带真实数字的 shape 表，比如：

  - source: (128, 9)
  - encoder hidden: (128, 9, 256)
  - decoder output: (128, 9, |V|)

  这样会更直观。

## 结构

这节 Transformer 里主要有这几种层。可以把它们理解成：有的层负责“表示词”，有的层负责“看上下文”，有的层负责“加工特
  征”，有的层负责“稳定训练”，最后一层负责“出预测”。

  1. Embedding 层

  作用：把离散的 token id 变成稠密向量。

  比如：

  - 输入：[12, 45, 9]
  - 输出：3 个 H 维向量

  为什么需要它：

  - 神经网络不能直接处理“词编号”这种离散符号
  - embedding 把每个词映射成可学习的语义表示

---------

  2. Positional Encoding 层

  作用：给每个位置加入“顺序信息”。

  因为 Transformer 本身没有 RNN，也没有卷积，它只看一堆 token 向量，默认并不知道：

  - 谁在前
  - 谁在后
  - 第几个词

  所以要把位置编码加到 embedding 上，让模型知道顺序。

---------

  3. Multi-Head Self-Attention 层

  作用：让序列中每个位置都能根据需要去关注其他位置。

  比如一句话里某个词可能要重点看：

  - 前面的主语
  - 后面的宾语
  - 很远处的修饰词

  self-attention 做的就是这种“按相关性聚合信息”。

  为什么是 multi-head：

  - 不同 head 可以学不同关系
  - 一个 head 可能关注语法
  - 一个 head 可能关注位置对应
  - 一个 head 可能关注长距离依赖

  所以它本质上是在做：
  让每个 token 融合全局上下文。

---------

  4. Masked Self-Attention 层

  这是 decoder 里的第一层注意力。

  作用：让当前位置只能看见自己和前面的 token，不能偷看后面的 token。

  为什么要这样：

  - 生成第 t 个词时，理论上只能依赖前 t-1 个词
  - 如果看到未来词，就等于作弊

  所以它的作用是：
  保证自回归生成成立。

---------

  5. Encoder-Decoder Attention 层

  这是 decoder 里的第二层注意力，也叫 cross-attention。

  作用：让 decoder 在生成目标词时，去查看 encoder 输出的源序列信息。

  直观理解：

  - decoder 正在生成第 t 个目标词
  - 它会去 source 里找当前最相关的部分

  所以这层的作用是：
  把输入序列的信息对接到输出序列生成上。

  如果没有这层，decoder 就更像一个只会“自己续写”的语言模型，而不是条件生成模型。

---------

  6. PositionWise FFN 层

  作用：对每个位置的表示单独做一次非线性变换。

  形式通常是：

  Linear -> ReLU -> Linear

  它和 attention 的区别是：

  - attention 负责“不同位置之间的信息交互”
  - FFN 负责“每个位置自己的特征加工”

  可以理解成：

  - attention 先把别人的信息拿过来
  - FFN 再把当前这个位置的表示重新整理一遍

---------

  7. Residual Connection 层

  作用：把输入直接加回输出。

  形式是：

  X + sublayer(X)

  为什么要这样：

  - 深层网络更容易训练
  - 防止信息在层数变深时丢失
  - 让每一层更像是在原表示上做“修正”

  所以残差连接的核心作用是：
  保留原信息，稳定深层训练。

---------

  8. LayerNorm 层

  作用：对每个位置的特征做归一化，让数值更稳定。

  它通常接在残差后面，也就是 AddNorm。

  为什么重要：

  - 缓解训练不稳定
  - 让不同层之间的数值尺度更平衡
  - NLP 里通常比 BatchNorm 更合适

  它的核心作用是：
  稳定训练过程，加快收敛。

---------

  9. Dropout 层

  作用：训练时随机丢掉一部分激活，防止过拟合。

  在这节里它通常出现在：

  - attention 之后
  - AddNorm 里面
  - positional encoding 后

  它的作用比较直接：
  正则化。

---------

  10. 最后一层 Linear / Dense 输出层

  作用：把 decoder 的隐藏状态映射到词表大小。

  输入：

  - (B, T, H)

  输出：

  - (B, T, vocab_size)

  含义是：

  - 每个位置对整个词表都给一个分数
  - 后面用 softmax / cross entropy 去算预测和损失

  所以它的作用是：
  把“隐藏表示”变成“具体预测哪个词”。

---------

  按模块总结

  Encoder 里每层主要是：

  1. self-attention：融合整句上下文
  2. FFN：加工每个位置特征
  3. residual + layernorm：稳定训练

  Decoder 里每层主要是：

  1. masked self-attention：只看已生成部分
  2. encoder-decoder attention：看输入序列
  3. FFN：加工当前位置特征
  4. residual + layernorm：稳定训练

---------

  一句话记忆版

  - Embedding：把词编号变成向量
  - Positional Encoding：告诉模型顺序
  - Self-Attention：看整句上下文
  - Masked Self-Attention：只能看前文
  - Cross-Attention：生成时看输入
  - FFN：逐位置做非线性加工
  - Residual：保留原信息
  - LayerNorm：稳定训练
  - Dense：输出词表预测

  如果你愿意，我下一条可以继续讲：为什么一个 block 里是 attention 在前、FFN 在后，而不是反过来。



























line NO. | repeat times | v | w | N^+(v) | visited | stacked | alpha(v)

6 | 1 | a | / | {b, s} | {0, …, 0} | {0, 0, …, 0} | /

9 | 1 | a | / | {b, s} | {0, …, 0} | {1, 0, …, 0} | /