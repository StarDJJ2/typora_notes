# STLink V2 引脚作用

STLink V2 是用于 STM32 微控制器的调试和编程工具。它具有 20 个引脚，可连接到目标板的 JTAG 或 SWD 接口。以下是 STLink V2 上各个引脚的作用：

**1. VDD：** 3.3V 电源，为目标板供电。 **2. GND：** 地线。 **3. SWCLK：** 串行线时钟，用于 SWD 调试。 **4. SWDIO：** 串行数据输入/输出，用于 SWD 调试。 **5. NRST：** 复位信号，用于复位目标板。 **6. TCK：** JTAG 测试时钟，用于 JTAG 调试。 **7. TMS：** JTAG 测试模式选择，用于 JTAG 调试。 **8. TDO：** JTAG 测试数据输出，用于 JTAG 调试。 **9. TDI：** JTAG 测试数据输入，用于 JTAG 调试。 **10. VREF：** 参考电压，用于模拟调试。 **11. SWO：** 单线输出，用于调试输出。 **12. nTRST：** 异步复位，用于复位目标板。 **13. VCAP：** 3.3V 电源，用于为目标板的外部器件供电。 **14. GND：** 地线。 **15. BOOT0：** 引导模式选择，用于选择目标板的启动模式。 **16. BOOT1：** 引导模式选择，用于选择目标板的启动模式。 **17. Mass Storage：** 大容量存储，用于连接外部存储设备。 **18. USB +：** USB 数据线正极，用于连接到 PC。 **19. USB -：** USB 数据线负极，用于连接到 PC。 **20. GND：** 地线。

**以下是一些常见引脚的用途：**

- **VDD 和 GND：** 为目标板供电。
- **SWCLK 和 SWDIO：** 用于 SWD 调试。
- **NRST：** 复位目标板。
- **TCK、TMS、TDO 和 TDI：** 用于 JTAG 调试。
- **VREF：** 用于模拟调试。
- **SWO：** 用于调试输出。
- **nTRST：** 异步复位，用于复位目标板。
- **VCAP：** 为目标板的外部器件供电。
- **BOOT0 和 BOOT1：** 选择目标板的启动模式。
- **Mass Storage：** 连接外部存储设备。
- **USB + 和 USB -：** 连接到 PC。

**请注意，STLink V2 的引脚功能可能因版本而异。** 具体功能请参考 STLink V2 的用户手册。





# SWD调试

SWD调试，即串行线调试（Serial Wire Debug），是STM32微控制器支持的一种调试模式。它使用两根数据线（<font color='red'>SWDIO和SWCLK</font>）和一根电源线（VDD）进行调试，与传统的JTAG调试相比，具有以下优点：

- **引脚数少：**SWD调试只需要4根引脚，而JTAG调试需要20根引脚。
- **速度快：**SWD调试的速度比JTAG调试快。
- **功耗低：**SWD调试的功耗比JTAG调试低。

SWD调试使用了一种称为**串行协议**的通信方式来与目标板进行通信。串行协议由以下几种类型的命令组成：

- **读命令：**用于读取目标板的内存或寄存器。
- **写命令：**用于写入目标板的内存或寄存器。
- **控制命令：**用于控制目标板的运行，例如复位、启动、停止等。

SWD调试可以使用**调试器**进行。调试器是一种用于调试软件的工具，它可以连接到目标板，并使用SWD协议与目标板进行通信。

STM32CubeMX是一款STM32微控制器的开发工具，它支持SWD调试。在STM32CubeMX中，可以使用以下步骤进行SWD调试：

1. **选择调试模式：**在STM32CubeMX的“Project”设置中，选择“SWD”作为调试模式。
2. **连接调试器：**将调试器连接到目标板的SWD接口。
3. **启动调试：**在STM32CubeMX中，单击“Debug”按钮启动调试。

SWD调试可以帮助开发人员快速定位和解决软件问题，提高软件开发效率。

以下是一些SWD调试的常见应用场景：

- **调试应用程序：**SWD调试可以用于调试应用程序的代码，例如查找错误、分析程序运行状况等。
- **调试外设：**SWD调试可以用于调试外设的驱动程序，例如检查外设是否正常工作、配置外设参数等。
- **调试系统：**SWD调试可以用于调试系统的启动过程、运行状态等。