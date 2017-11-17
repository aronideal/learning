
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

### 2.3. 模块调用

#### 2.3.1. 定义模块

如：hello.py

```python
def func():
    print('hello world')
```

#### 2.3.2. 调用模块的功能

导入库或导入函数

```python
import a
a.func()

from a import func # func 这个位置可以写成导入以 ‘,’ 分隔的多个函数，或 *，导入 a 库里的所有函数
func()
```

函数调用的名字可任意替代

```python
afunc = a.func
afunc()
```

使用 as 关键字重命名引用

```python
import a as moda
from a import func as func1
```

#### 2.3.3. 如果模块需要命令行直接执行，需要添加以下 if 语句

```python
if __name__ == '__main__':
    pass # 这里用实际业务逻辑代替
```

如需获取参数，需导入 sys 库

```python
import sys
sys.argv[1]
```

#### 2.3.4. 列举出模块里的所有函数或属性

```python
import sys

print(dir(sys))
```

#### 2.3.5. 模块分包和调用

```python
import a.b.c # 目录结构为 a/b/c.py
import a.b1 # 目录结构为 a/b1.py
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

#### 3.2.5. strip 移除头尾的字符

```python
''.strip() # 默认是去除空格
''.strip('_')
```

### 3.3. 元组

```python
tu = 1, 56, 'abc' # 声明元组，返回的是<class 'tuple'>
tu[2] # 按索引取值
tu[2] = 7 # 赋值会报错，因为元组是不可变的
```

### 3.4. 列表

带有 [2:3] 的读取称为 分片

带有 [2:3:1] 第三个值叫做 步长

```python
ls = [1, 4, 9, 16, 25]
ls[2]
ls[2:4] # 列表区间获取（左包含到右不包含）。返回的是一个新的列表
ls[2:4:2] # 列表区间获取（左包含到右不包含）。返回的是一个新的列表
ls[2:] # 列表区间获取（左包含到右结尾）
ls[:4] # 列表区间获取（左开头到右不包含）
ls[:] # 列表区间获取（左开头到右结尾）
ls + [36, 49, 64, 81, 100] # 拼接列表
ls.append(33) # 追加列表。返回None，影响list的值
ls.insert(2, 66) # 在索引位置前插入值。返回None，影响list的值
ls.extend([28, 33, 66]) # 扩展列表内容。返回None，影响list的值
ls.remove('6') # 删除列表第一个相同的内容。返回None，影响list值。不存在则报错
ls.pop(index) # 取出并删除list对应索引的数据，不传则从取删最后一个索引位的数据。返回对应的数据。不存在则报错
ls.clear() # 清理list所有的数据。返回None
ls.reverse() # 反转list数据。影响list。返回None
ls.count(4) # 在list查找指定值的出现个数。返回个数。未找到返回0
ls.index('3') 或 ls.index('3', 2) 或 ls.index('3', 2, 4) # 第一个参数是被搜索索引位的数据，第二个是begin包含，第三个是end不包含。返回第一个相同数据所在的索引，找不到则报错
ls.copy() # 返回一个新地址的list，得到的list做任何操作都不会影响本身的list
```

#### 3.4.1. 列表排序

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

### 3.5. 字典 <class 'dict'>

```python
d = {'a':'av', 'b':'b'}
```

清空字典

```python
d.clear() # 返回 <class 'NoneType'>，直接改变 d
```

拷贝字典

```python
d.copy() # 返回 <class 'dict'>，不改变 d
```

列举 key

```python
list(d.keys()) # 返回 <class 'dict_keys'>，不改变 d
```

通过 key 筛选

```python
d.get('b') # 返回值的类型。返回值。不存在时返回 <class 'NoneType'>
同 d['b']，不同的是 key 不存在，会报错
```

### 3.6. set

不会重复、无序。类型：<class 'set'>

```python
setval = {'a','b',1,2,3,1,1,2,3} # 会把相同的数据剔除掉，剩下唯一的。且数据无序
setval = set('ab1231123') # 会把相同的数据剔除掉，剩下唯一的。且数据无序
print({'a','b',6,''}-{'a','b',6}) # 相减，结果里只会筛选出左侧有，右侧没有的数据
print({'a','b',6,''}&{'a','b',6}) # 与，或者使用and连接。取交集，两侧都有的集合
print({'a','b',6,''}|{'a','b',6}) # 或，或者使用or连接。取并集，两侧所有数据的集合
print({'a','b',6,''}^{'a','b',6}) # 异或。取只有1方有的数据的集合
```

### 3.7. list tuple set dict 等区分

```python
['a', 'b', 'c'] # list
('a', 'b', 'c') # tuple
{'a', 'b', 'c'} # set
{'arg0':'a', 'arg1':'b', 'arg2':'c'} # dict
```

### 3.8. 布尔值

```python
True # 真
False # 假
```

### 3.9. 空对象

```python
None
```

### 3.10. 索引规律对照

     +---+---+---+---+---+---+
     | P | y | t | h | o | n |
     +---+---+---+---+---+---+
       0   1   2   3   4   5
      -6  -5  -4  -3  -2  -1

### 3.11. 关键字可能被变量名称替代

```python
print('hello world')
print = 'Print by This'
print('hello world') # 这里将报错，print已不再是函数
```

### 3.12. π

```python
from math import pi # 需引入math里的pi

