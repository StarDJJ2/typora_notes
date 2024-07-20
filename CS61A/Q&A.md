

# 全局变量和局部变量的关系

使用[Online Python Tutor - Composing Programs - Python 3](https://pythontutor.com/cp/composingprograms.html#mode=display)进行查看

```python
x = 12
z = 7

def f(y):
	z = 15
	print(x,y,z)

f(8)
print(x)
```

```python
def f(x):
	return g(x + 1) + 2
	
def g(y):
	return y + 3
	
f(7)
```

从本地帧先开始 再到全局帧

调用函数时候定义本地框架



# 打印字符串和组合字符串

```
x = "hello number" + str(2)
print(x)
print("hello number" , 2)         # 逗号可以解除数据类型的限制，同样的输出字符串
#They have same answer
```

将一行的输出变为两行输出

```
print("hello number", end = " ")
print(2)
```

```
a = 12

print(2+3 , a)

min(2+3, a)        #这里是因为没有打印 所以不会输出值  但是会做计算
```

# 自定义函数不写return结果 默认返回none



# 全局框架中访问本地框架中的变量  

定义的本地框架的函数必须返回该变量  才能在全局中进行访问

## 此情况下不可访问

```
def f(x):
	return 2
f(7)
print(x)
```

## 此情况下可访问  这里的y为全局变量

```
def f(x):
	return x
y = f(7)
print(y)
```

每次调用一次函数都会创建新的本地框架