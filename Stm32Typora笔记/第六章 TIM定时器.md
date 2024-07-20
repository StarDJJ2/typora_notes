外部中断占用CPU资源，定时器计数不占用CPU资源，定时器计数的速度也比外部中断快

外部中断只通过外部影响控制中断，而定时器中断需要提供一个数

定时器本质上是一个计数器，对外部脉冲进行计数

1Hz对应1s，1KHz对应1ms，1MHz对应1us

1MHz等于1000000Hz，1kHz等于1000Hz

[STM32—TIM（基本定时器）详解_stm32的tim-CSDN博客](https://blog.csdn.net/qq_45689790/article/details/114022445)

[初学STM32之定时器中断-CSDN博客](https://blog.csdn.net/MRVENJSR/article/details/122998889?ops_request_misc=%7B%22request%5Fid%22%3A%22170806747916800222894405%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fall.%22%7D&request_id=170806747916800222894405&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-19-122998889-null-null.142^v99^pc_search_result_base6&utm_term=STM32定时中断&spm=1018.2226.3001.4187)

[STM32学习笔记（四）丨TIM定时器及其应用（定时中断、内外时钟源选择）_tim时钟-CSDN博客](https://blog.csdn.net/weixin_62179882/article/details/128462610)

[STM32定时器（TIM）之预分频器（PSC）详解 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/82590576)

基本定时器只支持向上计数这一种计数模式。

通用定时器和高级定时器支持向上计数，向下计数和中央对齐（先向上计数，再向下计数）这三种计数模式

<font color='red'>定时器时钟（CK_CNT）</font>

ARPE介绍：[STM32 ARPE寄存器，影子寄存器_32中arpe是什么-CSDN博客](https://blog.csdn.net/nie15870449223/article/details/84503964)



计数器计数频率和计数器溢出频率：

[STM32单片机定时器时钟频率，计数器溢出率的理解_stm32f103的机器周期-CSDN博客](https://blog.csdn.net/x2872653493/article/details/134720954)



定时一秒，就表示定时频率为1Hz。

计算公式为：<font color='red'>CK_PSC / (PSC + 1) / (ARR + 1)</font>：72Mhz/10000/7200  （在10k的计数频率下，计100000个数）

PSC和ARR的范围都要在0~65535之间



在TIM_TimeBaseInit函数的最后，会立刻生成一个更新事件，来重新装载预分频器和重复计数器的值
预分频器有缓冲寄存器，我们写入的PSC和ARR只有在更新事件时才会起作用
为了让写入的值立刻起作用，故在函数的最后手动生成了一个更新事件
但是更新事件和更新中断是同时发生的，更新中断会置更新中断标志位，手动生成一个更新事件，就相当于在初始化时立刻进入更新函数执行一次
在开启中断之前手动清除一次更新中断标志位，就可以避免刚初始化完成就进入中断函数的问题
