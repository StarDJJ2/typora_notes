[Python入门：使用PyCharm调试Python程序-CSDN博客](https://blog.csdn.net/gelduoe/article/details/83782740)

1.debug工程代码显示为灰度



[新手必会，pycharm的调试功能(史上最详篇) - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/62610785)



最常用调试步骤：

step over（F8快捷键）：在单步执行时，在函数内遇到子函数时不会进入子函数内单步执行，而是将子函数整个执行完再停止，也就是把子函数整个作为一步。在不存在子函数的情况下是和step into效果一样的。简单的说就是，**程序代码越过子函数，但子函数会执行，且不进入。**

step into（F7快捷键）：在单步执行时，遇到子函数就进入并且继续单步执行，有的会跳到源代码里面去执行。

step into my code（Alt+Shift+F7快捷键）：在单步执行时，遇到子函数就进入并且继续单步执行，不会进入到源码中。

step out（Shift+F8快捷键）：假如进入了一个函数体中，你看了两行代码，不想看了，跳出当前函数体内，返回到调用此函数的地方，即使用此功能即可。

Resume program(F9快捷键)：继续恢复程序，直接运行到下一断点处。

以上四个功能，就是最常用的功能，一般操作步骤就是，**设置好断点，debug运行，然后 F8 单步调试，遇到想进入的函数 F7 进去，想出来在 shift + F8，跳过不想看的地方，直接设置下一个断点，然后 F9 过去。**



<font color='red'>写的很好</font>：[学会读懂traceback，处理Python异常-CSDN博客](https://blog.csdn.net/muzico425/article/details/104404295)



异常分类
BaseException 所有异常的基类
Exception 常见错误的基类
ArithmeticError 所有数值计算错误的基类
Warning 警告的基类
AssertError 断言语句（assert）失败
<font color='red'>AttributeError 尝试访问未知的对象属性</font>
DeprecattionWarning 关于被弃用的特征的警告
EOFError 用户输入文件末尾标志EOF（Ctrl+d）
FloattingPointError 浮点计算错误
FutureWarning 关于构造将来语义会有改变的警告
GeneratorExit generator.close()方法被调用的时候
ImportError 导入模块失败的时候
IndexError 索引超出序列的范围
<font color='red'>KeyError</font> 字典中查找一个不存在的关键字
KeyboardInterrupt 用户输入中断键（Ctrl+c）
MemoryError 内存溢出（可通过删除对象释放内存）
<font color='red'>NamerError</font> 尝试访问一个不存在的变量
NotImplementedError 尚未实现的方法
OSError 操作系统产生的异常（例如打开一个不存在的文件）
OverflowError 数值运算超出最大限制
OverflowWarning 旧的关于自动提升为长整型（long）的警告
PendingDeprecationWarning 关于特征会被遗弃的警告
ReferenceError 弱引用（weak reference）试图访问一个已经被垃圾回收机制回收了的对象
RuntimeError 一般的运行时错误
RuntimeWarning 可疑的运行行为（runtime behavior）的警告
StopIteration 迭代器没有更多的值
SyntaxError Python的语法错误
SyntaxWarning 可疑的语法的警告
IndentationError 缩进错误
TabError Tab和空格混合使用
SystemError Python编译器系统错误
SystemExit Python编译器进程被关闭
<font color='red'>TypeError</font> 不同类型间的无效操作
UnboundLocalError 访问一个未初始化的本地变量（NameError的子类）
UnicodeError Unicode相关的错误（ValueError的子类）
UnicodeEncodeError Unicode编码时的错误（UnicodeError的子类）
UnicodeDecodeError Unicode解码时的错误（UnicodeError的子类）
UserWarning 用户代码生成的警告
<font color='red'>ValueError</font> 传入无效的参数
ZeroDivisionError 除数为零
<font color='red'>FileNotFoundError</font> 没有找到指定文件