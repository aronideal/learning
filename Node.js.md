
[官方 latest-v6.x API](https://nodejs.org/docs/latest-v6.x/api)

## 1. 执行脚本

```javascript
node code.js
```

## 2. 功能点

#### 2.1. JSON 解析与格式化

```javascript
Javascript Object = JSON.parse(JSON String)

JSON String = JSON.stringify(Javascript Object)
```

## 3. 模块

#### 创建模块 test.js

```javascript
// 定义模块的函数
var func1 = function() {
    return "这是模块1";
};

module.exports = {
    func1 : func1
};
```

#### 使用模块

```javascript
var test = require("./test");

console.log(test.func1());
```

#### 3.1. 建立 HTTP 服务，文件名 testhttp.js

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

#### 3.2. 请求 HTTP 服务，文件名 testhttp_req.js

```javascript
const querystring = require("querystring");
const http = require('http');

const postData = querystring.stringify({
    'msg': 'Hello World!'
});

const options = {
    hostname: '10.0.6.40',
    port: 8089,
    method: 'POST', // GET or POST
    headers: {
        'Content-Type': 'application/x-www-form-urlencoded',
        'Content-Length': Buffer.byteLength(postData)
    }
};

const req = http.request(options, (res) => {
    const statusCode = res.statusCode;
    const statusMessage = res.statusMessage;
    const contentType = res.headers['Content-Type'];
    res.setEncoding('UTF-8');
    res.on('data', (chunk) => {
        if (200 === statusCode) {
            if (/^application\/json/.test(contentType)) {
                console.log(chunk);
            } else {
                console.log(`content-type '${contentType}' unsupported!`);
            }
        } else {
            console.log(`HTTP Error: ${statusCode}, ${statusMessage}!`);
        }
    });
});

req.write(postData);
req.end();
```

