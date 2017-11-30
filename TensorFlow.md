
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

node1 = tf.constant(value=3.0, dtype=tf.float32, name='const1')
```

### 变量 Variables

创建变量

```python
#initial_value: 变量值
#name: 变量名（可选）

#返回：<class 'tensorflow.python.ops.variables.Variable'>

tf.Variable(initial_value=0, name='num')
```

初始化变量，创建完所有变量之后初始化

```python
init = tf.global_variables_initializer()

session.run(init)
```

### Op

add（x、y相加）

```python
#value: 常量值
#dtype: 常量类型（可选）
#name: 常量名称（可选）

#返回：<class 'tensorflow.python.framework.ops.Tensor'>

addv = tf.add(x=1, y=2, name='addv')
```

```python
update = tf.assign(state, new_state)
```

