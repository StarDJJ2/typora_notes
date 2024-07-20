# 原因：数据采样点的突然增大，触发了多线程机制

torch.set_num_threads( )是PyTorch中的一个函数，用于设置PyTorch的线程数。它的作用是控制PyTorch在执行计算时使用的CPU线程数，从而提高计算效率。可以通过设置torch.set_num_threads(n)来指定使用的线程数，其中n为整数值。