print(pi)
```

### 3.13. del 关键字

删除变量（删除对数据的引用），不是删除数据。

```python
a = 1 # 变量 a 指向对象1
b = a # 变量 b 指向对象1
del a # 删除变量 a 对 对象1 的引用，但 b 依然引用着 对象1
print(b) # b 对 对象1 的引用还在，打印结果为 1

ls = [1,2,3]
del ls[1] # 删除的是变量引用 ls[1]，而不是数据 2
```

### 3.14. in、not in 关键字

```python
'1' in ['1', '2', 'c'] # 返回True
'1' not in ['1', '2', 'c'] # 返回False
```

### 3.15. 序列解包

```python
a, b, c = [1,2,3] # 或 a, b, c = (1,2,3) 或 其它序列形式

print(a) # 1
print(b) # 2
print(c) # 3
```

## 4. 运算符

### 4.1. 算数运算符 +、-、*、/、//、%、**

```python
2 + 3
2 - 3
2 * 3
2 / 3 # 无论参与运算的数据是否整型，全部返回浮点数
2 // 3 # 无论参与运算的数据是否浮点型，全部返回整数
2 % 3 # 取余运算
2**3 # 幂（乘方）运算。2的3次方
```

### 4.2. 比较运算符 <、<=、>、>=、==、!=

```python
2 < 3
2 <= 3
2 > 3
2 >= 3
2 == 3
2 != 3
```

### 4.3. 逻辑运算符 and

逻辑与。当左右表达式全部为True，返回True。否则，False

注意：逻辑运算符and支持短路计算，即左边为False，直接返回False，不再去计算右边表达式

```python
True and True -> True
True and False -> False
False and True -> False
False and False -> False
```

### 4.4. 逻辑运算符 or

逻辑或。当左右表达式全部为False，返回False。否则，True

注意：逻辑运算符or支持短路计算，即左边为True，直接返回True，不再去计算右边表达式

```python
True or True -> True
True or False -> True
False or True -> True
False or False -> False
```

### 4.5. 逻辑运算符 not

逻辑非。当右表达式为False，返回True。否则，False

```python
not True -> False
not False -> True
```

### 4.6. 运算符优先级

![运算符优先级](/python3-运算符优先级.png)

## 5. if 语句

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

其它写法：

```python
ret = x if x < y else y # 如果 x < y 为 True，则 ret 为 x。反之，ret 为 y。类似于三目运算

ret = [y, x][x < y] # 如果 x < y 为 True，则 ret 为 x。反之，ret 为 y。类似于三目运算
```

## 6. 循环

### 6.1. for 语句

```python
for n in [1,2,3]:
    print(n)
```

其它用法：

```python
ret = [x for x in range(10)] # 循环出0-9，放到一个list

ret = [(x, y) for x in [1,2,3] for y in [4,5,6]] # 多层循环，越往前越是外层，放到一个list
ret = [(x, y) for x in [1,2,3] for y in [4,5,6] if x != 1 and y != 5] # 多层循环，越往前越是外层，筛选，放到一个list
```

### 6.2. while 语句

```python
n = 0
while True:
    if n >= 3:
        break
    print(n)
    n=n+1
```

### 6.3. 循环控制

```python
break # 结束所在的循环体
continue # 跳过当前循环索引
else:
    print('else 内容块') # 循环条件不满足被触发（break之后不会触发）
