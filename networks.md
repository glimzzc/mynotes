# Networks





## Layered Model

### 上节课回顾
第一讲导论课我们介绍了：
- 课程基本安排
- 网络简史、网络之网络（互联网）、万维网 WWW
- 现代网络基本概念
  - 通信两端的**端系统/主机**（包括服务器）
  - 路由器与接入网/边缘路由器

---

### 本节课内容
本节课我们学习如何用**分层模型**理解网络：
- 早期通用的 **7层 OSI 模型**
- 它的优缺点
- 本课程重点：**5层 TCP/IP 模型**（最适合互联网）
  - 参考 Kurose & Ross 教材
  - 有时也被称为 TCP/IP 模型
  - 有时被简化为4层模型

---

### 网络分层模型
网络通信通过**协议栈**实现。
每层之间定义好协议来传递消息，因此也叫**协议栈**。

**模块化设计优点：**
- 内部组件可轻松替换
- 每层功能明确，更容易理解
- 缺点：可能存在**冗余**，多层做重复工作

---

### 设计原则
理想的网络分层模型应：
- 在需要独立抽象时创建层
- 每层有**明确定义**的功能
- 层边界尽量减少跨层数据流动
但层数与功能仍有设计选择空间

---

### 类比：航空出行
- 购票 / 退票
- 行李托运 / 领取
- 登机 / 下机
- 跑道起飞 / 降落
- 航线规划

**每层提供服务，并依赖下层提供的功能。**

---

### 面向对象设计思想
分层与面向对象编程完全一致：
- 每层内部实现**封装隐藏**
- 层间通信是**公共接口**
- 模块化便于维护与更新
- 某一层实现修改对其他层**透明**
  例如：登机流程改变不影响飞行与航线

---

### OSI 参考模型
OSI = 开放系统互联（Open Systems Interconnection）
- 1970年代由 ISO 国际标准化组织制定
- 当时网络协议尚未定型
- 并非专为互联网设计
- 通用网络模型
- **7层结构**
- 常用于教材与培训

---

### OSI 7层结构
1. 应用层
2. 表示层
3. 会话层
4. 传输层
5. 网络层
6. 数据链路层
7. 物理层

---

### 应用层、表示层、会话层
- **应用层**：面向用户的协议（ftp、http、smtp…）
- **表示层**：数据格式解释、压缩、加密
- **会话层**：管理应用之间的对话、分隔与同步

---

### 传输层
- 向下：接收会话层数据，拆分为**段**，交给网络层
- 向上：接收网络层数据，重组为会话层数据
- 负责**主机到主机**通信
- 头部携带目标地址
- 不关心底层网络设备

---

### 网络层
- 控制主机间子网的运行
- 决定数据包（数据报）如何**动态路由**
- 可提供拥塞控制与服务质量
- 是简单路由器能理解的**最高层**
  路由器不需要传输层与应用层

---

### 链路层 & 物理层
- **数据链路层**：负责数据包在节点间逐跳传递
  如以太网、Wi‑Fi；使用 **MAC 地址**
- **物理层**：负责**比特级**传输
  铜线、光纤、无线电；纯硬件层

---

### OSI 模型优缺点
**优点：**
- 层与协议定义清晰
- 通用性强，可用于各类网络

**缺点：**
- 过于复杂
- 表示层、会话层功能弱，可并入应用层

---

### TCP/IP 5层模型（互联网标准）
1. **应用层**
2. **传输层**
3. 网络层
4. 链路层
5. 物理层

表示层、会话层**合并到应用层**。
网络层有时叫**互联网层**。
也常合并为**4层模型**。

---

### 物理层 & 链路层
- **物理层**：数据 ↔ 电信号/光信号/无线电信号
- **链路层**：控制数据包在节点间传输
  错误检查、设备发现（如Wi‑Fi）

---

### 网络层
最主要协议：**IP 协议**
- 定义数据如何打包为**数据报/包**
- 网络寻址方案
- ICMP：路由器之间的控制消息
Java 只识别 IP 协议。

---

### 传输层
解决数据包丢失、乱序、损坏问题。
两大协议：
- **TCP**：可靠传输、重传、有序
  开销高
- **UDP**：检测损坏，不保证有序与可达
  开销低

---

### 应用层
- 用户代码与界面所在层
- 向传输层收发数据
- 不同协议处理不同数据：
  http、ftp、smtp 等
- 可自定义协议

---

### TCP/IP 模型优缺点
**优点：**
- 非常适合网络编程（尤其 Java 网络编程）
- 比 OSI 简单
- 完全适配互联网

**缺点：**
- 层与协议边界不够清晰
- 通用性不如 OSI

---

### 课程结构
1：课程介绍
2–4：网络分层与互联网架构
5–15：应用层
16：传输层
17–18：网络层
19：链路层与物理层
20：复习

---

### 总结 & 下节课
今天我们学习了：
- **7层 OSI 通用模型**
- **5层 TCP/IP 模型**（互联网与本课程重点）

接下来几讲：
- 端口与 IP 地址
- TCP 与 UDP 详解
这些是第5讲开始**Java 网络编程**的基础。



## Ports & TCP & UDP

### 上节课回顾
上节课我们学习了网络分层模型，特别是互联网最常用的 **TCP/IP 5层模型**：
- 应用层（最上层）
- 传输层
- 网络层
- 数据链路层
- 物理层（最底层）

数据从应用层向下经过协议栈传输，到达目标主机后再从下往上传递。

---

### 本节课内容
今天我们学习：
- **端口**（包括常用端口）
- 应用层以下各层如何完成网络通信
  - 传输层
  - 网络层
  - 数据链路层
  - 物理层

端口是开始编程前必须掌握的概念之一；另一个是 **IP 寻址**，我们将在下一讲学习。

---

### 端口
应用程序通过**网络端口**与传输层连接。
不同的端口号可以对应不同的**应用层进程**。
这使得**同一台主机、同一个IP地址**可以同时运行多个应用。

端口**纯由软件实现**，由操作系统提供。
可以分配给特定服务，如邮件、HTTP 等。

---

### 发送与接收
将**主机到主机**的传输转为**进程到进程**的传输，是**传输层**的工作。
这个过程称为：
- **多路复用**（发送端）
- **多路分用**（接收端）

应用程序通常会公布自己监听的端口。
发送方使用这个公布的端口号建立连接。
通信会持续使用同一端口，该端口也可用于发起新连接。

---

### 可用端口
一台主机上可用端口范围：**1~65535**
是16位无符号整数，0 不合法。
**TCP 端口和 UDP 端口相互独立**。

端口分类：
- **1~1023**：保留端口，由 IANA 分配
- **1024~65535**：常用自定义端口，可自由使用

在 UNIX 系统可查看 `/etc/services` 获取端口列表。

---

### 远程登录与文件传输
- **telnet**：端口 23，电传网络协议，早期客户端/服务器协议，**不安全，现已很少使用**
- **ssh**：端口 22，安全外壳协议，安全远程登录
- **ftp**：文件传输协议
  - 21端口：命令传输（dir、put、get等）
  - 20端口：数据传输（传统方式，速度慢）

---

### 电子邮件
- **smtp**：端口25，简单邮件传输协议，**用于发送邮件**
- **imap**：端口143，互联网消息访问协议，**用于接收/访问邮件**
- **pop3**：端口110，邮局协议版本3，**用于接收邮件**

---

### 网页服务
- **http**：端口80，超文本传输协议，**不安全**
- **https**：端口443，安全版HTTP，需要身份验证
（安全与认证将在第13讲讲解）

---

### 网络通信
在应用层，要发送的数据、目标主机与端口号会被打包准备传输。
传输层**不关心**底层通信的子网结构，只添加头部（端口、校验和等）。
网络层及以下会直接使用子网设备：
例如网络层决定数据包经过哪些节点。

---

### 传输层两大核心协议
1. **UDP**：用户数据报协议
2. **TCP**：传输控制协议

区别：
- 头部信息不同
- 服务可靠性不同
- 性能不同

两者都包含**校验和**以保证数据完整性。

---

### UDP
UDP 是**无连接**协议。
每个消息相互独立。
在数据前添加 **8字节头部**，包含：
- 源端口
- 目的端口
- 数据长度
- 校验和

端口用于标识源主机与目标主机上的进程。
UDP 只校验数据完整性，**损坏的数据会直接丢弃**。

---

### UDP 头部结构
源端口（2字节）| 目的端口（2字节）
数据长度（2字节）| 校验和（2字节）
数据内容...

注意：
UDP 头部**不包含IP地址**，TCP 也一样。
IP地址是**网络层**的职责。

---

### UDP 的用途
- **DNS 查询**：将域名转为IP（下一讲详细介绍）
- **实时多媒体**：通常封装在 RTP（实时传输协议）中
- 数据包有序号，接收方可判断是否丢包
- **不重传、不纠错**，接收方可自行插值补偿

---

### TCP
TCP 是**面向连接**的协议，在两台主机间维持**持久连接**。
保证**可靠传输**，丢失/损坏的数据会**重传**。
同时提供**拥塞控制**。

TCP 头部 **20字节**，包含：
- 序号
- 确认号
- 连接维护标志位
- 其他专用字段
其余字段与 UDP 相同。

序号与确认号用于**保证顺序**、检测丢包。

---

### TCP 头部结构
源端口（2字节）| 目的端口（2字节）
序号（4字节）
确认号（4字节）
标志位（2字节）| 接收窗口（2字节）
校验和（2字节）| 紧急指针（2字节）
选项（可选）
数据内容...

---

### 网络层 — IP
网络层对传输层数据添加头部并转发：
- IPv4 头部：20字节
- IPv6 头部：40字节

包含：
- 源/目标IP地址
- 协议类型（TCP / UDP）
- 头部校验和（IPv4）
- **TTL（生存时间）**

每经过一个网络节点，TTL 减1；减到0则丢弃，**防止数据包无限循环**。

---

### 数据链路层与物理层
数据以帧的形式传到物理层。
例如以太网帧有 **22字节头部**，包含：
- 前导码（同步用）
- 源与目的 **MAC 地址**
- 类型字段
- 校验和（通常在尾部）

MAC 地址用于帧在设备间**逐跳转发**。
校验和保证帧的完整性。

---

### 整体封装结构
链路层头部（如以太网22字节）
→ 网络层头部（20/40字节）
→ 传输层头部（8/20字节）
→ 数据

每一层都有源与目的“地址”：
- 传输层 ↔ 应用层：**端口**
- 网络层：**IP地址**
- 链路层：**MAC地址**

---

### 网络传输
源到目标通常会经过**多个设备**。
- 网络层路由器：决定主机之间的路径
- 链路层交换机/网桥：在网络组件间转发帧
- 物理层中继器/集线器：再生信号，延长传输距离

---

### 总结
- 数据发送时，每一层都会**添加头部**；接收时对应层**去掉头部**。
- 寻址体系至关重要：
  - 链路层：**MAC地址**（编程不关心）
  - 网络层：**IP地址**（标识源与目标主机）
  - 传输层：**端口号**（标识具体应用程序）

下节课我们学习：**DNS 域名系统**。





## DNS

### 本节课内容
本节课我们将学习：
- 如何把人类可读的网址（如 www.leeds.ac.uk）转换成 IP 地址
- **DNS（域名系统）** 的作用
- DNS 服务器的**层级结构**
- DNS 的查询方式
- DNS 提供的其他服务

下节课我们会详细讲解 IP 地址，以及如何在 Java 中使用 IP 地址。

---

### 核心概念
1. **间接寻址**
   用域名代替 IP 地址，人们几乎不直接使用 IP 地址。
2. **层级结构**
   体现在 IP 地址、域名和 DNS 服务器本身的结构中。
3. **分布式**
   没有任何一台 DNS 服务器包含所有域名与 IP，可扩展性强。
4. **缓存**
   本地缓存 DNS 查询结果，方便重复使用。

---

### 域名 vs IP 地址
- 人类更擅长记忆**名字**，而不是数字。
- 但名字几乎不提供主机位置信息。
- 顶级域如 .uk、.fr 仅能体现国家，无法定位更细粒度。
- .org、.net 等则完全不体现位置。
- **IP 地址是网络通信的原始数据**，属于网络层。
- IP 地址是**层级结构**，能更直接反映主机位置。

---

### 唯一性（1个域名 → 多个IP）
- 一个主机名可以对应**多个 IP 地址**。
- 热门服务器通常在全球部署多个 IP。
- DNS 会尝试选择**离用户最近**的 IP。
- 也可以轮流分配 IP，降低拥塞。
- 适用于大型网站、CDN（内容分发网络）。

### 唯一性（多个域名 → 1个IP）
- 多个域名可以映射到**同一个 IP**，称为**别名（aliasing）**。
- 对邮件地址特别有用。
- 发送邮件时，邮件客户端会查询 DNS，找到该域名对应的**正式服务器地址**。

---

### DNS 服务器层级
1. **根服务器（Root）**
   最顶层，指向各个顶级域服务器。
2. **顶级域服务器（TLD）**
   负责 .com、.org、.net、.uk、.fr 等。
   每个顶级域由一个机构维护（如 .com 由 Verisign 管理）。
3. **权威服务器（Authoritative DNS）**
   保存具体域名与 IP 的对应关系。

---

### DNS 协议
- 主要使用 **UDP** 协议。
- 数据量大时也可使用 TCP。
- 使用 **53 号端口**。
- 查询超时会自动重试。
- 消息分为**查询（query）**和**回复（reply）**，格式相同。

---

### DNS 查询过程
1. 本地主机向**本地DNS服务器**发起请求。
2. 本地DNS向**根DNS服务器**查询。
3. 根服务器返回对应**顶级域服务器（TLD）**地址。
4. 本地DNS向TLD服务器查询。
5. TLD返回对应**权威DNS服务器**地址。
6. 本地DNS向权威DNS查询，获得最终IP。
7. 将IP返回给主机。

---

### 递归查询与迭代查询
- **递归查询**：主机 → 本地DNS
  主机要求本地DNS“直接给我结果”。
