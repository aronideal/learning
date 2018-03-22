
## 1. 执行脚本

```javascript
node code.js
```

## 2. 功能点

#### 2.1. JSON格式解析与格式化

```javascript
Javascript Object = JSON.parse(JSON String)

JSON String = JSON.stringify(Javascript Object)
```

## 3. 模块使用

#### 3.1 建立 http 服务，文件名 testhttp.js

```javascript
const http = require('http');

const hostname = '10.0.6.40';
const port = 8089;

const server = http.createServer((req, res) => {
    res.statusCode = 200;
    res.statusMessage = 'OK';
    // 设置响应内容类别
    res.setHeader('Content-Type', 'application/xml');
    // 写入内容
    res.end('<?xml version=\'1.0\' encoding=\'UTF-8\'?>\n<root><node1/><node2><node2-1 att=\'val\'/></node2></root>');
});

// 启动监听服务
server.listen(port, hostname, () => {
    console.log(`Server started! http://${hostname}:${port}`);
});
```

#### 3.2. 请求 http 服务，文件名 testhttp_send.js

```javascript
const http = require('http');


```

