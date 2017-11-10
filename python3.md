
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
'Py' + 'thon'
'Py' 'thon' # 中间以空格分割，结果会将字符串连接起来（同+后效果）
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
str = 'Hello world'
str[1]
str[3:5] # 字符区间获取（左包含到右不包含）
str[3:] # 字符区间获取（左包含到右结尾）
str[:5] # 字符区间获取（左开头到右不包含）
str[:] # 字符区间获取（左开头到右结尾）
...
```

### 3.3. 列表

```python
list = [1, 4, 9, 16, 25]
list[2]
list[2:4] # 列表区间获取（左包含到右不包含）。返回的是一个新的列表
list[2:] # 列表区间获取（左包含到右结尾）
list[:4] # 列表区间获取（左开头到右不包含）
list[:] # 列表区间获取（左开头到右结尾）
list + [36, 49, 64, 81, 100] # 拼接列表
list.append(33) # 追加列表
```

### 3.4. 布尔值

```python
# True，真；False，假
```

### 3.5. 索引规律对照

     +---+---+---+---+---+---+
     | P | y | t | h | o | n |
     +---+---+---+---+---+---+
       0   1   2   3   4   5
      -6  -5  -4  -3  -2  -1

### 3.4. 关键字可能被变量名称替代

```python
print('hello world')
print = 'Print by This'
print('hello world') # 这里将报错，print已不再是函数
```

# 4. if语句

```python
if 22 > 11:
    print('22 > 11')
```

## 5. 函数使用

### 5.1. 打印文本

```python
print('Hello world')
print('The value of i is', 2)
print('I have a dream', end='.') # end是关键字，在内容结尾追加内容
print('''\
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
''') # 按格式打印
```