```

## 7. 其它用法

### 7.1. pass 语句

```python
pass # 当成一个普通语句执行，但不会产生任何效果。需要一个空实现的时候使用
```

## 8. 自定义函数

### 8.1. 无参

```python
def func():
    print('This is a function')

func()
```

### 8.2. 有参和默认值

```python
def func(arg1, arg2=3): # b有默认值，可不传
    print('This is a function', arg1, arg2)

func('v1')
func('v1', 'v2')
# 如果函数定义了1个以上有默认值的参数，调用的时候需写明参数名
multi_param_func('he', arg2='ll', arg3='o')
```

### 8.3. * 和 ** 参数

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

### 8.4. 有返回值

```python
def func(arg1):
    print('This is a function', arg1)
    return True

ret = func('v1')
```

### 8.5. 增加函数注解 (Function Annotations）

函数注解给使用者提供函数说明

```python
def func(arg0, arg1 : '参数1', arg2 : '参数2，默认值：2' = 2) -> '返回值：None':
    pass

func(2, 3, 4) # 正常调用得到函数功能。如需打印 Function Annotations 可通过 func.__annotations__ 得到
```

### 8.6. 增加doc注释

函数内第一行写'''注释，说明函数调用方法和功能。好处是可通过__doc__获得函数的介绍，更轻松的调用函数功能。如下：

```python
def func(arg0, arg1=3):
    '''
    func(arg0, arg1=3) -> None

    Return None. This function is test.

    Required arguments:
    arg0:   This is arg0.
    Optional arguments:
    arg1:   This is arg1.
    '''
    pass

print(func.__doc__)
```

### 8.7. 使用lambda关键字构建匿名函数

```python
def func(b):
    return lambda a: a + b # 返回的是lambda定义，是function类型。多个参数，则声明成lambda a,b,c:

lambdaFunc = func(66)
ret = lambdaFunc(77) # ret的值是66+77=132
```

## 9. 系统函数

### 9.1. print 函数

```python
print('Hello world')
print('The value of i is', 2)
print('b' in ['a', 'b', 'c'])
print('I have a dream', end='.') # end是关键字，在内容结尾追加内容
print('''\
Usage: thingy [OPTIONS]
     -h                        Display this usage message
     -H hostname               Hostname to connect to
''') # 按格式打印
print(func.__doc__) # func是一个函数名，结果将打印'''里的注释内容
```

### 9.2. input 函数

接收一个客户端输入，参数prompt是提示文本，返回字符串

```python
input('Hello')
```

### 9.3. int 函数

```python
int('1') # 转换str类型为int类型
```

### 9.4. list 函数

```python
list(range(5)) # 转换range类型为list类型
list(tuple('123456')) # 将list类型转换为tuple类型
list(map(lambda x: x, '123456'))
```

### 9.5. map 函数

```python
map(lambda x: x, range(10))) # <class 'map'>
```

### 9.6. len 函数

```python
len('Hello world') # 字符串
len([1,2,3,4]) # list
```

### 9.7. tuple 函数

```python
tuple(list('123456')) # 将list类型转换为tuple类型
```

### 9.8. range 函数

```python
range(5) # == 0,1,2,3,4 （左包含到右不包含）
range(2,5) # == 2,3,4 （左包含到右不包含）
range(0,5,2) # 第3个值表示增量，不指定则默认为1
```

### 9.9. abs 函数

取绝对值：

```python
abs(5) # -> 5
abs(-5) # -> 5
```

### 9.10. str 函数

```python
str('111') # <class 'str'>
```

### 9.11. round 函数

计算四舍五入值：

round(number[, ndigits]) -> number

number 是待四舍五入的数据
ndigits 是保留的小数位数

返回四舍五入的结果。

```python
round(3.141592653589793)
round(3.141592653589793, -1)
round(3.141592653589793, 0)
round(3.141592653589793, 1)
```

### 9.12. min 与 max 函数

计算最小值和最大值

```python
min([1,2,3])
max([1,2,3])
```

### 9.13. type 函数

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

### 9.14. reversed 函数

```python
list(reversed([1,2,3,4,5]))
```

### 9.15. sorted 函数

```python
sorted([1,2,3,4,5])
```

### 9.16. set 函数

```python
set([1,2,3,4,5])
```

### 9.17. math 函数

```python
from math import isnan

isnan(float('NaN')) # 计算是否非数字
```

## 10. 队列操作

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


