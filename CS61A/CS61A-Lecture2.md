# Python函数名

```python
f = max

# max is a built-in function

# and f become a function

max(1,2,3) = f(1,2,3)

# 也可以给max赋值

max = 7

#然后max的功能由f继承，自己变成一个值

#要让max回到原来 只需: max = f
```



# add and mul 函数

from operator import add, mul



```python
from operator import mul
def square(square):
​	return mul(square, square)
square(-2)
```



# print为Non-pure函数，返回值永远是None  但是会有一个额外输出  即打印值
