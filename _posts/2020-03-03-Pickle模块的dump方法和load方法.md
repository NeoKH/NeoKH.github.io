---
title: Python之Pickle模块
tags:
  - Python
---

# Python之Pickle模块

> python的pickle模块实现了基本的数据序列和反序列化。通过pickle模块的序列化操作我们能够将程序中运行的对象信息保存到文件中去，永久存储；通过pickle模块的反序列化操作，我们能够从文件中创建上一次程序保存的对象。

## dump方法

```python
pickle.dump(obj, file, [,protocol])
```

- 功能：序列化对象，将对象obj保存到文件file中去。

- 参数`protocol`：表示用到的序列化协议。目前有5种协议，但不需要作过多了解，一般它的取值有以下两种：

  - `pickle.HIGHEST_PROTOCOL`：表示最高可用的协议版本。[点击此处了解更多](https://www.programcreek.com/python/example/701/pickle.HIGHEST_PROTOCOL)

  - `pickle.DEFAULT_PROTOCOL`：表示用来pickling的默认协议版本。可能比`pickle.HIGHEST_PROTOCOL`小。目前默认的协议版本是3，协议3是专门为Python3设计的一种新的协议。

    如果没有指定该参数，就是默认的`DEFAULT_PROTOCOL`。

- 参数`file`：file表示保存到的类文件对象，**file必须有write()接口**，file可以是一个以'w'打开的文件或者是一个StringIO对象，也可以是任何可以实现write()接口的对象。



## load方法



```py
pickle.load(file, *, fix_imports=True, encoding="ASCII", errors="strict")
```

- 功能：从文件对象中读取一个序列化后的对象并将其解序列化成原来的层级结构。
- `file`参数必须有两个方法：`read()`方法接收一个整数参数和一个`readlines()`方法不要求参数。两个方法都应该返回字节。

- 其他参数暂不关注



## pickle模块衍生出两个类

- `class pickle.Pickler(file, protocol=None, *, fix_imports=True)`
- `class pickle.Unpickler(file, *, fix_imports=True, encoding="ASCII", errors="strict")`
- 这两个类也有一些方法，跟上面的方法等价，例如`Pickler`类的`dump()`方法和`Pickler(file, protocol).dump(obj)`等价、`load()`方法和`Unpickler`类的`load()`方法等价。

## 什么东西可以被序列化

- `None`, `True`, 和 `False`
- 整数、浮点数和复数
- 字符串、字节和字节数组
- 元组、列表、集合和仅包括可序列化对象的字典
- 定义在一个模块上层的函数
- 定义在一个模块上层的内建函数
- 定义在一个模块上层的类
- 一些类的实例，这些类包括其`__dict__`或调用`__getstate__()`的结果是可序列化的。

### 示例代码

```py
import pickle

# An arbitrary collection of objects supported by pickle.
# 支持序列化的字典
data = {
    'a': [1, 2.0, 3, 4+6j],
    'b': ("character string", b"byte string"),
    'c': {None, True, False}
}

with open('data.pickle', 'wb') as f:
    # Pickle the 'data' dictionary using the highest protocol available.
    # 用最高协议版本序列化data字典，将其写入文件"data.pickle"中
    pickle.dump(data, f, pickle.HIGHEST_PROTOCOL)
```



```pyt
# 经过上面的代码，已经在本地磁盘中写入了一个文件"data.pickle"，现在我们将其读入，并将其解序列化
import pickle

with open('data.pickle', 'rb') as f:
    # The protocol version used is detected automatically, so we do not
    # have to specify it.
    data = pickle.load(f)
print(data)
```





---

参考博客：

[https://blog.csdn.net/gaishi_hero/article/details/82025234](https://blog.csdn.net/gaishi_hero/article/details/82025234)

