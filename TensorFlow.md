
## TensorFlow 概念

### 图graphs 表示计算任务

### 会话Session 在上下文中执行 图graphs，图graphs 必须在 会话Session里被启动

### Tensor 表示数据，可以看成一个n维的数据或列表

### 变量Variable 来维护数据

### 使用feed、fetch为任意的操作赋值或获取数据

### TensorFlow是一个编程系统，图graphs 中的节点称为 op（operation），一个op获得0或多个Tensor，执行计算，产生0或多个Tensor

## TensorFlow 概念图

![TensorFlow 概念图](/TensorFlow-概念图.png)

## TensorFlow 入门

### 引用 TensorFlow 模块

```python
import tensorflow as tf
```

### 常量

```python
#value: 常量值
#dtype: 常量类型（可选）
#name: 常量名称（可选）

#返回：<class 'tensorflow.python.framework.ops.Tensor'>

const1 = tf.constant(value=3.0, dtype=tf.float32, name='const1')
```

### 变量 Variables

创建变量

```python
#initial_value: 变量值
#name: 变量名（可选）

#返回：<class 'tensorflow.python.ops.variables.Variable'>

var1 = tf.Variable(initial_value=0, name='var1')
```

初始化变量，创建完所有变量之后初始化

```python
init = tf.global_variables_initializer()

session.run(init)
```

### Op

add（相加）

```python
#x: 数据
#y: 数据
#name: 常量名称（可选）

#返回：<class 'tensorflow.python.framework.ops.Tensor'>

addv = tf.add(x=1, y=2, name='addv')
```

subtract（相减）

```python
#x: 数据
#y: 数据
#name: 常量名称（可选）

#返回：<class 'tensorflow.python.framework.ops.Tensor'>

subtractv = tf.subtract(x=1, y=2, name='subtractv')
```

multiply（相乘）

```python
#x: 数据
#y: 数据
#name: 常量名称（可选）

#返回：<class 'tensorflow.python.framework.ops.Tensor'>

multiplyv = tf.multiply(x=2, y=3, name='multiplyv')
```

divide（相除）

```python
#x: 数据
#y: 数据
#name: 常量名称（可选）

#返回：<class 'tensorflow.python.framework.ops.Tensor'>

dividev = tf.divide(x=6, y=3, name='dividev')
```

assign（赋值）

```python
#ref：<class 'tensorflow.python.ops.variables.Variable'> 对象
#value：赋予的值

#返回：<class 'tensorflow.python.framework.ops.Tensor'>

uv = tf.assign(ref=a, value=b) # 相当于 a = b，把 b 赋给 a
```