- **迭代查询**：本地DNS → 根 → TLD → 权威
  本地DNS自己一步步问下去。
- 一次完整解析总共需要 **8 条消息**。

---

### DNS 缓存（关键优化）
DNS 查询过程开销大、延迟高、消息多。
因此使用**缓存**提升性能：
- 查询结果会被缓存在本地DNS服务器。
- 下次查询先查缓存，不用再访问根服务器。
- 缓存内容带有 **TTL（存活时间）**，过期失效。
- 解析失败的结果也会缓存，但TTL更短。

---

### 总结
本节课我们学习了：
- **DNS（域名系统）** 用于将人类可读域名转为 IP 地址。
- 是一个**分布式、层级化**的服务器系统。
- **缓存**是提升性能的关键。
- 支持一对多、多对一的域名/IP映射。

下节课：我们终于开始 Java 编程，学习 **java.net.InetAddress** 与 IP 地址。



## Application Layer & IP Addressing & Java InetAddress

### 上节课回顾

在之前的课程中，我们学习了互联网的核心组成部分：
- 网络体系结构的**分层模型**，重点是 TCP/IP 5 层模型（第2讲）
- **端口**：与进程绑定，而非与主机绑定（第3讲）
- **DNS 域名系统**：将人类可读的主机名映射为 IP 地址（第4讲）

---

### 本节课内容
从本节课开始，我们将进入**实际的 Java 网络编程**（共11讲）。
本节课重点：
1. 应用层基础
2. **IP 地址详解**（IPv4 / IPv6）
3. **Java InetAddress 类**：实现主机名与 IP 互转
4. 编写模拟 `nslookup` 的简单 Java 程序

---

### IP 寻址
互联网上的每台公开主机都有**唯一的 IP 地址**。
当前使用两种协议：
- **IPv4**：互联网协议第4版
- **IPv6**：互联网协议第6版

IPv6 正在逐步替代 IPv4，但目前暂无完全停用 IPv4 的时间表。

---

### IPv4
- 通常写成 **4 段十进制格式**：`a.b.c.d`
- 每段 0~255，共 4 字节
- 总地址数量约 **42.9 亿**
- 已远远不够全球设备使用

### 分类编址（早期）
- A 类：0.*.*.* ~ 127.*.*.*
- B 类：128.*.*.* ~ 191.*.*.*
- C 类：192.*.*.* ~ 223.*.*.*
- D 类：多播
- E 类：保留备用

### 分类编址的问题
- 地址空间浪费严重
- 很多机构用 B 类地址，但利用率极低
- 大量地址被保留，无法分配

---

### IPv4 解决方案
#### 1. CIDR 无类别域间路由
- 用**任意位数前缀**划分子网
- 写法：`a.b.c.d/x`，x 是前缀位数
- 灵活分配子网大小，避免浪费

#### 2. NAT 网络地址转换
- 内网使用私有地址，出口共用一个公网 IP
- 典型内网段：`10.*.*.*`
- 只是临时方案，非长久之计

---

### IPv6（长期解决方案）
- 地址长度：**16 字节（128 位）**
- 总地址数：约 **3×10³⁸**，几乎用不完
- 格式：8 组十六进制数，用冒号分隔
- 可省略前导零，连续零可用 `::` 代替
- 支持 CIDR 子网划分

---

### Java InetAddress 类
`java.net.InetAddress` 是 Java 中表示**IP 地址**的核心类。
- 同时支持 **IPv4 和 IPv6**
- 封装了**主机名 + IP 地址**
- 用于 Socket、ServerSocket、URL 等所有网络类

#### 特点
- **没有 public 构造方法**
- 必须用**静态工厂方法**创建对象
- 属于**不可变对象**，无 set 方法

---

#### 创建 InetAddress 的三种方法
1. `getByName(String hostname)`
   最常用，根据主机名获取 IP
2. `getAllByName(String hostname)`
   返回该主机对应的所有 IP 数组（多 IP 服务器）
3. `getLocalHost()`
   获取本机地址

这些方法会**自动访问 DNS**，可能抛出 `UnknownHostException`。

---

#### 常用获取方法（Getter）
- `getHostName()`：获取主机名
- `getHostAddress()`：获取 IP 地址字符串
- `getAddress()`：以字节数组返回 IP
- `isLoopbackAddress()`：判断是否为回环地址
- `isReachable(int timeout)`：类似 ping，测试是否可达

---

#### 简单 Java 示例：模拟 nslookup
```java
import java.net.*;

public class Lookup {
    private InetAddress inet = null;

    public void resolve(String host) {
        try {
            inet = InetAddress.getByName(host);
            System.out.println("Host name: " + inet.getHostName());
            System.out.println("IP Address: " + inet.getHostAddress());
        } catch (UnknownHostException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        Lookup lookup = new Lookup();
        lookup.resolve(args[0]);
    }
}
```

---

### 总结
- 本节课学习 **IP 地址**：IPv4、IPv6、CIDR、NAT
- Java 用 **InetAddress** 封装主机与 IP
- 工厂方法创建对象，自带 DNS 查询
- 可实现 `nslookup` 功能

---
下节课：**Java I/O Streams（Java I/O 流）**





## Java IO Streams

### 本节课内容
本节课我们将学习：
- Java 中的 **I/O 流模型**
- 字节流与字符流的区别
- 输入流 / 输出流
- 缓冲流、包装流
- 流在网络编程中的作用

---

### 什么是 I/O 流？
- **流（Stream）** 是数据在程序与外部之间传输的通道
- 可以是文件、网络连接、内存等
- 流是**单向**的：要么读，要么写
- 数据像水流一样连续传输

---

### 两大流分类
1. **字节流（Byte Stream）**
   - 以 **字节** 为单位传输
   - 适合图片、视频、文件等二进制数据
   - 顶层类：`InputStream`、`OutputStream`

2. **字符流（Character Stream）**
   - 以 **字符** 为单位传输
   - 适合文本数据
   - 顶层类：`Reader`、`Writer`

---

### 字节流基类
```java
InputStream  // 所有字节输入流的父类
OutputStream // 所有字节输出流的父类
```
- 抽象类
- 用于读取/写入原始字节
- 网络套接字底层使用字节流

---

### 字符流基类
```java
Reader   // 所有字符输入流父类
Writer   // 所有字符输出流父类
```
- 自动处理字符编码
- 适合文本通信

---

### 流的包装（流嵌套）
Java 流支持**包装模式**，给基础流增加功能：
- 缓冲：提高效率
- 转码：字节 ↔ 字符
- 按行读取

常用组合：
```java
// 套接字字节流 → 转为字符流 → 缓冲
BufferedReader in = new BufferedReader(
    new InputStreamReader( socket.getInputStream() )
);
```

---

### 核心流介绍

#### 1. InputStreamReader
- 将**字节流**转为**字符流**
- 必须用在套接字网络通信中

#### 2. BufferedReader
- 提供**缓冲**功能
- 支持 `readLine()` 按行读取文本
- 大幅提升性能

#### 3. PrintWriter
- 按行写文本
- 支持 `println()`
- 可开启自动刷新

---

### 网络编程中最常用的流组合
```java
// 读取服务器发来的文本
BufferedReader in = new BufferedReader(
    new InputStreamReader(socket.getInputStream())
);

// 向服务器发送文本
PrintWriter out = new PrintWriter(
    socket.getOutputStream(), true
);
```

---

### 流的重要特性
1. **阻塞特性**
   - 读流时如果没有数据，线程会一直等待
   - 直到数据到达或连接关闭

2. **单向性**
   - 一个流只能读或者只能写
   - 套接字需要**两个流**完成双向通信

3. **关闭**
   - 关闭包装流会自动关闭底层流
   - 关闭套接字会自动关闭所有相关流

---

### 总结
- Java I/O 分为**字节流**和**字符流**
- 网络编程必须用**包装流**
- `BufferedReader` + `PrintWriter` 是客户端/服务器标准搭配
- 流读写是**阻塞操作**
- 下一节开始学习 **Socket 客户端编程**





## Java Socket

### 本节课内容
本节课我们将学习：
- 应用程序如何通过**套接字（Socket）**与传输层对接
- Java 中的 **Socket 类** 详解
- 套接字的**输入流与输出流**
- 基于流的网络通信原理
- 两个完整示例：每日忠告客户端、KnockKnock 客户端

---

### 网络应用程序通信模型
- 应用层协议位于**传输层之上**
- 应用程序不直接读写网络数据包
- 应用程序通过**套接字（Socket）**访问网络服务
- 套接字是应用程序与传输层之间的**接口**

---

### 套接字（Socket）是什么？
- 套接字是**两台机器之间通信的端点**
- 代表一个**双向连接**
- 每个连接由**4个要素**唯一标识：
  1. 源IP
  2. 源端口
  3. 目标IP
  4. 目标端口
- 操作系统通过这4个值区分不同连接

---

### Java Socket 类
Java 使用 `java.net.Socket` 实现客户端TCP连接：
- 创建对象时**自动发起连接**
- 必须指定**主机名 + 端口号**
- 连接失败会抛出 `IOException`

常用构造方法：
```java
Socket(String host, int port)
Socket(InetAddress address, int port)
```

---

### 核心方法
```java
// 获取连接的输入流（读数据）
InputStream getInputStream()

// 获取连接的输出流（写数据）
OutputStream getOutputStream()

// 关闭套接字与所有流
void close()
```

- 一旦关闭，套接字**无法复用**
- 关闭流会自动关闭套接字

---

### 基于流的通信
- 套接字本质是**基于流**的通信
- 输入流：**读取**服务器发来的数据
- 输出流：**发送**数据到服务器
- 流是单向的，套接字是双向的

---

### 流的包装（常用）
原始流效率低，通常包装为：
```java
// 读取文本
BufferedReader in = new BufferedReader(
    new InputStreamReader(socket.getInputStream())
);

// 写入文本（自动刷新）
PrintWriter out = new PrintWriter(
    socket.getOutputStream(), true
);
```

---

### 阻塞特性
- 从套接字流中**读取数据是阻塞操作**
- 没有数据时，线程会一直等待
- 直到：
  1. 数据到达
  2. 连接关闭
  3. 超时抛出异常

---

### 示例1：每日忠告客户端
```java
Socket s = new Socket("date.example.com", 4242);

BufferedReader in = new BufferedReader(
    new InputStreamReader(s.getInputStream())
);

String advice = in.readLine();
System.out.println(advice);

s.close();
```

---

### 示例2：KnockKnock 客户端
```java
Socket kkSocket = new Socket("localhost", 2323);

PrintWriter out = new PrintWriter(kkSocket.getOutputStream(), true);
BufferedReader in = new BufferedReader(
    new InputStreamReader(kkSocket.getInputStream())
);

// 交互协议逻辑
String fromServer;
while ((fromServer = in.readLine()) != null) {
    System.out.println("服务器: " + fromServer);
    if (fromServer.equals("Bye.")) break;

    String fromUser = stdIn.readLine();
    if (fromUser != null) {
        System.out.println("客户端: " + fromUser);
        out.println(fromUser);
    }
}
```

---

### 客户端工作流程
1. 创建 Socket，指定**服务器IP + 端口**
2. 获取输入流、输出流
3. 按照应用层协议**收发数据**
4. 通信结束，关闭套接字
5. 退出程序

---

### 重点总结
- 客户端 Socket **主动发起连接**
- 每个 Socket 对应一个**唯一连接**
- 通信基于**输入流、输出流**
- 读写操作是**阻塞**的
- 通信完成必须**关闭资源**

---

### 下节课预告
学习**服务器端套接字（ServerSocket）**
- 如何监听端口
- 如何接受客户端连接
- 如何实现简单服务器



## Java ServerSocket

### 上节课回顾
上一讲我们学习了如何用 Java 编写网络客户端：
- 应用程序如何通过套接字与传输层对接
- 如何使用 java.net 包中的 **Socket 类**
- 每个套接字都有**输入流**和**输出流**，用于收发数据
- 通常会对原始流进行包装，至少加入**缓冲**
- 从套接字读取数据是**阻塞操作**——会一直等待直到有数据可读

---

### 本节课内容
本节课我们学习网络通信的另一半：**服务器**。
- 使用同样来自 java.net 的 **ServerSocket**
- 在指定端口监听，直到客户端发起连接
- 以 **Socket 对象**的形式接收客户端
- 这个 Socket 会使用与监听端口相同的端口号
- 讲解两个示例：DailyAdviceServer 和 KnockKnockServer
- 指出一个**核心局限性**，并在接下来4讲中解决

---

### 客户端 vs 服务器
网络架构本身**不区分**客户端和服务器，二者都是主机/终端系统。
核心区别在于**连接建立方式**：
- **客户端**：主动发起连接请求
- **服务器**：使用 ServerSocket **接受连接**

一旦通信开始，二者几乎没有区别，都用 Socket 通信。
应用层会区分二者，例如：浏览器（客户端）与 Web 服务器。

---

### 客户端与服务器的特点
**客户端**
- 假设服务器存在，且有固定 IP 和端口
- 启动 → 连接 → 按协议通信 → 关闭 → 退出

**服务器**
- 在主机上**持续运行**
- 在固定端口监听客户端连接
- 处理客户端连接/断开
- 实现通信协议

---

### 7 种基本套接字操作
1. 连接远程主机
2. 发送数据
3. 接收数据
4. 关闭连接
5. 绑定到监听端口
6. 监听入站连接请求
7. 接受远程主机连接

- 客户端只需要前 4 种
- 服务器需要全部 7 种

---

### ServerSocket 类
ServerSocket 提供服务器专属的核心功能：
- 打开指定端口，允许外部连接
- 在该端口监听 TCP 连接
- 协商客户端与服务器的连接
- 为每个客户端创建一个普通 **Socket** 用于通信

其余通信功能都由普通 Socket 类提供。

---

### 最常用构造方法
```java
public ServerSocket(int port) throws BindException, IOException
```
- port：要监听的端口号
- 主机固定为**本地主机（localhost）**
- 与客户端 Socket 不同，不需要指定远程地址
- BindException：无法绑定端口时抛出（属于 IOException）

