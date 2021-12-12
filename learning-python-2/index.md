# 🐍一些 python 的内置函数

## map()
`map(func,Iterable)`

map() 函数接收两个参数，一个是函数，一个是 Iterable.

map 将传入的函数依次作用到序列的每个元素，并把结果作为新的 Iterator 返回。

```python
>>> def f(x):
    ...     return x * x
    ...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
    [1, 4, 9, 16, 25, 36, 49, 64, 81]
```

r 是一个 Iterator，是一种惰性序列。所以要用 list() 将其转变为 list 输出。

何为惰性？

迭代器仅仅在迭代至某个元素时才计算该元素，而在这之前或之后，元素可以不存在或者被销毁。

## reduce()
`reduce()`把一个函数作用在一个序列`[x1, x2, x3, ...]`上，这个函数必须接收两个参数，`reduce()`把结果继续和序列的下一个元素做累积计算，其效果就是：
> reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)

```python
>>> from functools import reduce
>>> def fn(x, y):
...     return x * 10 + y
...
>>> def char2num(s):
...     return {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}[s]
...
>>> reduce(fn, map(char2num, '13579'))
    13579
```

## lambda
lambda 的一般形式是关键字 lambda 后面跟一个或多个参数，紧跟一个冒号，以后是一个表达式。
```python
f = lambda x,y,z : x+y+z
print f(1,2,3)  #6
g = lambda x,y=2,z=3 : x+y+z
print g(1,z=4,y=5)  #10
```

