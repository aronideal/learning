
[官网学习指南](https://docs.python.org/3/tutorial/)     [PyCharm集成开发环境下载](https://www.jetbrains.com/pycharm/download/)

## 1. py文件声明部分

### 1.1. 指定设备环境

```python
#!/usr/bin/env python3
```

### 1.2. 设定编码

```python
# -*- coding: UTF-8 -*-
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

#### 3.2.1. 字符串格式化

```python
'Hello {}, I\'m {}'.format('Mr.Li', 'here')
'Hello {0}, I\'m {1}'.format('Mr.Li', 'here')
'Hello {name}, I\'m {location}'.format(name='Mr.Li', location='here')
'Hello {info[0]}, I\'m {info[1]}'.format(info=['Mr.Li', 'here'])
'Hello {info[name]}, I\'m {info[location]}'.format(info={'name':'Mr.Li', 'location':'here'})
'Py'      'thon' # 中间以空格分割，结果会将字符串连接起来
```

#### 3.2.2. 使用'\\'转义字符

```python
'I\'m here.'
"\"I'm here!\", she said."
'space\ninput'
```

使用'r'前缀，'\\'转义字符被当做普通字符处理

```python
r'C:\some\name' # win32系统中路径使用r的情况比较多
```

#### 3.2.3. 计算字符串长度

```python
len('Hello world')
```

#### 3.2.4. 读取字符

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
