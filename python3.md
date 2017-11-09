
[官网学习指南](https://docs.python.org/3/tutorial/)     [PyCharm集成开发环境下载](https://www.jetbrains.com/pycharm/download/)

## 1. py文件声明部分

### 1.1. 指定设备环境

```python
#!/usr/bin/env python3
```

### 1.2. 设定编码

```python
# -*- coding: utf-8 -*-
```

## 2. 源码注释

```python
# this is the first comment
```

## 3. 变量的使用

### 3.1. 数字

```python
width  =  20
height  =  17 / 3
```

### 3.2. 字符串

```python
name  =  '李四'
```

#### 3.2.1. 计算字符串长度

```python
len('Hello world')
```

#### 3.2.2. 读取字符

```python
word = 'Hello world'
word[0]
word[1]
...
```

## 4. 打印内容

### 4.1. 打印固定文本

```python
print('Hello world')
```

### 4.2. 按格式打印

```python
print('''\
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
''')
```

### 4.3. 打印包括转义字符的内容

```python
print(r'C:\some\name') # 此处使用'r'前缀，则\n不会被当做换行符
```