---

### 常用获取方法（Getter）
- `public InetAddress getInetAddress()`
  返回服务器使用的地址
- `public int getLocalPort()`
  返回服务器正在监听的端口

这些属性**没有公共 setter**，是不可变的。
缓冲区大小、超时等可以设置。

---

### 重要方法
1. **`public Socket accept() throws IOException`**
   - 阻塞（一直等待）直到客户端连接
   - 返回一个新的 Socket，用于与该客户端通信

2. **`public void close() throws IOException`**
   - 释放监听端口，供其他程序使用
   - 同时关闭所有已连接的 Socket
   - 服务器不在无限循环时应调用
   - 用 Ctrl+C 终止程序通常也会释放端口

---

### 简单服务器编写步骤
1. 在指定端口创建 ServerSocket
2. 调用 `accept()` 监听连接，阻塞直到客户端连接，返回 Socket
3. 为 Socket 设置输入/输出流
4. 按约定协议通信
5. 客户端或服务器关闭连接
6. 返回步骤 2 继续监听

协议可封装到单独的类中。

---

### 示例 1：每日忠告服务器（DailyAdviceServer）
```java
try {
    ServerSocket serverSock = new ServerSocket(4242);
    while (true) {
        Socket sock = serverSock.accept();
        // 记录客户端地址等
        PrintWriter writer = new PrintWriter(sock.getOutputStream());
        String advice = getAdvice();
        writer.println(advice); // 发送给客户端
        writer.close();
        sock.close();
    }
} catch (IOException ex) { ... }
```

---

### 示例 2：KnockKnock 服务器
使用**独立协议类**处理与客户端的通信：
`KnockKnockProtocol`

将连接管理与通信逻辑分离，便于后续扩展为多客户端服务器。

#### 初始化监听端口
```java
serverSocket = new ServerSocket(2323);
kkp = new KnockKnockProtocol();
```

#### 主循环
```java
while (true) {
    clientSocket = serverSocket.accept();

    PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);
    BufferedReader in = new BufferedReader(
        new InputStreamReader(clientSocket.getInputStream()));

    String outputLine = kkp.processInput(null);
    while ((inputLine = in.readLine()) != null) {
        outputLine = kkp.processInput(inputLine);
        out.println(outputLine);
        if (outputLine.equals("Bye.")) break;
    }
    out.close();
    in.close();
    clientSocket.close();
}
```

---

### KnockKnockServer 说明
- PrintWriter 开启**自动刷新**：println、printf 会自动刷新缓冲区
- InputStreamReader 通过流包装实现缓冲
- 协议逻辑由独立类 `KnockKnockProtocol` 处理
- 服务器是**串行**的：一次只能处理一个客户端

---

### KnockKnockProtocol 核心逻辑
用状态变量标记协议阶段：
- WAITING：等待
- SENTKNOCKKNOCK：已发送敲门
- SENTCLUE：已发送线索
- ANOTHER：再来一个

```java
public String processInput(String theInput) {
    if (state == WAITING) {
        theOutput = "Knock! Knock!";
        state = SENTKNOCKKNOCK;
    } else if (state == SENTKNOCKKNOCK) {
        if (theInput.equalsIgnoreCase("Who's there?")) {
            theOutput = clues[currentJoke];
            state = SENTCLUE;
        } else {
            theOutput = "你应该说 Who's there! 再来一次。Knock! Knock!";
        }
    }
    return theOutput;
}
```

---

### 局限性（重点）
两个示例都有**严重局限**：
- 同一时间**只能处理一个客户端**
- 只有一个协议实例
- 处理当前客户端时，无法接受新客户端
- 无法同时服务多个用户

启动多个服务器也不行：**同一个端口只能被一个程序绑定**，第二个会报 BindException。

---

### 更好的方案
将客户端连接交给**独立线程**处理，主线程继续监听。
这种**多线程服务器**方案将在接下来几讲讲解。

---

### 总结与下节课
本节课我们学习了：
- 用 ServerSocket 实现简单服务器
- 通过 `accept()` 在固定端口监听客户端连接
- 为每个客户端打开连接（端口不同）
- **只能同时处理一个客户端**

接下来3讲，我们将学习如何用**线程**实现**同时处理多个客户端**的服务器。





## Threads

### 上节课回顾

前两讲我们学习了如何用 Java 实现**客户端**与**简单服务器**。

- 客户端使用 **Socket 类**：连接指定服务器地址与端口，按照约定协议通信。
- 服务器使用 **ServerSocket 类**：调用 `accept()` 监听指定端口；连接建立后，`accept()` 返回一个 Socket 对象，用于执行服务端协议逻辑。

------

### 简单服务器的问题

我们提到了简单（单线程）服务器的关键局限：

1. **`accept()` 是阻塞方法**：只有客户端连接时才返回，否则整个服务器一直等待。
2. **同一时间只能处理一个客户端**：其他客户端会排队等待，造成延迟。
3. **通信期间服务器频繁空闲**：等待客户端响应时，线程无事可做。
4. **一个服务器对应一个协议处理器**，而非每个客户端一个。

------

### 本节课内容

简单的 “每个客户端一个协议处理器” 虽然直观，但上述问题很严重。

解决方案有两种：

1. 使用 **java.nio 提供的非阻塞通信**（第 12 讲讲解）。
2. 使用**并发线程**：一个或多个客户端对应一个线程（接下来 3 讲重点）。

本节课开始，我们用 3 讲时间学习**并行计算**。

------

### 为什么需要并行计算

现代硬件几乎全是并行架构，并行编程已成为必备技能。

本课程（BCS 认证课程）要求必须覆盖并行编程内容。

### 摩尔定律与架构演变

1965 年，戈登・摩尔提出经验规律：

芯片上的晶体管密度每 **18~24 个月翻一番**。

虽然摩尔定律仍有效，但**处理器主频不再同步增长**，核心瓶颈是**发热**。

------

### 并行的优势

提升性能的核心方式：让多个计算**同时执行**。

### 自动并行的局限

芯片设计者已尝试自动化并行：

- **指令级并行（ILP）**：流水线架构，像工厂流水线分阶段处理指令。

- **超标量架构**：CPU 多运算单元（FPU/ALU）独立工作。

    但这些方式无法无限扩展。

------

### 主流并行硬件架构

1. **共享内存架构**

    所有处理单元（核心 / CPU）访问**同一块内存**。

    适用：现代台式机、笔记本、手机等几乎所有单机设备。

    

2. **分布式内存架构**

    每个处理单元只访问**部分内存**。

    适用：超算集群、云计算分布式系统。

    

3. **GPU（图形处理器）**

    专为图形渲染、大规模并行计算设计。

    现广泛用于机器学习、加密货币等非图形场景，称为 **GPGPU（通用 GPU）**。

    

------

### 并行与并发

#### 并发（Concurrency）

同一时间段内**多个任务都在推进**，不一定同时执行。

例如：GUI 事件驱动，主线程持续运行，回调在独立任务（线程）中处理。

操作系统通过**时间片轮转 / 抢占式多任务**实现。

#### 并行（Parallelism）

利用**多个处理单元**真正**同时执行**多个计算。

- 并行 ⇒ 一定并发
- 并发 ≠ 一定并行（单核 CPU 也能并发）

------

### 进程 vs 线程

#### 进程（Process）

- 独立执行环境，拥有**私有运行时资源**。
- 独立堆内存、栈内存。
- 创建 / 销毁成本**高**。
- 通常：1 个应用 = 1 个进程（也可多进程）。

#### 线程（Thread）

- 由进程创建，**在进程内部运行**。
- 每个进程至少有 1 个线程（Java 主线程）。
- 有独立栈，但**共享进程堆内存**。
- 轻量级，创建 / 销毁成本**低**。
- 调度与核心分配由操作系统**调度器**决定。

------

### 并行编程的语言与框架

多数语言都支持并行编程：

- C/C++：OpenMP、Cilk、pthread、C++11 原生线程
- Python：threading 库（受 GIL 限制）
- **Java**：语言级原生支持多线程（`java.lang.Thread`、`java.util.concurrent`）

------

### 总结与下节课

本节课重点：

- 并行计算的重要性
- 共享内存 vs 分布式内存
- 并发 vs 并行
- 进程 vs 线程

接下来两讲，我们学习**Java 多线程服务器的多种实现方式**



## Java Threads & Multi Threaded Server

### 上节课回顾
- 两讲之前：我们用 **ServerSocket** 实现了简单 Java 服务器
  - 调用阻塞的 `accept()` 方法等待客户端
  - **同一时间只能处理一个客户端**
  - 例子：DailyAdviceServer、KnockKnockServer
- 上一讲：我们学习了**并行计算基础**
  - 并行硬件的发展历史
  - 共享内存 vs 分布式内存
  - 并行性 vs 并发
  - **进程 vs 线程**

---

### 本节课内容
本节课我们将学习：
- 如何用 Java 实现**多线程服务器**
- 使用 Java 内置的 **Thread 类**
- 基于**共享内存**（单机多核/集群单节点）
- 模型：**一个客户端一个线程（thread‑per‑client）**
- 下一讲会介绍两种**线程池**方案，替代本模型

首先学习 Java 并行编程基础。

---

### Java 线程实现方式
Java 有两种基础线程实现方式：
1. 继承 **Thread 类**（java.lang）
2. 实现 **Runnable 接口**

两种方式都需要把业务代码写在：
`public void run()`

启动线程执行 run() 方法，必须调用：
`public void start()`

常用辅助方法：
- `join()`：等待该线程执行完毕
- `sleep(long millisecs)`：让线程休眠

---

### 调度器（Scheduler）
线程不是创建后立刻运行。
线程何时执行由操作系统的**调度器**管理。
调度器会根据其他应用、后台任务等动态分配 CPU 时间。

因为无法控制外部程序与系统任务，**并行程序每次运行结果可能不同**。
这种**不确定性**通常需要避免。
可以用**同步（synchronisation）**解决（本节课后半部分）。

---

### 方式1：继承 Thread 类
代码示例：HelloT.java
```java
public class HelloT extends Thread {
    public void run() {
        System.out.println("Hello from a thread.");
    }

    public static void main(String args[]) {
        HelloT t = new HelloT();
        t.start(); // 调度执行
    }
}
```
`t.run()` 何时真正被调用，由调度器决定。

---

### 运行多个线程
```java
public class HelloT extends Thread {
    public void run() { ... }

    public static void main(String args[]) {
        HelloT t1 = new HelloT();
        t1.start(); // 启动线程1

        HelloT t2 = new HelloT();
        t2.start(); // 启动线程2
    }
}
```
调用 `start()` 只是启动线程，**执行时机仍由调度器控制**。

---

### 方式2：实现 Runnable 接口
代码示例：HelloI.java
```java
public class HelloI implements Runnable {
    public void run() {
        System.out.println("Hello from a thread.");
    }

    public static void main(String args[]) {
        HelloI h = new HelloI();
        Thread t = new Thread(h);
        t.start();
    }
}
```
这种方式是**使用线程**，而不是**成为线程**。

---

### 线程编程常见问题
两个核心问题：**数据竞争**、**同步**。

#### 数据竞争（Data Race）
多个线程同时读写**同一内存位置**，结果取决于线程执行顺序。
```
线程1：globalData = 1;
       a = globalData;
线程2：globalData = 2;
```
a 的值是 1 还是 2？无法确定。
因为无法控制线程执行顺序，结果**每次运行都可能不同**（不确定性）。

---

### 同步（Synchronisation）
当一个线程必须等待另一个线程完成时，必须做同步。
两种常用方式：

1. **`t.join()`**
   阻塞调用线程，直到子线程 t 运行结束。

2. **同步代码块 / 同步方法**
   同一时间只允许一个线程进入。

---

### 同步（1）：join()
```java
t = new Thread();
t.start();
// 主线程与 t 并发运行

t.join();
// 主线程阻塞，直到 t.run() 执行完毕
```

---

### 同步（2）：同步代码块
指定**同一时间只能有一个线程进入**的代码块。
Java 使用 `synchronized(对象)` 实现：
```java
synchronized(System.out) {
    System.out.print("Socket host: " + so.getInetAddress());
    System.out.print(" on port: " + so.getPort());
    System.out.println();
}
```
不加同步，多个线程的打印内容会**交错混乱**。

---

### 同步（3）：同步方法
Java 支持直接把方法声明为 `synchronized`：
```java
public synchronized void printStatus() {
    System.out.print("Socket host: " + so.getInetAddress());
    System.out.print(" on port: " + so.getPort());
    System.out.println();
}
```
效果和同步代码块一致。
注意：**过度使用 synchronized 会严重影响性能**。

---

### 同步（4）补充说明
有些场景可以合并打印语句避免同步。
- PrintStream、PrintWriter **内部已做同步**
- OutputStream 一般**不做同步**
  → 输出到同一日志文件时需要同步

多线程服务器必须注意：
多个线程是否会写入**同一全局数据、文件、数据库**等。
只要至少一个线程在写，就可能出现**数据竞争**，需要同步。

---

### 客户端—服务器架构选择
服务器架构由应用需求决定：
- 预期**多少并发客户端**？
- 客户端连接**持续多久**？
- 通信类型：持续交互还是间歇通信？

例子：
- FTP 服务器：大量**短连接**
- 聊天服务器：较少**长连接**

---

### 多线程 Knock‑Knock 服务器
把原 KnockKnockServer 改为 **KKMultiServer**：
- 仍只有一个主线程
- 每次 `accept()` 都会创建一个新的 **KKClientHandler**
- KKClientHandler 继承自 Thread
- 构造方法传入客户端 Socket
- **每个客户端一个独立协议实例**（KnockKnockProtocol 无需修改）
- 客户端 KnockKnockClient 完全不用改

---

### KKMultiServer 代码
```java
public class KKMultiServer {
    public static void main(String[] args) throws IOException {
        boolean listening = true;
        ServerSocket serverSocket = null;

        try {
            serverSocket = new ServerSocket(2323);
        } catch (IOException e) {
            System.err.println("Could not listen on port: 2323.");
            System.exit(-1);
        }

        // 每 accept 一个客户端就新建一个线程
        while (listening)
            new KKClientHandler(serverSocket.accept()).start();

        serverSocket.close();
    }
}
```

