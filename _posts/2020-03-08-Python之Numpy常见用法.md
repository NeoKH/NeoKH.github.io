---
title: Numpy之concatenate方法
tags:
  - Python
  - Numpy
---

`concatenate`，顾名思义，起拼接作用。需要注意的是它的`axis`参数，同其他高维操作一样，该函数在作用于高维数组时容易思维混乱。所以在此记录一个例子，以供分析：

```py
import numpy as np
a=[
	[ [[ 1],[ 2],[ 3]],
	  [[ 4],[ 5],[ 6]] ],
	[ [[ 7],[ 8],[ 9]],
	  [[10],[11],[12]] ]
  ]
print(np.concatenate(a,axis=0))
print(np.concatenate(a,axis=1))
print(np.concatenate(a,axis=2))
```

a是一个四维数组。当concatenate的第一个参数是一个数组而不是多个数组，拼接的其实是所有的`a[i]`，即在本例中，`np.concatenate(a,axis=0)`写法等同于`np.concatenate((a[0],a[1]),axis=0)`。

- 第一个拼接结果

```py
[
 [[ 1][ 2][ 3]]
 [[ 4][ 5][ 6]]
 [[ 7][ 8][ 9]]
 [[10][11][12]]
]
```

- 第二个拼接结果

```py
[
 [[ 1][ 2][ 3][ 7][ 8][ 9]]
 [[ 4][ 5][ 6][10][11][12]]
]
```

- 第三个拼接结果

```py
[
 [[ 1  7][ 2  8][ 3  9]]
 [[ 4 10][ 5 11][ 6 12]]
]
```



