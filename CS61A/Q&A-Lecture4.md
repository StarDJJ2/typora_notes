# 1.double params

```python
def make_adder(x):
    def adder(y):
        return x+y
    return adder

(make_adder(1))(2)


```

![image-20230707104442521](C:\Users\25075\AppData\Roaming\Typora\typora-user-images\image-20230707104442521.png)

为什么这里的return adder返回的不是adder中return 返回的值，  因为make_adder返回的adder只是函数的名字而不是adder( )

<font color='red'>lamda function相比于def时 statement要更加的简洁，节省name space，让你的代码更加的</font>>compact

```python
pred, curr = 0, 1
pred, curr = curr, pred + curr
pred, curr = curr, pred + curr
pred, curr = curr, pred + curr
pred, curr = curr, pred + curr
```

<font color='red'>在右边的值向左边的变量assign前 ，右边的expression就已经进行了计算</font>



# 2.lamda x : f

```python
def f(y):
    return y + 1

g = lambda x : f

eight = g(2)(7)
```

```python
g = lambda x : lambda y : y + 1

eight = g(2)(7)
```

