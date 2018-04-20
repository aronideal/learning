
## 页面加载回调，同 window.onload

```javascript
$(document).ready(function() {
});
```

## ajax 请求

```javascript
$.ajax({
    url: 'url 地址',
    username: '认证用户名',
    password: '认证密码',
    type: 'POST', // 默认 GET。GET/POST/PUT
    method: 'POST', // 1.9版本后才新增，兼容请使用 type。 默认 GET。GET/POST/PUT
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

## 选择器

```javascript
$('#id') // 按 ID 获取
$('.class') // 按 Class 获取
$('元素') // 按元素获取
```

## jQuery 对象操作

#### 判断 class 定义 & 添加 class 定义 & 移除 class 定义

```javascript
#('<选择器>').hasClass('className')
#('<选择器>').addClass('className')
#('<选择器>').removeClass('className')
```

#### 取值 & 赋值，同 element.value

```javascript
#('<选择器>').val()
#('<选择器>').val('new value')
```

## 获得内部文本 & 设置内部文本，同 element.interText

```javascript
#('<选择器>').text()
#('<选择器>').text('sssss')
```

## 获得内部html & 设置内部html，同 element.interHTML

```javascript
#('<选择器>').html()
#('<选择器>').html('<br/>')
```
