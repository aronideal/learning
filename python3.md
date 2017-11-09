
## .py文件声明部分

### 指定设备环境

```python
#!/usr/bin/env python3
```

### 设定编码

```python
# -*- coding: utf-8 -*-
```

## 源码注释

```python
# this is the first comment
```

## 变量的使用

### 数字

```python
width  =  20
height  =  17 / 3
```

### 字符串

```python
name  =  "李四"
```

## 打印内容

### 打印固定文本

```python
print('Hello world')
```

### 按格式打印

```python
print("""\
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
""")
```

### 打印包括转义字符的内容

```python
print(r'C:\some\name') # 此处使用'r'前缀，则\n不会被当做换行符
```

## 计算字符串长度

```python
len('Hello world')
```
