[STM32笔记之EXTI外部中断-CSDN博客](https://blog.csdn.net/qq_52746299/article/details/132782386?spm=1001.2014.3001.5502)

[STM32学习笔记之EXTI应用实例：对射式红外传感器计次-CSDN博客](https://blog.csdn.net/qq_52746299/article/details/132788281)

[江协科技STM32——旋转编码器计次（软件消抖）_旋钮式音量编码器的去抖动-CSDN博客](https://blog.csdn.net/qq_63434393/article/details/132489786)

[STM32-外部中断详解_stm32外部中断-CSDN博客](https://blog.csdn.net/qq_44016222/article/details/123539693?ops_request_misc=%7B%22request%5Fid%22%3A%22170804481916800182750722%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=170804481916800182750722&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-123539693-null-null.142^v99^pc_search_result_base6&utm_term=外部中断&spm=1018.2226.3001.4187)

优先级一样且同时产生的中断，按照向量表顺序来处理中断

每个中断有16个优先级

优先级是在多个中断源同时申请，产生拥挤时才有作用，只有一个中断的情况下，优先级随便



1.先判断抢占优先级，高抢占优先级可以打断低抢占优先级的中断

2.如果抢占优先级相同，再判断响应优先级，高响应优先级不能打断低响应优先级

抢占和响应优先级都一样则哪个中断先发生，则执行哪个

抢占和响应优先级都一样前面讲的是按照中断地址表的顺序排，不是哪个先产生就先执行



void GPIO_EXTILineConfig( )这个函数可以配置AFIO的数据选择器，来选择我们想要的中断引脚