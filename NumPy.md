
## NumPy 入门

### 引入 NumPy 模块

```python
import numpy as np
```

### 产生随机数

```python
from numpy.random import rand

# 建立一个 长度为3 的随机列表（一维）
rand(3)
# 建立一个 3x3 的随机矩阵（二维）
rand(3, 3)
# 建立一个 3x3x3 的随机矩阵（三维）
rand(3, 3, 3)
```