---

### KKClientHandler 代码
```java
public class KKClientHandler extends Thread {
    private Socket socket = null;

    public KKClientHandler(Socket socket) {
        super("KKClientHandler");
        this.socket = socket;
    }

    public void run() {
        try (
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream()));
        ) {
            String inputLine, outputLine;
            KnockKnockProtocol kkp = new KnockKnockProtocol();
            outputLine = kkp.processInput(null);
            out.println(outputLine);

            while ((inputLine = in.readLine()) != null) {
                outputLine = kkp.processInput(inputLine);
                out.println(outputLine);
                if (outputLine.equals("Bye."))
                    break;
            }
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

### 本节课总结
本节课我们学习：
- Java 多线程基础
- 第一种多线程服务器实现：
  **thread‑per‑client（一个客户端一个线程）**
- 缺点：**线程数量无限制增长**，资源不可控

下一讲介绍两种**线程池模型**，解决资源无限增长问题。
本讲代码已发布在 Minerva。

---





## Threads Pool & Executor Server

### 上节课回顾
上一讲我们学习了 Java 多线程编程，以及**第一种多线程服务器模型**：
- **单客户单线程（thread-per-client）**
  主线程为每个客户端单独启动一个处理线程。
- 优点：可同时处理多个客户端，实现简单。
- 缺点：大量客户端连接会导致**资源不可控增长**，降低性能。

---

### 本节课内容
今天我们学习两种**使用有限数量线程**的替代方案：
1. **线程池（thread pool）**
   固定线程数，控制资源占用。
   需提前预估线程数量。
2. **执行器服务器（Executor server）**
   Java 提供的 `Executors` 工具，更灵活。
   是本课讲解的**第三种服务器架构**。

---

### 线程池服务器
基本思路：使用**固定数量的线程**处理客户端。
也叫 **threads-per-server**（线程数由服务器设定，而非客户端）。
- 所有线程在监听端口处排队。
- 第一个线程的 `accept()` 会阻塞其他线程，直到新客户端连接。
- 效果如同多个服务器共用同一个监听端口。

---

### 实现思路
本质上，每个线程都运行第8讲的**单线程串行服务器**逻辑：
- 程序启动时创建固定数量线程。
- 所有线程监听**同一个端口**（线程可实现，进程不行）。
- 每个线程调用阻塞的 `accept()`。
- `accept()` 返回后，每个线程**一次处理一个客户端**。

---

### 线程池服务器（代码框架）
```java
public class ThreadPoolServer {
    public void runServer(int poolSize) {
        ServerSocket serverSock = new ServerSocket(2323);

        for (int i = 0; i < poolSize; i++) {
            ServerThread s = new ServerThread(serverSock);
            s.start();
        }
    }
}
```
- 始终只有一个 ServerSocket，被所有线程共享。
- 因此只占用一个监听端口。
- poolSize 可设为静态变量，由命令行传入。

---

### 服务线程（代码框架）
```java
public class ServerThread extends Thread {
    private ServerSocket serverSock = null;

    public ServerThread(ServerSocket s) {
        serverSock = s;
    }

