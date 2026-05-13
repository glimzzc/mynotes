# Node.js

文章参考：

Node.js 是一个基于 Chrome V8 引擎 (Google Chrome 的内核) 的 JavaScript 运行时环境，它使得 JavaScript 不仅可以在浏览器中运行，还可以在服务器端运行。

Node.js 的主要特点包括：

1. **非阻塞 I/O**：Node.js 使用事件驱动和异步 I/O 模型，这使得它能够处理大量并发连接，并且性能高效。

    > **同步 I/O（阻塞模型）的情况：**
    >
    > 在传统的同步 I/O 模型中，当服务器接收到一个请求时，它会进行一些 I/O 操作，比如读取文件、访问数据库等。这些操作是**阻塞的**，即服务器在等待操作完成时无法处理其他请求。这样，**如果有大量请求到达**，服务器可能会被阻塞，导致延迟增加，吞吐量下降。

2. **单线程**：Node.js 采用单线程模型来处理所有的并发请求。通过事件循环（Event Loop）和回调函数，Node.js 能够在同一个线程上高效地管理多个任务。

3. **高性能**：Node.js 基于 Google 的 V8 引擎，这使得它能够执行 JavaScript 代码非常快速。

4. **模块化**：Node.js 提供了丰富的内置模块和包管理器 npm（Node Package Manager），开发者可以很容易地安装、共享和使用各种开源模块。

5. **广泛的应用场景**：Node.js 被广泛应用于构建高性能的 Web 应用程序、API 服务、实时聊天系统等。



很好，这一块是蓝桥杯 Web / Node 赛道的**高频考点** 👍
我给你整理一份**可直接复习 + 能上手写代码的 Node 三大核心模块资料（fs / path / http）**，结合你现在的水平（你已经写过服务器了），我会讲到**考试会考的点 + 常见坑 + 模板代码**。

------

# 🧠 一、三大核心模块总览

| 模块   | 作用       | 关键词   |
| ------ | ---------- | -------- |
| `fs`   | 文件操作   | 读写文件 |
| `path` | 路径处理   | 拼路径   |
| `http` | 创建服务器 | 接口     |

------

# 📂 二、fs 模块（文件系统）⭐必考

------

## 1️⃣ 同步读取（最基础）

```js
const fs = require('fs')

const data = fs.readFileSync('./test.txt', 'utf-8')
console.log(data)
```

📌 特点：

- 阻塞（考试常考区别）

------

## 2️⃣ 异步读取

```js
fs.readFile('./test.txt', 'utf-8', (err, data) => {
  if (err) return console.log(err)
  console.log(data)
})
```

------

## 3️⃣ Promise 写法（推荐）

```js
const fs = require('fs/promises')

async function run() {
  const data = await fs.readFile('./test.txt', 'utf-8')
  console.log(data)
}
run()
```

------

## 4️⃣ 写文件

```js
fs.writeFileSync('./a.txt', 'hello')
```

------

## 5️⃣ 追加文件

```js
fs.appendFileSync('./a.txt', '\nworld')
```

------

## 6️⃣ 判断文件是否存在

```js
fs.existsSync('./a.txt')
```

------

## 7️⃣ 删除文件

```js
fs.unlinkSync('./a.txt')
```

------

## ⚠️ fs 高频考点

### ❗ 必考 1：同步 vs 异步

| 类型  | 特点   |
| ----- | ------ |
| sync  | 阻塞   |
| async | 非阻塞 |

------

### ❗ 必考 2：编码问题

```js
fs.readFileSync('./a.txt') // 返回 Buffer
fs.readFileSync('./a.txt', 'utf-8') // 返回字符串
```

------

# 🛣️ 三、path 模块（路径处理）⭐必考

------

## 1️⃣ 拼接路径（最重要）

```js
const path = require('path')

const p = path.join(__dirname, 'index.html')
```

👉 永远用 `join`，不要自己拼 `'../'`

------

## 2️⃣ 获取文件名

```js
path.basename('/a/b/c.txt') // c.txt
```

------

## 3️⃣ 获取后缀

```js
path.extname('a.txt') // .txt
```

------

## 4️⃣ 获取目录

```js
path.dirname('/a/b/c.txt') // /a/b
```

------

## ⚠️ path 高频考点

### ❗ __dirname

```js
console.log(__dirname)
```

👉 当前文件所在目录

------

