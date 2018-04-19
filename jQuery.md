
## window.onload

```javascript
$(document).ready(function() {
});
```

## 选择器

```javascript
$('#id') // 按 ID 获取
$('.class') // 按 Class 获取
$('元素') // 按元素获取
```

## ajax

```javascript
$.ajax({
    url: 'url 地址',
    method: 'POST', // 默认 GET。GET/POST/PUT
    data: {},
    dataType: 'json', // Ajax 响应数据类型。xml/html/script/json/jsonp/text
    async: true, // 默认 true,
    cache: true, // 默认 true,
    timeout: 3000, // 请求超时时间，毫秒值
    contentType: 'application/json; charset=UTF-8', // 默认 application/x-www-form-urlencoded; charset=UTF-8
    success: function(data, textStatus, jqXHR) {
    }, // 调用成功完成并返回
    error: function(jqXHR, textStatus, errorThrown) {
    }, // 调用错误回调
});
```

## jQuery 对象操作

#### 取值 & 赋值

```javascript
#('<选择器>').val()
#('<选择器>').val('new value')
```