    public void run() {
        while (true) {
            Socket client = serverSock.accept();
            Protocol p = new Protocol(client);
            p.handleClient();
        }
    }
}
```
每个服务线程**连续处理多个客户端**。

---

### 线程池运行机制
- 线程池大小是**固定参数**。
- 每个线程是运行 `accept()` 的串行服务器。
- 线程在监听端口处排队。
- 哪个线程从 `accept()` 返回由 JVM 和调度器决定，**每次运行不确定**。
- 客户端断开后，线程回到循环开头再次调用 `accept()`，即**回到线程池**。

---

### 线程安全问题
多个线程同时对**同一个 ServerSocket 调用 accept()**。
问题：
- `accept()` 能否正常工作？
- 会不会把同一个客户端分给多个线程？
- **`accept()` 是线程安全的吗？**

官方文档没有明确说明。
不同 JVM 实现可能不一样。
**原则：如果一个类没有明确声明线程安全，就默认不安全。**

---

### 实现线程安全的 accept()
使用 `synchronized` 保证同一时间只有一个线程调用 `accept()`：
```java
public void run() {
    while (true) {
        synchronized (serverSock) {
            Socket client = serverSock.accept();
        }
        Protocol p = new Protocol(client);
        p.handleClient();
    }
}
```
这样就不再依赖 `accept()` 本身是否安全。
但哪个线程先进入同步块仍然不确定。

---

### 线程池模型 优缺点
**优点：**
- 可在同一端口处理多个客户端。
- 资源**有限且可控**。
- 客户端连接之间不会频繁创建/销毁线程。

**缺点：**
- 必须根据预期负载**调整线程池大小**。
- 太小：客户端需要等待。
- 太大：开销增加，整体变慢。
- 理想情况：能**动态调整**线程数。

---

### 执行器服务器
理想目标：
- 线程空闲时**复用**，不重复创建。
- 所有线程都忙时，**才创建新线程**。

用底层 `Thread` 实现很麻烦，
Java 提供了高层 **Executor 框架**，位于 `java.util.concurrent`。

---

### java.util.concurrent 包
`java.lang.Thread` 是**低层次**并发工具。
Java 5 引入了更高层次的模型：`java.util.concurrent`。
- **调度与执行分离**。
- 让我们管理线程使用，创建/销毁细节交给系统。
- 性能由 JVM 保证。

---

### newCachedThreadPool
创建**弹性缓存线程池**：
- 现有线程都忙 → 创建新线程。
- 线程空闲 → 复用。
- **自动适应客户端数量**。

也提供 `newFixedThreadPool(...)`，固定线程数，
效果与我们手动写的线程池一样，缺点也相同。
两种线程池**只需改一行代码**即可切换。

---

### 使用方式
```java
ExecutorService service = Executors.newCachedThreadPool();
service.submit(new KKClientHandler(client));
```
- `submit()` 接收 `Runnable` 或 `Thread`。
- 由框架自动调度执行。

---

### KKExecutorServer 完整代码
```java
public class KKExecutorServer {
    public static void main(String[] args) throws IOException {
        ServerSocket server = null;
        ExecutorService service = null;

        server = new ServerSocket(2323);
        service = Executors.newCachedThreadPool();

        while (true) {
            Socket client = server.accept();
            service.submit(new KKClientHandler(client));
        }
    }
}
```

---

### 执行器服务器 优缺点
**优点：**
- 资源用尽才创建新线程，更节省资源。
- 只需一行代码就能切换固定/缓存线程池。

**缺点：**
- 线程数**无上限**，仍可能耗尽内存或卡顿。
- 长连接客户端会长期占用资源。
- 更精细控制（如最大线程数）可使用 `ThreadPoolExecutor`，本课不深入。

---

### 如何选择架构
取决于：
- 应用需求
- 协议特点（是否耗资源、是否计算密集）
- 预期并发连接数
- 用户行为（连接时长、通信频率）

注意区分：
- **设计**：客户端-服务器架构
- **通信**：客户端-服务器协议

同一架构可复用于不同协议。

---

### 总结与下节课
本节课学习了**两种线程池服务器**：
1. **线程池模型**：每个线程相当于独立服务器，共用 ServerSocket。
2. **执行器服务**：高层多线程调度框架。

加上上一讲的 **单客户单线程**，本课共讲解 **3 种服务器架构**。

下节课：另一种提升服务器性能的方案 —— **非阻塞 I/O（NIO）**。



## Java NIO（重要）
### 上节课回顾（要考）

在前面几节课中，我们学习了**多线程服务器**如何同时服务多个客户端。
每个客户端都有独立的处理器（handler）。
处理器要么继承自 `Thread`，要么实现 `Runnable` 接口。
我们可以使用高层的 `Executor` 来方便地管理**固定大小或弹性大小的线程池**。

但每个线程**同一时间仍然最多只处理一个客户端**。
这可能造成**线程资源浪费**。

---

### 本节课内容
今天我们学习一种提升性能的替代方案：**非阻塞 I/O**。
- 阻塞 I/O 与非阻塞 I/O 的对比
- `java.nio` 与 `java.io` 的区别
- `Buffer`、`Channel`、`Selector` 三大核心类
- 如何应用到服务器架构

本节课不深入细节。

---

### 基于 java.io 的阻塞 I/O
`java.io` 中的 `read()`、`write()` 都是**阻塞方法**。
执行这些操作的线程会一直空闲等待，直到连接建立、数据到达等。
**浪费资源**，但实现简单。

多线程服务器可以优化资源利用：
当一个线程空闲时，调度器会挂起它并运行其他线程。
但如果每个线程都处理**长连接、低频率通信**的客户端，仍然会浪费 CPU。

---

### 超时异常
阻塞方法如果一直等不到客户端响应会**卡死**。
可以设置超时：
`Socket.setSoTimeout(超时毫秒)`
超时会抛出 `SocketTimeoutException`。
但这**仍然浪费CPU资源**。

---

### 基于 java.nio 的非阻塞 I/O
`java.nio` 提供**非阻塞 I/O**，最初为**高性能服务器**设计。

- 长连接客户端对线程池仍然不友好
- 阻塞 I/O **必须使用线程**
- 多线程会带来**同步问题**
- `java.nio` 允许**单线程处理多个客户端**
- 但**业务逻辑更复杂**

---

### Java 核心类
非阻塞 I/O 最重要的三个组件：
1. **Buffer（缓冲区）**：存放数据
2. **Channel（通道）**：I/O 对象的容器（如 Socket）
3. **Selector（选择器）**：管理多个通道

- `Buffer` 在 `java.nio`
- `Channel` 和 `Selector` 在 `java.nio.channels`

---

### 缓冲区（Buffer）
- **非流模式**的 I/O 容器
- 供 Channel 进行 I/O 操作
- 以**大数据块**传输，而非单个字节
- **可双向读写**（对比 java.io 流是单向的）
- 直接映射操作系统底层缓冲区，效率更高

---

### 通道（Channel）
- 代表可轮询的 I/O 目标（如 Socket）
- 可设置为**阻塞/非阻塞**
- **双向通信**
- 从关联的 Buffer 读写数据
- 向 Selector **注册**，由 Selector 监控状态（可读、可写等）

---

### 选择器（Selector）
- 管理一组注册的 Channel
- `select()` 方法查询所有通道
- 返回**就绪**的通道（可接收、可读、可写）

---

### 通道注册
创建 Selector：
`Selector selector = Selector.open();`

注册通道：
`serverChannel.register(selector, SelectionKey.OP_ACCEPT);`

常用事件：
- `OP_ACCEPT`：服务器监听连接
- `OP_READ`：可读
- `OP_WRITE`：可写

---

### 典型事件循环（单线程）
```
while (true) {
    selector.select();
    获取就绪键集合迭代器

    while (有下一个键) {
        取出键并移除
        如果键无效则跳过

        if (可接收) 处理连接
        else if (可读) 读取数据
        else if (可写) 发送数据
    }
}
```

这是**单线程、事件驱动模型**。

---

### 接收客户端连接
1. 获取服务器通道
2. 调用 `accept()` 得到客户端通道
3. 设置为**非阻塞**
4. 向 Selector 注册 `OP_READ` 监听读事件

---

### 从客户端读取
1. 分配 ByteBuffer
2. 从通道读取数据到缓冲区
3. 读取为 -1 表示连接关闭
4. 保存消息，注册 `OP_WRITE` 准备回复

---

### 向客户端写入
1. 从 HashMap 取出消息
2. 通过 `channel.write()` 发送
3. 重新注册 `OP_READ` 等待下一条消息

---

### 非阻塞 I/O 优缺点
- 概念上比多线程简单，但**实现更难**
- 读写切换逻辑复杂
- 刚推出时性能远超阻塞 I/O
- 但随着线程调度优化，优势逐渐缩小

---

### 今天的非阻塞 I/O
- 普通服务器可轻松支持 **约1万线程**
- 基于流的多线程服务器**性能可高 30%**
- 非阻塞 I/O 仍适合：**大量长连接、低活跃**的场景
- 这类场景下阻塞 I/O 浪费资源严重

---

### 总结
本节课学习：
- Java `java.nio` 非阻塞 I/O
- 单线程维护大量连接
- 使用 **Buffer + Channel + Selector**
- 代码比多线程更复杂

下节课：**安全与安全套接字**

需要我把这份内容整理成**考试背诵版精简要点**吗？



## 网络安全

### 往期课程回顾
在之前的课程中，我们学习了如何实现**可同时处理多个客户端**的服务器：
- **多线程服务器**：每个客户端处理器独立运行在自己的线程上，Java 中可通过 Executor 方便实现。
- **非阻塞 I/O**：单线程可处理多个客户端，但开发成本更高，由 Java 的 `java.nio` 包实现，在现代机器上效率不如多线程服务器。

---

### 本节课内容
本节课重点讲解**网络安全**：
- 安全网络通信
- 私钥与公钥加密
- 身份认证与数字证书
- Java 实现：`SSLSocket` 类

本讲仅为概述；部分同学后续会选修大三课程 **COMP3911 安全计算**，会更深入讲解这些内容。

---

### 网络安全发生在哪些层？
需要在**多层**实现安全保障：
- 应用层：可快速部署新安全机制
- 网络层：安全覆盖范围广，但无法做用户身份认证

| 层次       | 安全协议示例                        |
| ---------- | ----------------------------------- |
| 应用层     | PGP（良好隐私协议）                 |
| 传输层     | SSL（安全套接字层，用于 TCP 连接）¹ |
| 网络层     | VPN（虚拟专用网，基于 IPsec）       |
| 数据链路层 | WEP（有线等效保密，用于 Wi‑Fi）     |
| 物理层     | 量子通信（未来方向）                |

¹SSL 实际位于应用层与传输层之间，但对应用层表现为传输层协议——详见本节课后段。

---

### 核心概念
Java 中**基于标准 Socket 的通信本质上是不安全的**：
- 网络流量**未加密**，可被截获
- 若消息加密，即使被截获也难以读取

由此引出两个问题：
1. **加密问题**：如何防止通信内容被窃听
2. **认证问题**：如何确认连接的是真实服务器（如登录场景）

---

### 安全核心目标
需要解决两个方面：
1. **加密**：流量即使被截获也安全
2. **认证**：客户端能确认连接到目标服务器（服务器认证）

本节课不讨论客户端认证。
两者结合可达到可接受的安全程度，**没有任何系统是绝对安全的**。

---

### 加密原理
- 原始明文消息：M
- 加密算法 E：将 M 加密为密文 C = E(M)
- 解密算法 D：将 C 还原为 M = D(C)

加密/解密算法 E、D 是公开的，因此必须配合**密钥**使用：无密钥则无法预测 E、D 的效果。

> 注：算法设计不在本课程范围内，部分同学可选修大三课程 **COMP3223 密码学**。

---

### 对称密钥算法
也称为**私钥密码学**
通信双方共享**同一密钥 k**：
- C = Eₖ(M)
- M = Dₖ(C)

双方使用相同密钥，因此称为**对称**。
标准算法：DES（数据加密标准）、AES（高级加密标准）。

工作流程：
1. 客户端向服务器请求密钥 k
2. 服务器发送 k
3. 客户端用 k 加密消息并发送
4. 服务器接收并用 k 解密

---

### 对称密钥的问题
- 密钥必须**提前安全分发**，若明文传输会被截获
- 需通过其他渠道传递，物理预装密钥不适合网络通信
- 任何持有密钥的人都能读取全部通信内容
- 攻击者可截获并转发消息，不易被发现
  （量子通信可检测此类截获行为）

---

### 非对称密钥算法
也称为**公钥密码学**
每个通信方拥有一对**私钥 / 公钥**：kₚᵥₜ（私钥）、kₚᵤᵦ（公钥）

发送流程：
1. 获取接收方的**公钥 kₚᵤᵦ**
2. 用公钥加密：C = E<sub>kpub</sub>(M)
3. 接收方用**私钥**解密：M = D<sub>kprv</sub>(C)

即使密文 C 被截获，没有私钥也无法解密；私钥**从不外传**。
公钥与私钥存在特殊数学关联，但无法从公钥推导出私钥。
标准实现：**RSA** 算法。

---

### 实际应用方案
- 对称密钥：代码执行**效率高**
- 非对称密钥：**计算开销大**

常用折中方案（混合加密）：
1. 用**非对称算法**安全传输一个简短的**会话密钥**（对称密钥）
2. 用该会话密钥 + **对称算法**加密/解密大量通信数据
密钥安全 → 对称加密通信安全。

---

### 中间人攻击（MITM）
公钥是公开的，任何人都可用它加密。
接收方无法确认消息来源。

攻击场景：
1. A 想给 B 发消息，请求 B 的公钥 k<sup>B</sup>ₚᵤᵦ
2. 攻击者 M 截获响应，把自己的公钥 k<sup>M</sup>ₚᵤᵦ 发给 A
3. A 用 k<sup>M</sup>ₚᵤᵦ 加密消息
4. M 截获消息，用自己私钥解密读取
5. M 再用 k<sup>B</sup>ₚᵤᵦ 加密转发给 B

这就是**中间人攻击**。

---

### 身份认证
为传输的公钥**增加可信度**。
- 服务器向新客户端发送**数字证书**，包含自身公钥 k<sup>S</sup>ₚᵤᵦ
- 证书可保证公钥确实来自该服务器
- 客户端可验证证书有效性
- 之后客户端再发送自己的公钥用于通信

证书由**受信任的认证机构（CA）**签名，伪造难度极高。
Java 使用标准 **X.509 证书**。

---

### 获取证书
- 商业机构向认证机构购买证书（如 SSL 证书由 VeriSign 签发）
- 可使用 Java 自带的 **keytool** 工具生成和管理证书
实现安全通信必须使用证书。

---

### Java 安全相关组件
Java 提供安全通信包：
- **JSSE**（Java 安全套接字扩展）：`javax.net.*`
- 包含 **SSL**（安全套接字层）：`javax.net.ssl.*`
- 包含更新的 **TLS**（传输层安全）

这些协议位于**应用层与传输层之间**，
严格来说打破了 5 层 TCP/IP 模型（但不违反 7 层 OSI 模型，见第 2 讲）。

---

### SSLSocket 类
`SSLSocket` 由 `SSLSocketFactory` 构造。
使用工厂模式（而非直接构造）可支持更多安全特性（如认证）。

`SSLSocket` 是在普通 Socket 基础上增加安全层：
```java
public class SSLSocket extends Socket
```
创建后用法与普通 Socket 一致。

示例：
```java
SSLSocketFactory factory = (SSLSocketFactory) SSLSocketFactory.getDefault();
SSLSocket socket = (SSLSocket) factory.createSocket(host, port);
```

---

### 类使用细节
代码见学习平台：`ListCipherSuites.java`（并非所有系统都能运行）。
通过选择不同工厂，可指定不同的认证/加密方法与算法。
- `getDefault()`：返回支持**服务器认证 + 加密通信**的工厂
- `getSupportedCipherSuites()`：获取支持的加密套件
- `getEnabledCipherSuites()`：获取当前启用的加密套件

加密套件需客户端与服务器协商。
网络通信功能继承自普通 `Socket`。

> 注：2024 年 11 月在 feng-linux.leeds.ac.uk 可正常运行。

---

### SSLServerSocket 类
在普通 `ServerSocket` 基础上增加安全层：
```java
public class SSLServerSocket extends ServerSocket
```
创建后用法与普通 `ServerSocket` 一致，继承所有网络功能。
所有尝试连接的客户端**必须遵守服务器的安全协议**，
避免恶意客户端故意要求弱安全策略。

---

### 回显服务器代码片段
代码见学习平台：`EchoServer.java`
需先用 keytool 配置证书¹
```java
private void runServer() {
    try {
        SSLSocket sslsocket = (SSLSocket) sslserversocket.accept();
        BufferedReader bRead = new BufferedReader(
            new InputStreamReader(sslsocket.getInputStream()));
        String string = null;
        while ((string = bRead.readLine()) != null) {
            System.out.println(string);
            System.out.flush();
        }
        sslsocket.close();
        sslserversocket.close();
    } catch (IOException ex) { ... }
}
```
¹见练习 3 第 2 题，已在 feng-linux.leeds.ac.uk 测试通过。

---

### 回显客户端代码片段
代码见学习平台：`EchoClient.java`
与不安全客户端相比，改动极小。
```java
private void runClient() {
    try {
        BufferedReader bIn = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bOut = new BufferedWriter(
            new OutputStreamWriter(sslsocket.getOutputStream()));
        String string = null;
        while ((string = bIn.readLine()) != null) {
            bOut.write(string + '\n');
            bOut.flush();
        }
        sslsocket.close();
    } catch (IOException ex) { ... }
}
```
通过 `bOut.write()` 发送的内容**已被加密**。

---

### 总结与下次课程
本节课简要介绍了网络安全：
- 对称密钥算法（仅私钥）
- 非对称密钥算法（私钥 + 公钥）
- 身份认证的必要性
- Java 中的 `SSLSocket`

到目前为止，我们使用的都是 **TCP** 协议。
下节课讲解另一种常用传输层协议：**UDP**。

要不要我帮你把这一讲整理成**考试必背精简版**？



## UDP
### 往期课程回顾
到目前为止，我们所有的客户端–服务器示例都使用了 **Socket、ServerSocket** 或它们的子类（如 SSLSocket）。
- 位于**应用层**
- 使用传输层协议 **TCP（传输控制协议）**
- 在两台主机间建立**持久连接**
- 互联网上收发消息最常用的协议

---

### 本节课内容
今天我们学习**另一种协议**：**UDP（用户数据报协议）**
- 无连接协议：**没有持久连接**
- Java 中通过 `java.net` 包的两个新类实现：
  - **DatagramPacket**（数据报包）
  - **DatagramSocket**（数据报套接字）
- 看一个基于 UDP 的客户端–服务器示例
- 第16讲会更深入讲解 UDP（与 TCP）的传输层细节
- 本讲聚焦**应用层视角**需要知道的内容

---

### TCP（传输控制协议）
- **可靠**：丢失/损坏的数据包会自动重传
- **有序**：自动重排数据，保证顺序
- **拥塞控制**：调节发送速度避免丢包
- **速度**：比 UDP 慢

**类比：电话通话**
- 先建立连接
- 通话期间一直保持连接
- 有序通信

---

### UDP（用户数据报协议）
- **不可靠**：不保证交付
- **无序**：数据按到达顺序接收
- **无拥塞控制**
- **速度**：比 TCP 快

**类比：电子邮件**
- 消息不一定按发送顺序到达
- 发送方与接收方无持久联系
- 不保证邮件一定送达

---

### 什么时候用 UDP
UDP **不适合**需要**完整、有序数据**的应用（如 FTP、HTTP），这类应用优先保证可靠性。

UDP 适合**优先追求速度**的场景：
- 音视频流媒体（少量丢包可接受）
- DNS 查询（第4讲）
- 可靠性测试（发送 UDP 包，看是否在指定时间返回）
- **组播**（下一讲）

---

### 实时网络
如果不需要 TCP 的全部服务，可以**先用 UDP，再在应用层添加所需功能**。

典型实时通信需求：
- 响应快（延迟≤400ms）
- 少量丢包不影响理解对话
- 需要丢包/超时处理策略

常见应用：
- **VoIP**：IP 语音通话
- **RTP**：实时传输协议

---

### RTP（实时传输协议）
实时对话类应用的开放标准：
- 通常**运行在 UDP 之上**，在网络层看起来就是普通 UDP 包
- 12 字节 RTP 头部：包含序号、时间戳等
- 双方都用 RTP 更容易互通

私有协议示例（如 Skype）：
- 音视频数据包用 UDP
- 控制信令用 TCP
- 防火墙屏蔽 UDP 时，媒体包也会走 TCP（第17讲）

---

### Java 中的 UDP
实现分为两部分，都在 `java.net` 中：

#### DatagramPacket 类
- 负责把数据**装入/拆出**数据报
- **目标地址与端口属于数据报，不属于套接字**
- 源地址与端口自动添加

#### DatagramSocket 类
- 负责**发送/接收**数据报
- 只知道本地监听/发送端口

---

### 对客户端–服务器模型的影响
#### TCP
- 把网络连接当作**流**
- 永久双向连接
- 可假设数据能收到、按序到达

#### UDP
- **没有唯一持久连接**的概念
- 只处理**单个消息/包**
- 每台主机都必须监听数据
- DatagramSocket 不知道目标是谁
- 不需要一对一连接，可**一对多**（第15讲）

---

### DatagramPacket 类
按使用场景有两种构造方法：

#### 用于接收
```java
public DatagramPacket(byte[] buffer, int length)
```
- 协议通常限制最大长度（典型 8K）
- 缓冲区容量 ≥ 指定长度

#### 用于发送
```java
public DatagramPacket(byte[] data, int length, InetAddress destination, int port)
```
- 从数组加载数据
- 包含目标地址与端口

---

### 获取方法（Getters）
- `public byte[] getData()`
  返回数据缓冲区（字节数组），不是 I/O 流，需手动转字节
- `public int getLength()`
  要发送/已接收的数据长度
- `public InetAddress getAddress()`
  发送时是目标 IP，接收时是源 IP
- `public int getPort()`
  目标端口或源端口

---

### 设置方法（Setters）
与 Socket 不同，**创建后可修改字段**（因为无持久连接）。
适合复用数据包、提升性能、减少 GC。

- `public void setData(byte[] buffer)`
- `public void setLength(int length)`
- `public void setAddress(InetAddress address)`
- `public void setPort(int port)`

---

### DatagramSocket 类
客户端与服务器**使用同一个类**（没有 DatagramServerSocket），但构造方式不同。

#### 客户端
```java
public DatagramSocket() throws SocketException
```
系统**自动分配端口**。

#### 服务器
```java
public DatagramSocket(int port) throws SocketException
```
绑定到**指定端口**（告知客户端）。

两者都会绑定本地端口并监听入站数据。

---

### 常用方法（1）
- `public int getLocalPort()`
  返回套接字绑定的端口（主要对客户端有用）
- `public InetAddress getLocalAddress()`
  返回本地绑定地址（多 IP 硬件有用）
- `public void close()`
  关闭数据报套接字

---

### 常用方法（2）
- `public void send(DatagramPacket d) throws IOException`
  发送构造好的数据报
- `public void receive(DatagramPacket d) throws IOException`
  **阻塞**接收单个数据报，相当于 TCP 的 `accept()`
- `public void setSoTimeout(int timeout) throws SocketException`
  设置最大阻塞时间（毫秒），超时抛 `SocketTimeoutException`

---

### 连接管理便捷方法
- `public void connect(InetAddress host, int port)`
  仅与指定目标通信，发往其他目标会抛异常
  **不是 TCP 意义上的连接**，只是单向限定通信对象
- `public void disconnect()`
  解除限制，恢复可与任意方通信

**不是必须使用**，下例未用到。

---

### 示例1：回显客户端/服务器
代码见学习平台：
- UDPEchoClient.java
- UDPEchoServer.java

功能：
- 服务器端口由启动参数指定
- 客户端发送字符串包（目标地址、端口、字符串均为命令行参数）
- 服务器原样返回字符串
- 客户端处理**丢包**与**非法来源包**

---

### UDPEchoServer 代码片段
```java
// 绑定端口
DatagramSocket socket = new DatagramSocket(servPort);

// 复用同一个数据包
DatagramPacket packet = new DatagramPacket(new byte[ECHOMAX], ECHOMAX);

// 服务器循环
while (true) {
    socket.receive(packet); // 接收客户端包

    // 服务器打印客户端信息
    System.out.println("Handling client at " +
        packet.getAddress().getHostAddress() +
        " on port " + packet.getPort());

    // 回显给客户端
    socket.send(packet);
}
```

---

### UDPEchoClient 代码片段（1）
```java
DatagramSocket socket = new DatagramSocket();

