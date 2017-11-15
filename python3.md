
[官网学习指南](https://docs.python.org/3/tutorial/)    [Python下载](https://www.python.org/downloads/)    [PyCharm开发环境下载](https://www.jetbrains.com/pycharm/download/)

如果报出：

    无法启动此程序，因为计算机中丢失 api-ms-win-crt-runtime-l1-1-0.dll。尝试重新安装该程序以解决此问题。 

下载安装Windows支持库，最后重启电脑以解决：

    https://www.microsoft.com/zh-CN/download/details.aspx?id=53840


## 1. python3 文件规范

### 1.1. 指定设备环境

```python
#!/usr/bin/env python3
```

### 1.2. 设定编码

```python
# -*- coding: UTF-8 -*-
```

## 2. python3 编程习惯

### 2.1. 严格遵守换行缩进

以4个space（或1个tab）作为一个缩进单位（依个人习惯）

    +---+---+---+---+---+---+---+---+---+---+---+---+
    | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10| 11| 12|
    +---+---+---+---+---+---+---+---+---+---+---+---+
    |               | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
    +---+---+---+---+---+---+---+---+---+---+---+---+
    |               |               | 1 | 2 | 3 | 4 |
    +---+---+---+---+---+---+---+---+---+---+---+---+

### 2.2. 源码加注释

```python
# 单行注释

'''
多行注释
'''

"""
多行注释
"""
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

#### 3.2.3. 读取字符

```python
str = 'Hello world'
str[1]
str[3:5] # 字符区间获取（左包含到右不包含）
str[3:] # 字符区间获取（左包含到右结尾）
str[:5] # 字符区间获取（左开头到右不包含）
str[:] # 字符区间获取（左开头到右结尾）
...
```

#### 3.2.4. join 连接序列成字符串

```python
'-'.join(list('123'))
'-'.join(tuple('123'))
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
list.append(33) # 追加列表。返回None，影响list的值
list.insert(2, 66) # 在索引位置前插入值。返回None，影响list的值
list.extend([28, 33, 66]) # 扩展列表内容。返回None，影响list的值
list.remove('6') # 删除列表第一个相同的内容。返回None，影响list值。不存在则报错
list.pop(index) # 取出并删除list对应索引的数据，不传则从取删最后一个索引位的数据。返回对应的数据。不存在则报错
list.clear() # 清理list所有的数据。返回None
list.reverse() # 反转list数据。影响list。返回None
list.count(4) # 在list查找指定值的出现个数。返回个数。未找到返回0
list.index('3') 或 list.index('3', 2) 或 list.index('3', 2, 4) # 第一个参数是被搜索索引位的数据，第二个是begin包含，第三个是end不包含。返回第一个相同数据所在的索引，找不到则报错
list.copy() # 返回一个新地址的list，得到的list做任何操作都不会影响本身的list
```

#### 3.3.1. 列表排序

* key 列表排序的规则

* reverse 逆序列表的值

```python
list = [1, 4, 9, 16, 25]
list.sort(key=lambda item: item)
list.sort(key=lambda item: item, reverse=True)
```

复杂列表的排序：

```python
list = [['a', 2], ['b', 3], ['c', 1]]
list.sort(key=lambda item: item[0])
list.sort(key=lambda item: item[1])
```

### 3.4. 布尔值

```python
True # 真
False # 假
```

### 3.5. 空对象

```python
None
```

### 3.6. 索引规律对照

     +---+---+---+---+---+---+
     | P | y | t | h | o | n |
     +---+---+---+---+---+---+
       0   1   2   3   4   5
      -6  -5  -4  -3  -2  -1

### 3.7. 关键字可能被变量名称替代

```python
print('hello world')
print = 'Print by This'
print('hello world') # 这里将报错，print已不再是函数
```

## 4. if 语句

```python
if 22 > 11:
    print('22 > 11')
elif 22 == 11:
    print('22 == 11')
else:
    print('22 < 11')
```

使用in关键字：

```python
if ok in ('y', 'ye', 'yes'):
    print(ok)
```

is 和 ==：

```python
if [2] is [2]: # is是对象的比对，不成立
    pass
if [2] == [2]: # ==是值的比对，成立
    pass
```

## 5. 循环

### 5.1. for 语句

```python
for n in [1,2,3]:
    print(n)
```

### 5.2. while 语句

```python
n = 0
while True:
    if n >= 3:
        break
    print(n)
    n=n+1
```

### 5.3. 循环控制

```python
break # 结束所在的循环体
continue # 跳过当前循环索引
else:
    print('else 内容块') # 循环条件不满足被触发（break之后不会触发）
```

## 6. 其它用法

### 6.1. pass 语句

```python
pass # 当成一个普通语句执行，但不会产生任何效果。需要一个空实现的时候使用
```

## 7. 自定义函数

### 7.1. 无参

```python
def func():
    print('This is a function')

func()
```

### 7.2. 有参和默认值

```python
def func(arg1, arg2=3): # b有默认值，可不传
    print('This is a function', arg1, arg2)

func('v1')
func('v1', 'v2')
# 如果函数定义了1个以上有默认值的参数，调用的时候需写明参数名
multi_param_func('he', arg2='ll', arg3='o')
```

### 7.3. * 和 ** 参数

\* 是 <class 'tuple'>

\*\* 是 <class 'dict'>

```python
def func(*values): # * 只能存在一次
    for value in values:
        print(value)

def func1(**keypairs): # ** 只能存在一次
    for key in keypairs:
        print(key, '=', keypairs[key])

def func2(*values, **keypairs): # * 和 ** 同时存在时，* 必须放在 ** 前。* 和 ** 只能存在一次
    for value in values:
        print(value)
    for key in keypairs:
        print(key, '=', keypairs[key])

func('1', '2', '3') # 不能指定参数名
func1(a='1', b='2', c='3') # 必须指定参数名
func2('1', '2', '3', a='1', b='2', c='3') # 必须指定参数名
```

### 7.4. 有返回值

```python
def func(arg1):
    print('This is a function', arg1)
    return True

ret = func('v1')
```

### 7.5. 增加函数注解 (Function Annotations）

函数注解给使用者提供函数说明

```python
def func(arg0, arg1 : '参数1', arg2 : '参数2，默认值：2' = 2) -> '返回值：None':
    pass

func(2, 3, 4) # 正常调用得到函数功能。如需打印 Function Annotations 可通过 func.__annotations__ 得到
```

### 7.6. 增加doc注释

函数内第一行写'''注释，说明函数调用方法和功能。好处是可通过__doc__获得函数的介绍，更轻松的调用函数功能。如下：

```python
def func(arg0):
    '''func(arg0) -> None -- 空函数，举例说明这行注释的意义'''
    pass

print(func.__doc__)
```

### 7.7. 使用lambda关键字构建匿名函数

```python
def func(b):
    return lambda a: a + b # 返回的是lambda定义，是function类型。多个参数，则声明成lambda a,b,c:

lambdaFunc = func(66)
ret = lambdaFunc(77) # ret的值是66+77=132
```

## 8. 系统函数

### 8.1. print 函数

```python
print('Hello world')
print('The value of i is', 2)
print('I have a dream', end='.') # end是关键字，在内容结尾追加内容
print('''\
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
''') # 按格式打印
print(func.__doc__) # func是一个函数名，结果将打印'''里的注释内容
```

### 8.2. input 函数

接收一个客户端输入，参数prompt是提示文本，返回字符串

```python
input('Hello')
```

### 8.3. int 函数

```python
int('1') # 转换str类型为int类型
```

### 8.4. list 函数

```python
list(range(5)) # 转换range类型为list类型
list(tuple('123456')) # 将list类型转换为tuple类型
```

### 8.5. len 函数

```python
len('Hello world') # 字符串
len([1,2,3,4]) # list
```

### 8.6. tuple 函数

```python
tuple(list('123456')) # 将list类型转换为tuple类型
```

### 8.7. range 函数

```python
range(5) # == 0,1,2,3,4 （左包含到右不包含）
range(2,5) # == 2,3,4 （左包含到右不包含）
range(0,5,2) # 第3个值表示增量，不指定则默认为1
```

### 8.8. type 函数

检查数据类型：

```python
type(2)
type(None)
type(print)
```

返回：

    <class 'int'>
    <class 'NoneType'>
    <class 'builtin_function_or_method'>

## 9. 队列操作

```python
from collections import deque

deq = deque([1,2,3,4,5,6])

deq.append(7) # 追加到队尾，返回None。影响队列
deq.appendleft(8) # 追加到队头，返回None。影响队列

deq.pop() # 返回尾部数据，并影响队列数据。空队列执行后报错
deq.popleft() # 返回头部数据，并影响队列数据。空队列执行后报错

# 其它用法同list
...

print(deq)
```


