
## 建立 http 服务，文件名 testhttp.js

```javascript
const http = require('http');

const hostname = '10.0.6.40';
const port = 8089;

const server = http.createServer((req, res) => {
    res.statusCode = 200;
    res.statusMessage = 'OK';
    res.setEncoding('UTF-8');
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

## 执行脚本

    node testhttp.js