### ❗ 为什么不用字符串拼接？

```js
'../index.html' ❌
path.join(__dirname, '../index.html') ✅
```

👉 防止路径错误（跨平台）

------

# 🌐 四、http 模块（服务器）⭐⭐⭐核心

------

## 1️⃣ 创建服务器（必背模板）

```js
const http = require('http')

const server = http.createServer((req, res) => {
  res.end('hello')
})

server.listen(3000, () => {
  console.log('server running')
})
```

------

## 2️⃣ 获取请求信息

```js
req.url     // 路径
req.method  // GET / POST
```

------

## 3️⃣ 路由判断

```js
if (req.url === '/' && req.method === 'GET') {
  res.end('首页')
}
```

------

## 4️⃣ 返回 HTML

```js
res.setHeader('Content-Type', 'text/html;charset=utf-8')
res.end('<h1>hello</h1>')
```

------

## 5️⃣ 返回 JSON（你之前踩过坑）

```js
res.setHeader('Content-Type', 'application/json;charset=utf-8')

res.end(JSON.stringify([
  { name: '张三' }
]))
```

❗ 不能直接传数组（你之前报错就是这个）

------

## 6️⃣ 读取文件返回页面（必考）

```js
const fs = require('fs')
const path = require('path')

const html = fs.readFileSync(path.join(__dirname, 'index.html'))

res.setHeader('Content-Type', 'text/html;charset=utf-8')
res.end(html)
```

------

## 7️⃣ POST 请求（重点）

```js
let body = ''

req.on('data', chunk => {
  body += chunk
})

req.on('end', () => {
  console.log(body)
  res.end('ok')
})
```

------

## 8️⃣ 解析参数

```js
const url = require('url')

const obj = url.parse(req.url, true)

console.log(obj.query)
```

------

# ⚠️ http 高频坑（你已经踩过）

------

## ❌ 错误：res.end(数组)

```js
res.end([1,2,3]) ❌
```

------

## ✅ 正确：

```js
res.end(JSON.stringify([1,2,3]))
```

------

## ❌ 忘记设置响应头

```js
res.end('你好') ❌ 可能乱码
```

------

## ✅

```js
res.setHeader('Content-Type', 'text/plain;charset=utf-8')
```

------

# 🧩 五、三模块组合（考试最爱）

------

## 📌 场景：访问页面

```js
if (req.url === '/') {
  const html = fs.readFileSync(path.join(__dirname, 'index.html'))
  res.setHeader('Content-Type', 'text/html;charset=utf-8')
  res.end(html)
}
```

------

## 📌 场景：接口返回数据

```js
if (req.url === '/api') {
  const data = fs.readFileSync('./data.json', 'utf-8')
  res.setHeader('Content-Type', 'application/json')
  res.end(data)
}
```

------

# 🚀 六、考试常见题型

------

## 🧪 题型1：写一个服务器返回页面

👉 考：

- http
- fs
- path

------

## 🧪 题型2：实现接口

👉 考：

- GET / POST
- JSON

------

## 🧪 题型3：文件操作

👉 考：

- readFile
- writeFile

------

## 🧪 题型4：路径拼接

👉 考：

- path.join
- __dirname

------

# 🎯 七、终极模板（建议你背）

```js
const http = require('http')
const fs = require('fs')
const path = require('path')

const server = http.createServer((req, res) => {
  if (req.url === '/') {
    const html = fs.readFileSync(path.join(__dirname, 'index.html'))
    res.setHeader('Content-Type', 'text/html;charset=utf-8')
    res.end(html)
  }

  else if (req.url === '/api') {
    const data = fs.readFileSync(path.join(__dirname, 'data.json'))
    res.setHeader('Content-Type', 'application/json;charset=utf-8')
    res.end(data)
  }

  else {
    res.statusCode = 404
    res.end('Not Found')
  }
})

server.listen(3000)
```

------

# 🧠 最后给你一份记忆口诀

👉 Node 三大模块：

```
fs 读写文件
path 管路径
http 开服务
```

👉 核心组合：

```
http + fs + path = 网页服务器
```

------

# 💡 如果你想冲高分

我可以帮你做一套：

✅ 蓝桥杯风格真题（带评分点）
✅ 一题一练（从简单到难）
✅ 包含你之前做过的“接口 + 地图 + 验证码”结合题

直接模拟比赛环境训练 👍
