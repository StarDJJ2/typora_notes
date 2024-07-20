[彻底弄懂 Linux 下的文件描述符（fd）_linux fd管理-CSDN博客](https://blog.csdn.net/yushuaigee/article/details/107883964)

在Linux中，你可以使用<font color='red'>lsof</font>命令来查看一个进程下的文件描述符。具体命令如下：

Copy code

```
lsof -p <进程ID>
```

你需要将`<进程ID>`替换为你要查看的进程的实际ID。这将列出该进程打开的所有文件描述符，包括文件、目录、管道等。