// 设置接收超时
socket.setSoTimeout(TIMEOUT);

// 发送包
DatagramPacket sendPacket = new DatagramPacket(
    bytesToSend, bytesToSend.length, serverAddress, servPort);

// 接收包
DatagramPacket receivePacket = new DatagramPacket(
    new byte[bytesToSend.length], bytesToSend.length);
```

---

### UDPEchoClient 代码片段（2）
```java
do {
    socket.send(sendPacket); // 发送字符串
    try {
        socket.receive(receivePacket);

        // 检查是否来自未知地址
        if (!receivePacket.getAddress().equals(serverAddress))
            throw new IOException("Received from unknown source");

        receivedResponse = true;
    } catch (InterruptedIOException e) {
        System.out.println("Timed out ..."); // 超时重发
    }
} while (!receivedResponse);

// 输出结果
if (receivedResponse)
    System.out.println("Received: " + new String(receivePacket.getData()));
```

---

### 在真实网络中测试
- 在**同一主机（localhost）**或**局域网（LAN）**测试时，几乎不会丢包
- 在**广域网（WAN）/ 互联网**上，**丢包与损坏很常见**（第17讲说明原因）

不要误以为 UDP 比 TCP 简单！
一旦考虑丢包，程序逻辑通常会**复杂很多**。

---

### 总结与下次课程
本节课学习了 UDP：
- **快速但不可靠**的数据传输
- Java 中用 `DatagramPacket` + `DatagramSocket` 实现
- 一对一简单示例：UDP 回显服务器

下次课程：UDP 如何实现**一对多通信（组播）**。

要不要我帮你整理**TCP vs UDP 一页对比速记表**，方便考试复习？









## Multicasting

### 上一讲回顾
上一讲我们学习了传输层协议 **UDP（用户数据报协议）**：
- 不保证消息一定送达，也不保证数据包按序到达
- 不维持持久连接
- 比可靠的 TCP 更快
- Java 中用 **DatagramSocket** 和 **DatagramPacket** 实现
- 看过回显服务器示例
- 提到典型用途：DNS 查询（使用 53 号端口）

---

### 本节课内容
本节课讲解 UDP 的另一类用途：**向多个客户端发送相同数据**
- 通信模型（包括一对多）
- 定义**广播**与**组播**
- Java 如何用 **MulticastSocket**（java.net 包）实现组播
- 以一组组播客户端/服务器示例收尾

---

### 通信模型
到目前为止我们只讲了**一对一通信**：
- 也叫**点对点**或**单播（unicast）**，记为 1:1
- TCP 中 Socket 天然就是这种模型：套接字按地址+端口绑定到两端
- UDP 中 DatagramPacket+DatagramSocket 也是这种模型：数据包只发往一个地址+端口

两种情况下，数据包经过哪些中间路由器都**不指定**。

---

### 一对多通信
我们之前的多线程/非阻塞 I/O 服务器已经能处理多个客户端（可用 TCP 或 UDP）。

但如果要**把同一条消息发给大量客户端**（直播、视频会议等）：
- 每个客户端都要单独发一次
- 规模一大就**效率极低、无法扩展**

---

### 一对多通信的类型
#### 广播（Broadcasting）
- 把消息发给**同一子网内所有主机**
- 典型场景：设备刚入网获取 IP（DHCP 协议）
- IPv4 保留地址：**255.255.255.255**（本地广播，路由器不转发）
- IPv6 不支持广播，改用组播“all hosts”

#### 组播（Multicasting）
- 把消息发给**一组指定主机**
- 服务器只发**一份**到网络，由路由器复制转发给组内客户端
- 需要路由器额外支持

---

### 组播（Multicast）核心特点
- 服务器只发**一份数据**，网络自动复制分发给多个客户端
- 服务器到边缘路由器的链路上**不易拥塞**
- 每个客户端只收到一份副本
- 客户端只需改用 **MulticastSocket** 即可

---

### 组播架构
典型模式：
- 服务器持续发送数据流（一直在线）
- 客户端随时加入、接收、离开
- 适合：**直播、实时推送**等场景
- 不适合：点播（每个客户端需要不同流）

---

### 用 TCP 还是 UDP？
- **TCP**：需要为每个客户端维持连接、逐一确认、处理重传，**无法实现大规模组播**
- **UDP**：只需路由器支持单包多路径转发，错误处理交给应用层，**适合组播**

Java 组播**基于 UDP** 实现。

---

### 组播地址
一组专门用于组播的 IP 地址：
- **IPv4**：D 类地址，范围 **224.0.0.0 ~ 239.255.255.255**
- **IPv6**：前缀 **ff00::/8**

每个地址代表一个**组播组**：
- 服务器发往该地址
- 客户端监听该地址（无需建立连接）

---

### 路由与作用范围（TTL）
#### 路由
组播依赖路由器处理 D 类地址，路由逻辑更复杂，但**对应用层透明**。
服务器甚至可以用普通 DatagramSocket，只需把目标地址设为组播地址即可；
但**客户端必须用 MulticastSocket 加入组**。

#### 作用范围（TTL）
数据包有个字段叫 **TTL（Time To Live）**，控制“能传多远”：
- TTL=0：仅本机
- TTL=1：局域网/学院
- TTL=48：全国范围
- TTL=225：全球范围（近似）

---

### MulticastSocket 类
Java 组播的核心类：
- 位于 **java.net**
- **继承自 DatagramSocket**
- 保留 UDP 模型，增加**加入/离开组播组**的能力
- 使用：组播 IP + 任意标准 UDP 端口

---

### 服务器常用方法
- `public MulticastSocket() throws SocketException`
  创建组播套接字（地址/端口在数据包里指定）
- `public void setTimeToLive(int ttl)`
  设置所有发包的 TTL（默认 1，仅局域网）
- `public void send(DatagramPacket p)`
  发送数据包（继承自 DatagramSocket）

---

### 客户端常用方法
- `public MulticastSocket(int port) throws SocketException`
  绑定到指定端口
- `public void joinGroup(InetAddress address)`
  **加入组播组**（可加多个组）
- `public void leaveGroup(InetAddress address)`
  **离开组播组**
- `public void receive(DatagramPacket p)`
  接收数据包（继承自 DatagramSocket）

---

### 示例：组播客户端/服务器
代码平台：NumberServer.java、NumberClient.java
- 服务器端口：4446
- 组播地址：228.3.4.5（IPv4 组播段）
- 服务器不断发送整数流
- 客户端加入组，接收 5 个整数后关闭

---

### 服务器代码片段（1）
```java
// 构造方法：指定数据包的目标地址与端口，不是套接字
public NumberServer(String host, int port) {
    try {
        mcGroup = InetAddress.getByName(host); // 组播IP
    } catch (UnknownHostException ex) { ... }

    mcPort = port;

    try {
        socket = new MulticastSocket(); // 端口运行时指定
        socket.setTimeToLive(ttl);      // 设置TTL
    } catch (IOException ex) { ... }
}
```

---

### 服务器代码片段（2）
```java
while (true) { // 无限循环
    // 每2秒发送一个递增数字
    byte[] data = String.valueOf(counter).getBytes();

    DatagramPacket dp = new DatagramPacket(
        data, data.length, mcGroup, mcPort);

    try {
        socket.send(dp);
        System.out.println("Sent message");
    } catch (IOException ex) { ... }

    try {
        Thread.sleep(2000); // 暂停2秒
    } catch (InterruptedException ex) { ... }

    counter++;
}
```

---

### 客户端代码片段（1）
```java
public NumberClient(String host, int port) {
    try {
        mcAddr = InetAddress.getByName(host);
    } catch (UnknownHostException ex) { ... }

    try {
        mcGroup = new InetSocketAddress(mcAddr, mcPort);
        netInt = NetworkInterface.getByName("bge0");
        socket = new MulticastSocket(mcPort);
        socket.setSoTimeout(timeout); // UDP必须设超时
        socket.joinGroup(mcGroup);    // 加入组
    } catch (IOException ex) { ... }
}
```

---

### 客户端代码片段（2）
```java
public void runClient() {
    int num = 0;
    // 只收5个包
    while (num < 5) {
        byte[] data = new byte[256];
        DatagramPacket p = new DatagramPacket(data, data.length);

        try {
            socket.receive(p); // 阻塞等待
            System.out.println(new String(p.getData()));
        } catch (IOException ex) { ... }

        num++;
    }
    socket.leaveGroup(mcGroup); // 优雅离开组
    socket.close();
}
```

---

### 总结与下次课程
本节课学习了**一对多通信**，重点是**组播**：
- 向多主机同时发送相同数据的**高效方式**
- Java 用 **MulticastSocket** 实现
- 目前运营商支持仍有限

这是**应用层与 Java 网络编程的最后一讲**。
接下来 4 讲，我们进入**协议栈下层**（网络层、链路层等）的学习。

要不要我帮你整理**广播/单播/组播一页速记对比**，方便复习？





## Transport layer（重要）
大卫·海德
利兹大学
### 往期课程回顾

在简要介绍了端口、DNS 和 IP 地址后，我们主要聚焦于**应用层**。
- Java 网络应用开发
- 可使用 **TCP**（Socket/ServerSocket）或 **UDP**（DatagramPacket/DatagramSocket）
- 只需假设传输层服务按协议正常工作，无需了解下层（网络层、链路层、物理层）原理

---

### 本节课内容
本节课是**下层核心内容**4讲中的第1讲，有助于理解网络应用的性能。
本节课聚焦**传输层**：
- UDP 与 TCP 首部结构
- 在不可靠信道上实现**可靠数据传输**的方法
- TCP 的连接管理与拥塞控制

---

### 传输层服务
- 为不同主机上运行的应用提供**逻辑通信**
- 传输协议运行在**端系统/主机**内
- 控制**进程间**的数据传输
- 主机间的数据传输由下层负责

---

### UDP：用户数据报协议
- **尽力而为服务**：UDP 报文段可能失序、丢失
- **无连接**：发送方与接收方无握手过程
- 每个 UDP 报文段独立处理

### 为什么需要 UDP？
- 无需建立连接，**无连接建立延迟**
- 报文段首部**更小**
- **无拥塞控制**，可按需要全速发送
  （部分网络会因此屏蔽 UDP，仅放行 DNS）

---

### UDP 报文段结构
常用于**丢包可容忍、对速率敏感**的流媒体应用，可在应用层自行实现可靠性。
使用场景：DNS、SNMP（简单网络管理协议）。

**32位格式**
- 源端口号 | 目的端口号
- 长度（UDP 报文总字节数，含首部）
- 校验和
- 应用数据（消息）

---

### TCP：传输控制协议
- **点对点**：一个发送方，一个接收方
- **可靠**：保证数据完整有序
- 有发送缓冲区与接收缓冲区
- **流水线**：可连续发送多个包，不必等待前一个确认
- **全双工**：同一连接双向传输
- **面向连接**：传输前必须**三次握手**
- **流量控制**：发送方不会压垮接收方

---

### TCP 报文段结构
**32位格式**
- 源端口号 | 目的端口号
- 序号（sequence number）
- 确认号（acknowledgement number）
- 首部长度 | 标志位（URG、ACK、PSH、RST、SYN、FIN）
- 接收窗口（rwnd，流量控制）
- 校验和
- 紧急指针
- 选项（变长）
- 应用数据（变长）

**关键标志位**
- ACK：确认号有效
- SYN：连接建立
- FIN：连接关闭
- RST：重置连接

---

### TCP 流量控制
目标：发送方发送速度**不会超出接收方缓冲区容量**。
- 接收方：在 TCP 首部中告知发送方**可用缓冲区大小（RcvWindow）**
- 发送方：保证已发送未确认的数据量 < 最新接收窗口

---

### RDT：可靠数据传输
- `rdt_send()`：上层调用，发送数据
- `udt_send()`：传输层调用，通过不可靠信道发包
- `rdt_rcv()`：信道到达时触发
- `deliver_data()`：交付给上层应用

---

### 不可靠信道上的可靠传输
用**有限状态机（FSM）**描述可靠传输原理，发送方与接收方各一个 FSM。

#### 最简单情况：理想可靠信道
- 发送方：上层调用 → 打包 → 发送
- 接收方：收到包 → 解包 → 上交应用

#### 信道存在比特错误
用**校验和**检测错误，无法纠错。
- 接收方正确接收 → 回 **ACK（确认）**
- 接收方检测到错误 → 回 **NAK（否认）**
- 发送方收到 NAK/错误确认 → **重传**

#### 致命问题：确认包本身也可能出错
会导致**重复包**。
解决方法：给数据包加**序号**，TCP 正是这么做的。

---

### 带 0/1 序号的发送方 FSM
只用 **0、1 两个序号**（停等协议）即可避免重复。
- 发送序号 0 → 等待 ACK0
- 收到 ACK0 → 切换到等待发送 1
- 出错/NAK → 重传当前包

#### 接收方 FSM
- 等待序号 0 → 收到正确 0 → 交付数据 → 回 ACK0 → 切换等待 1
- 出错 → 回 NAK
- 收到重复序号 → 直接回 ACK，不上交应用

> 实际要提升性能需要**流水线**，即一次发多个包，这就需要更多序号。
> TCP 自动处理所有这些问题（丢包、错包、重复、失序）。

---

### 拥塞控制原理（重要）
- 多个输入流争抢同一个输出端口 → 队列堆积
- 缓冲区溢出 → **丢包**
- 处理器性能不足也会导致拥塞

拥塞控制 ≠ 流量控制：
- 流量控制：端到端，避免发太快压垮接收方
- 拥塞控制：避免压垮**网络（路由器）**

---

### 拥塞控制两种方式
1. **端到端拥塞控制**
   网络不提供显式反馈，主机通过**丢包、延迟**判断拥塞。
   **TCP 使用这种方式**。

2. **网络辅助拥塞控制**
   路由器直接反馈拥塞信号或发送速率。

---

### TCP 拥塞控制
核心思想：**探测可用带宽**
- 维护拥塞窗口 **CongWin**
- 无丢包时增大窗口
- 丢包时减小窗口

两个阶段：
- **慢启动**
- **拥塞避免**

由阈值（ssthresh）决定切换。

#### TCP 慢启动
- 初始 CongWin = 1 MSS
- 每收到一个 ACK → CongWin += 1
- **指数增长**
- 直到丢包 或 超过阈值

#### TCP 拥塞避免
- 进入线性增长：每轮 RTT 窗口 +1
- 发生丢包：
  - 阈值 = 当前 CongWin / 2
  - CongWin 重置为 1
  - 回到慢启动

---

### 总结与下次课程
本节课覆盖了**应用层正下方的传输层**：
- TCP、UDP 提供的服务与首部格式
- 可靠数据传输原理
- TCP 流量控制与拥塞控制

接下来两讲，我们学习更下一层：**网络层**。

要不要我帮你整理**TCP/UDP 头部+拥塞控制一页考试背诵版**？







## Network Layer

### 上一讲回顾
上一讲我们学习了位于**端系统/主机**中的**传输层**，以及它的两个核心协议：
- **TCP（传输控制协议）**：可靠，保证无差错、无丢包、无失序，支持连接管理与拥塞控制。
- **UDP（用户数据报协议）**：不可靠、无连接，通常比 TCP 更快，头部更短小。

---

### 本节课内容
本讲是应用层以下4讲中的**第2讲**，我们开始学习**网络层**：
- IP 地址所在的层次，也叫 **IP 层/互联网层**
- 负责数据包在**多段中间路径**上的路由选择
- 数据包在路由器中如何被转发
- **通用转发**，以及由此产生的**软件定义网络（SDN）**

---

### 无类别域间路由（CIDR）
回顾第5讲：现在的 IP 地址遵循 **CIDR** 规范：
- 地址中的**子网部分长度可以任意**
- IPv4 格式：`a.b.c.d/x`，x 表示子网部分的比特数
- IPv6 类似

示例：`200.23.16.0/23`

---

### IP 地址从何而来？
#### 主机如何获取 IP 地址？
- 手动配置：管理员写入系统文件
- 更常用：**DHCP（动态主机配置协议）**
  即插即用，从服务器**动态获取地址**。

#### 网络如何获取子网段？
从 **ISP（互联网服务提供商）** 分配地址空间。

---

### ICMP：互联网控制报文协议
用于**主机与路由器**之间传递网络层信息：
- 错误报告（主机不可达）
- 回显请求/应答（ping）

ICMP 消息**封装在 IP 数据报**中传输，包含：类型、代码、出错 IP 数据报的前8字节。

#### 常用类型码
- 0 0：回显应答（ping 应答）
- 3 0～3 7：目的网络/主机/协议/端口不可达等
- 8 0：回显请求（ping 请求）
- 11 0：TTL 超时
- 12 0：IP 头部错误

---

### traceroute 与 ICMP
工作原理：
1. 源主机向目标发送一组 UDP 报文
2. 第一个 TTL=1，第二个 TTL=2，依此类推
3. 第 n 个数据报到达第 n 个路由器时，路由器丢弃并返回 **ICMP 11/0（TTL 超时）**
4. 源计算**往返时间 RTT**，测3次取统计值
5. 最终 UDP 到达目标，因端口不存在返回 **ICMP 3/3（端口不可达）**，探测停止

---

### IPv6
#### 设计动机
- 解决 IPv4 **32位地址耗尽**问题
- 头部更简洁，加快路由器处理
- 内置**服务质量（QoS）**

#### IPv6 数据报格式
- 固定 **40字节头部**，无 IPv4 式可选字段
- 路由器**不允许分片**，分片过大直接返回错误（ICMPv6 类型2）

---

### IPv4 头部
- 版本、头部长度、服务类型
- 数据报总长度、标识、标志、片偏移
- TTL、协议、头部校验和
- 32位源IP、32位目的IP
- 可选字段 + 数据

---

### IPv6 头部
- 版本、优先级、流标签
- 有效载荷长度、下一个头部、跳数限制
- **128位源地址**
- **128位目的地址**
- 数据

关键字段：
- **优先级**：区分数据报优先级
- **流标签**：标识同一“流”的包
- **下一个头部**：指示上层协议（TCP/UDP/选项）

---

### IPv4 到 IPv6 的其他变化
- **校验和**：完全移除，降低每跳处理开销（传输层与链路层仍会校验）
- **选项**：保留，但移到头部外部，由“下一个头部”指示
- **ICMPv6**：新增“包过大”等类型，支持组播管理

---

### IPv4 向 IPv6 过渡
无法全网一次性切换，因此 IPv4 与 IPv6 **必须长期共存**。
核心方案：**隧道（Tunnelling）**
- IPv6 报文作为**载荷**封装在 IPv4 数据报中，在 IPv4 路由器间传输

---

### 路由器
路由器完成两大功能：
1. **运行路由算法**，计算高效路径（下一讲讲解）
2. **转发数据报**：根据转发表从入端口送到出端口

理想路由器没有应用层/传输层，但现实中常会用到，**打破分层模型**。

---

### 路由器架构
- **路由处理器**：计算转发表，控制平面（软件）
- **高速交换结构**：硬件转发数据
- **输入端口 / 输出端口**：物理层、链路层处理

---

### 输入端口功能
1. 线路端接：物理层接收比特
2. 链路层协议处理（如以太网）
3. **查表转发**：查转发表确定出端口
4. 排队：处理速度跟不上线路速度时缓存

---

### 交换结构
将数据包从输入缓冲区传到对应输出缓冲区，三种方式：
1. **内存**：早期，CPU 控制，慢
2. **共享总线**：较快，受总线带宽限制
3. **交叉开关（Crossbar）**：最快，无总线争抢

---

### 输出端口功能
- 缓存：交换结构可能比发送快
- 缓存溢出 → **丢包**
- 可调度优先级（网络中立性相关）

---

### 转发表
- 按 **目的IP前缀（a.b.c.d/x）** 映射输出端口
- 多匹配时采用**最长前缀匹配**（最精确范围）

---

### 通用转发
早期路由器只看**目的IP**转发。
通用转发支持：
- **匹配–动作**模型
- 可匹配：端口、IP、协议、传输/网络/链路层头部任意字段
- 动作：转发、丢弃（防火墙）等

传统 IP 转发只是通用转发的**特例**。

---

### SDN：软件定义网络
通用转发推动了 **SDN** 发展：
- 基于头部任意信息的**流转发**
- **控制与数据平面分离**
- 软件可独立部署、模块化编程
- 标准：**OpenFlow**

---

### 总结与下次课程
本节课开始学习**网络层**：
- ICMP、IPv4、IPv6
- 隧道技术实现 IPv4/IPv6 互通
- 通用转发与 SDN

下一讲：**转发表是如何构建的**（路由算法）。

要不要我帮你把 **L17 也配上标准英文标题**，和之前15、16统一成套？



## Routing Algorithms

### 上一讲回顾
上一讲我们学习了路由器如何使用**转发表**转发数据包：
- 传统方式仅使用**目的IP地址**
- 现代方式支持更多字段与动作，即**匹配–动作模式**
- 称为**通用转发**，在**软件定义网络（SDN）**中实现
- 还介绍了 **ICMP**、**IPv6** 以及通过**隧道**实现 IPv4/IPv6 共存

---

### 本节课内容
本节课是**网络层**的第二讲，重点讲解数据包的**路由选择算法**：
- **Dijkstra 算法**（链路状态算法）
- **RIP**（距离向量算法）
- **OSPF** 及其分层版本（子网内部路由）
- **BGP**（子网间路由的事实标准）

本讲只关注**目的IP地址**，并以**最优路径**为目标。

---

### 路由：图抽象表示
用图 \(G=(N, E)\) 表示网络：
- \(N\)（结点）：路由器集合
- \(E\)（边）：链路集合

链路代价：\(c(x, y)\) 表示链路 \(x→y\) 的开销。
路径总代价 = 所有链路代价之和。
**路由算法**：找到**最小代价路径**。

---

### 路由算法分类
#### 按信息范围
1. **全局式**
   所有路由器知道完整拓扑与链路代价 → **链路状态算法**（如 Dijkstra）
2. **分布式**
   仅知道直连邻居，与邻居迭代交换信息 → **距离向量算法**（如 RIP）

#### 按更新方式
- **静态**：路由变化很慢
- **动态**：随链路代价/拓扑自动更新

---

### Dijkstra 链路状态路由算法
前提：全网拓扑与代价**已知**（通过链路状态广播实现）。
功能：计算**从源结点到所有其他结点的最短路径**，生成转发表。

符号说明：
- \(c(x,y)\)：直接链路代价，无连接为 ∞
- \(D(v)\)：当前源到 v 的路径代价
- \(p(v)\)：路径上的前驱结点
- \(N'\)：已确定最短路径的结点集合

#### 算法步骤
1. 初始化：\(N' = \{源点\}\)，邻居赋直接代价，其余为 ∞
2. 循环：
   - 选 \(N'\) 外代价最小的结点 \(w\)，加入 \(N'\)
   - 更新 \(w\) 的邻居代价：\(D(v) = min(D(v), D(w)+c(w,v))\)
3. 直到所有结点都在 \(N'\) 中

---

### Dijkstra 示例结果
从结点 u 出发的最短路径树与转发表：
| 目的结点 | 出链路 |
| -------- | ------ |
| v        | (u,v)  |
| x        | (u,x)  |
| y        | (u,x)  |
| w        | (u,x)  |
| z        | (u,x)  |

---

### RIP：路由信息协议
- **距离向量算法**，分布式、仅知本地信息
- 1982 年随 BSD UNIX 发布
- **度量标准：跳数**（最大 15 跳，16 表示不可达）

#### RIP 通告
- 邻居间**每 30 秒**交换距离向量（通告）
- 每个通告最多包含 25 个子网路由
- 报文比链路状态小，但**收敛慢、无保证**

#### 链路失效
- 180 秒未收到通告 → 认为邻居/链路失效
- 失效路由作废，新通告扩散全网

#### 实现特点
- 由应用层守护进程 **route-d** 管理
- 基于 **UDP** 发送，**打破分层架构**

---

### OSPF：开放式最短路径优先
- **Open**：协议公开
- 属于**链路状态算法**，运行在**自治系统（AS）内部**
- 每个结点持有完整拓扑图，用 **Dijkstra 算法**计算路由
- 通告直接封装在 **IP 报文**中，不使用 TCP/UDP
- 管理员控制力强

#### 分层 OSPF
大规模网络采用**两层结构**：区域 + 骨干
- 区域内：详细链路状态信息
- 区域间：只发布路由汇总
- 三类路由：区域内路由、区域边界路由、骨干路由、边界路由（连接其他AS）

---

### BGP：边界网关协议
**互联网 AS 间路由的事实标准**。
功能：
1. 从邻居AS获取子网可达性信息
2. 在AS内传播可达信息
3. 基于策略与代价选择最优路由
4. 向全网宣告子网存在

#### BGP 基础
- 路由器间通过**半永久 TCP 连接**交换信息（BGP 会话）
- **eBGP**：跨AS会话
- **iBGP**：AS内会话

#### 路由选择规则
1. **本地优先级**最高优先（管理员策略）
2. **AS-PATH 最短**优先
3. 下一跳路由器**代价最小**优先
4. 其他规则

---

### 总结与下次课程
本节课学习了互联网常用路由算法：
- **OSPF**：AS 内路由，基于 Dijkstra
- **BGP**：AS 间路由，互联网核心

网络层内容到此结束。
下一讲学习最后两层：**链路层**与**物理层（简要）**。

要不要我把 **L17、L18 也配上标准英文标题**，和你之前要的 15、16 完全统一成套？



## Link Layer

### 往期课程回顾
在过去三讲中，我们学习了**应用层以下的各层**：
- **传输层**：TCP、UDP、连接管理与拥塞控制
- **网络层（IP层/互联网层）**：路由器如何转发数据包、各类路由算法

---

### 本节课内容
本节课学习**最底层的两层**：
1. **数据链路层（链路层）**
   - 以太网协议与MAC地址
   - 多设备如何共享同一信道
2. **物理层**（简要介绍）

这是本模块**最后一节新知识课**。

---

### 链路层：术语
- **结点（Node）**：主机或路由器
- **链路（Link）**：连接相邻结点的通信信道（有线/无线）
- **LAN**：局域网
- **帧（Frame）**：链路层的数据包单元
- 链路层负责：在**物理相邻**的两个结点之间传输数据

---

### 链路层类比
数据包会在不同链路上使用不同的链路协议传输（以太网、帧中继、WiFi等），每种协议提供的服务不同。

**旅行类比**：从利兹到洛桑
- 出租车：利兹→机场（对应第一段链路）
- 飞机：机场→日内瓦（对应中间链路）
- 火车：日内瓦→洛桑（对应最后一段链路）
- **旅行者 = 数据包/帧**
- **运输段 = 通信链路**
- **运输方式 = 链路层协议**
- **旅行社 = 路由算法**

---

### 链路层提供的服务（1）
1. **成帧与链路访问**
   - 将网络层数据报封装成**帧**，加头部与尾部
   - 共享信道需做**信道访问控制**
   - 使用**MAC地址**（与IP地址不同）
2. **相邻结点间可靠交付**（可选）
   - 实现类似TCP的机制
   - **有线链路很少用**（错误率极低）
   - **无线链路常用**（错误率高）

### 链路层提供的服务（2）
3. **流量控制**：避免相邻收发结点速率不匹配
4. **错误检测**：信号衰减/噪声导致错误，接收方检测并要求重传或丢弃
5. **纠错**：无需重传，直接纠正比特错误
6. **半双工/全双工**
   - 半双工：两端可发，但**不能同时发**
   - 全双工：可同时收发

---

### 链路层在哪里实现？
- 实现在**每个主机**中
- 通过**网卡（NIC，网络接口控制器）**或芯片实现
- 集成硬件、软件、固件
- 连接到主机系统总线（如PCI）

---

### 多访问链路（共享链路）
#### 两种链路类型
1. **点对点**
   拨号上网、交换机与主机之间的链路
2. **广播（共享）**
   以太网、WiFi、卫星、共享射频信道

多结点同时发送会产生**冲突（Collision）**，必须用协议协调。

---

### 多访问协议
分布式算法，规定结点**何时可以发送**，避免冲突、高效共享信道。

#### 三大类
1. **信道划分**
   把信道按时间/频率/编码分片，独占使用
2. **随机访问**
   随机发送，冲突后重试
3. **轮流访问**
   结点按顺序发送，数据多的可用更久

---

### TDMA：时分多址
- 给每个结点分配**固定时长时隙**
- 问题：空闲时隙浪费带宽、利用率低

### FDMA：频分多址
- 把信道划分为**不同频段**，每个结点独占一个频段
- 问题：每个结点带宽有限

---

### 随机访问协议：时隙ALOHA
#### 核心思想
- 有数据就立即在时隙开始发送
- 检测到冲突 → **随机等待后重传**

#### 效率
- 大量结点时，最大效率约 **1/e ≈ 37%**
- 单结点发送时可占满带宽

---

### MAC 地址
每个网络接口必须有全球唯一 **MAC地址（介质访问控制地址）**：
- **48位**，烧录在网卡ROM中
- 格式例：`1A-2F-BB-76-09-AD`
- IEEE统一管理分配
- **扁平结构**（无层级），可移动设备

#### 与IP地址对比
- **MAC**：像身份证号，**设备自带、不变**
- **IP**：像通讯地址，**随网络位置变化**

---

### ARP：地址解析协议
**已知IP，如何获取MAC？**
- 每个IP结点（主机/路由器）有**ARP表**
- 动态缓存：**IP ↔ MAC** 映射
- 广播查询，单播应答

---

### 以太网帧结构
- **前导码**：同步时钟
- **目的MAC / 源MAC**
- **类型**：标识上层协议（通常是IP）
- **数据载荷**
- **CRC**：循环冗余校验，错误检测

**以太网特性**：无连接、不可靠。

---

### 以太网标准
- 统一MAC协议与帧格式
- 不同速率：2Mbps / 10Mbps / 100Mbps / 1Gbps / 10Gbps
- 不同物理介质：双绞线、光纤

---

### 物理层
网络模型的**最底层**，负责**逐比特**传输。
- 介质：双绞线、光纤、无线
- 无线：高错误率、多访问特性
- 常见协议：
  - **802.11（WiFi）**
  - **Bluetooth**
  - **Zigbee（物联网）**

---

### 总结与下次课程
本节课学习了**最底层两层**：
- **链路层**：相邻结点传输、MAC地址、共享信道协议、以太网
- **物理层**：比特级传输、介质与无线标准

下一课是**最后一课**，对整门课程进行全面总结。

---

我也直接给你配好**标准统一英文标题**：
**Lecture 19: Link Layer, MAC Addresses, Ethernet & Physical Layer**

需要我把 **L8、13、14、15、16、17、18、19 整套标题+翻译目录**一次性整理好给你吗？



## Review

下面是 **Lecture 20 课件逐页中文翻译**。这是 COMP2221 Networks 的复习课，主要用于考前总结，包括考试形式、课程整体结构和各层协议回顾。

---

### 今天的课程

今天的课程目的是对本课程进行总览和复习，为考试做准备：

* 考试形式；
* 考试中会考什么；
* 总结课程内容；
* 最后留几分钟进行模块反馈。

---

### 第 3 页：TCP/IP 协议栈

**The TCP/IP protocol stack**

图中展示了 TCP/IP 五层协议栈在不同设备中的位置：

| 设备            | 包含的层                                                     |
| --------------- | ------------------------------------------------------------ |
| Host 主机       | Application 应用层、Transport 传输层、Network 网络层、Link 链路层、Physical 物理层 |
| Router 路由器   | Network 网络层、Link 链路层、Physical 物理层                 |
| Switch 交换机   | Link 链路层、Physical 物理层                                 |
| Repeater 中继器 | Physical 物理层                                              |

也就是说：

主机需要完整五层，因为它要运行应用程序。
路由器主要处理 IP 层，也就是网络层。
交换机主要处理链路层，例如 MAC 地址。
中继器只负责物理层信号转发。

---

### 第 4 页：课程整体结构

在总体介绍之后，课程按照 **5 层 TCP/IP 协议栈** 从上到下进行讲解：

**Application layer 应用层**
负责单个进程之间的通信，主要对应 Lectures 5–15。

**Transport layer 传输层**
提供端口，用来控制进程之间的数据传输，对应 Lectures 3 和 16。

**Network layer 网络层**
处理主机和路由器的 IP 地址，对应 Lectures 4、5、17、18。

**Link layer 链路层**
负责相邻节点之间的数据通信，对应 Lecture 19。

**Physical layer 物理层**
负责发送单个比特，在 Lecture 19 中简要提到。

此外，课程也介绍了 **7 层 OSI 模型**，对应 Lecture 2。

---

### 第 5 页：术语和地址

数据包在不同层通常有不同的名称。除了物理层和应用层之外，其他层通常都有某种形式的“地址”。源地址和目标地址会出现在这些层的 header 中。

| 层                 | 数据包常用名称  | 地址或类似概念 |
| ------------------ | --------------- | -------------- |
| Application 应用层 | Message 消息    | 无             |
| Transport 传输层   | Segment 段      | Port 端口      |
| Network 网络层     | Datagram 数据报 | IP 地址        |
| Link 链路层        | Frame 帧        | MAC 地址       |
| Physical 物理层    | 无              | 无             |

补充说明：

1. UDP 的全称是 User Datagram Protocol，虽然名字里有 Datagram，但它属于传输层。
2. IP 地址可以通过 DNS，也就是 Domain Name System，被转换成主机名。

---

### 第 6 页：为什么需要缓冲 Buffering

传输层、网络层和链路层这三层都会给消息添加 header，有时也会添加 trailer 或 footer。

header 的大小取决于具体协议，例如：

* TCP 或 UDP；
* IPv4 或 IPv6；
* Ethernet 或 IEEE 系列协议。

每一层的 header 大小可能是 **20–40 bytes**。

这意味着，最终通过物理层发送出去的消息，可能比应用层原始数据大很多。

例如，telnet 可能只发送单个字符。

这说明了：在应用层进行 buffering 很重要，因为它可以提高 I/O 性能。

在 Java 中，可以很方便地使用 streams 实现 buffering，这部分对应 Lecture 6。

---

### 第 7 页：性能 Performance

还有其他方法可以提高性能，尤其是服务器性能：

**1. 使用非阻塞 I/O**

对应 Lecture 12。

非阻塞 I/O 允许一个服务器线程同时处理多个客户端。

但是它不容易实现。

**2. 使用多线程**

对应 Lectures 9–11。

每个客户端处理器都有自己的线程。

这种方式比较容易实现，尤其是配合 Executor 的线程池使用。

它可以很好地利用现代多核架构。

这种策略不仅适用于 I/O，也适用于大多数问题。

---

### 第 8 页：UDP

课程中也学习了 UDP，对应 Lecture 14。

UDP 的特点：

**Connectionless 无连接**

不像 TCP，TCP 会维护连接直到关闭。

**Unreliable 不可靠**

数据包可能丢失，也可能不按照发送顺序到达。

这也和 TCP 不一样。

UDP 可以考虑用于流媒体应用。

UDP 也可以用于 **multicasting 多播**，对应 Lecture 15。

多播的意思是：

同一份数据发送给多个接收者，同时不会造成严重拥塞。

不过 UDP 多播并不广泛使用，虽然 IPv6 支持它。

---

### 第 9 页：安全 Security

课程也简单接触了网络安全，这是一个越来越重要的问题。

Lecture 13 中学习了 SSLSockets。

还学习了：

* 加密 encryption 的基础；
* 认证 authentication 的基础；
* 对称密钥算法 symmetric key algorithms，使用私钥；
* 非对称密钥算法 asymmetric key algorithms，使用私钥和公钥。

这个重要主题会在 Level 3 模块 **COMP3911 Secure Computing** 中完整讲解。

---

### 第 10 页：课程总结 1

**Lecture 1**：网络介绍，也包括课程管理信息。

**Lecture 2**：网络架构；5 层模型和 7 层模型。

**Lecture 3**：端口、UDP 和 TCP；低层协议的 headers。

**Lecture 4**：DNS，以及它如何把域名映射到 IP 地址。

**Lecture 5**：IP 地址、IPv4 和 IPv6；CIDR 和 NAT；Java 中的 InetAddress。

**Lecture 6**：Java I/O streams，包括 buffering 和 filters。

**Lecture 7**：Socket 类；构造 socket 涉及互联网访问和端口绑定。

**Lecture 8**：ServerSocket 类，以及实例如何监听端口。

---

### 第 11 页：课程总结 2

**Lecture 9**：并行和并发编程的总体概念。

**Lecture 10**：Java Thread 类；同步；thread-per-client 服务器。

**Lecture 11**：线程池服务器；Executor service。

**Lecture 12**：非阻塞 I/O；Buffer、Channel 和 Selector。

**Lecture 13**：网络安全：加密和认证；SSLSocket 类。

**Lecture 14**：UDP：DatagramPacket 和 DatagramSocket。

**Lecture 15**：一对多通信；使用 UDP 进行 multicasting；MultiSocket 类。

---

### 第 12 页：课程总结 3

**Lecture 16**：传输层：连接管理和拥塞控制；有限状态机；UDP 和 TCP headers。

**Lecture 17**：网络层：CIDR 的更多细节；tunnelling 隧道技术；路由器、交换结构和 generalized forwarding tables。

**Lecture 18**：路由算法：Dijkstra 算法、RIP 和 advertisements、分层 OSPF 和 BGP。

**Lecture 19**：链路层：MAC 地址；多路访问协议；一些 Ethernet 标准；物理层。

---

### 第 13 页：网络通信的完整过程

Kurose 和 Ross 统计过，当一个学生通过以太网线把笔记本连接到大学网络时，背后会发生多少步骤。

如果使用 Wi-Fi，过程也类似。

他们一共列出了 **24 个步骤**。

现在做一个总结很有用，因为它可以帮助我们看到：课程中学到的各层知识，如何组合起来完成一个日常操作。

---

### 第 14 页：1. 设备发现 Device discovery

连接之后，笔记本首先需要一个 IP 地址。

笔记本操作系统会把一个 **DHCP request** 放进 UDP segment 中。

然后 UDP segment 被放进 IP datagram 中。

再然后 IP datagram 被放进 link-layer frame 中，并在以太网上广播。

以太网交换机会把这个消息发送到所有 outgoing ports，包括路由器。

路由器会提取这个 DHCP request。

然后路由器返回一个 DHCP message。

这个 DHCP message 同样被封装在：

```text
UDP segment
→ IP datagram
→ link-layer frame
```

里面。

笔记本提取 DHCP message，得到：

* 自己的 IP 地址；
* 将要使用的 DNS server 地址。

补充：DHCP = Dynamic Host Configuration Protocol，动态主机配置协议，对应 Lecture 17。

---

### 第 15 页：2. 获取路由器的 MAC 地址

学生现在在浏览器中输入：

```text
www.google.com
```

浏览器需要使用 DNS 把这个域名转换成 IP 地址。

浏览器创建一个 DNS query，并把它放进 UDP segment 中，目标端口是 **53**。

然后它会被发送到已经配置好的 DNS server。

和之前一样，数据会被放进：

```text
IP datagram
→ link-layer frame
```

中。

但是此时笔记本还不知道路由器的 MAC 地址。

所以它会创建一个 **ARP query**，并把它放进 link-layer frame 中进行广播。

路由器会发送一个 ARP reply，仍然是在 link-layer frame 中，返回给笔记本操作系统。

补充：ARP = Address Resolution Protocol，地址解析协议，对应 Lecture 19。

---

### 第 16 页：3. 获取 IP 地址

现在笔记本可以通过路由器发送 DNS query 了。

路由器从 frame、datagram、segment 中提取出 query。

然后路由器使用自己的 forwarding table 查看应该把它发送到哪里。

接着，路由器再把数据放进：

```text
segment
→ datagram
→ frame
```

中，然后发送出去。

DNS query 会经过多个路由器到达 DNS server。

这些路由过程中可能涉及：

* RIP；
* OSPF；
* BGP。

这些内容对应 Lecture 18。

DNS server 检查自己的 cache。假设找到了对应记录，它会向笔记本发送 DNS reply。

这个 reply 同样经过：

```text
segment
→ datagram
→ frame
```

封装。

最后，笔记本操作系统提取消息，并得到：

```text
www.google.com
```

对应的 IP 地址。

---

### 第 17 页：4. 下载网页

Web 浏览器创建一个 TCP socket。

这个 socket 首先会和 web server 进行 handshake，也就是握手。

握手过程中的每一步都会使用：

* 浏览器的端口号；
* 服务器的端口号 80。

然后浏览器创建一个 HTTP GET request。

这个请求会通过一个或多个路由器转发给服务器。

服务器向笔记本返回 HTTP response message。

笔记本提取其中的信息，并显示网页。

当然，在浏览器和服务器之间发送的所有消息，都会被封装成：

```text
TCP segment
→ IP datagram
→ link-layer frame
```

---

### 第 18 页：最后

祝考试好运。

---

#### 这份课件的核心总结

这节课不是讲新知识，而是把整个 COMP2221 Networks 串起来：

从应用层的 HTTP、DNS、Socket，到传输层的 TCP/UDP，再到网络层的 IP、路由算法，最后到链路层的 MAC、ARP 和物理层传输。

最重要的理解是：

```text
应用层消息
→ 传输层 Segment
→ 网络层 Datagram
→ 链路层 Frame
→ 物理层 Bits
```

接收方再反过来逐层解封装：

```text
Bits
→ Frame
→ Datagram
→ Segment
→ 应用层 Message
```
