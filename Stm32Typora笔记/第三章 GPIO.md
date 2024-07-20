# 1.输出模式

输入可以忍受5V的高点平，但是输出最大就只能是3.3V

每个GPIO外设共有16个引脚，编号0-15

寄存器是32位，而引脚只有16位，因此只有低16位是每一位对应一个引脚



## 1.保护二极管

如果输入电压比上方的3.3V要高，那么上方的二极管就会导通，输入电压产生的电流就会直接流入VDD而不会流入内部电路，可以避免过高的电压对内部这些电路产生伤害

如果输入电压比0V还要低，这个电压是相对于VSS的电压，所以是可以有负电压的。这是下方的二极管就会导通，电流会从VSS直接流出去。

如果输入电压在0-3.3V之间，这时二极管对电路没有影响，这就是保护二极管的用途



施密特触发器：对输入电压进行整形
如果输入电压大于某一阈值，输出就会瞬间升为高电平

如果输入电压小于某一阈值，输出就会瞬间降为低电平

只有低于下限和高于上限，输出才会变化。中间留有一定范围，可以有效避免因信号波动造成的输出抖动现象



MOS管就是一种电子开关

数据寄存器1时，N-MOS断开，高阻模式，可外接上拉电阻5V输出；**数据寄存器为0**，下管导通，接VSS，输出低电平，低电平有驱动能力，高电平没有，可作为**通讯协议的驱动方式（I2C通讯引脚）**。推挽输出也叫强推模式P-MOS高电平，开漏输出N-MOS低电平输出



[STM32 GPIO八种输入输出模式 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/113367004)

## 2.浮空/上拉/下拉输入

可以容忍5V的引脚，它的上方保护二极管要做一下处理，不然直接接VDD3.3V的话，外部在接入5V电压就会导致上边二极管开启，并且产生较大电流，不太妥当。



![image-20240209104535335](C:\Users\25075\AppData\Roaming\Typora\typora-user-images\image-20240209104535335.png)

低电平驱动电路(MCU中一般使用这种方式)

左边为低电平0V，则会与3.3V形成电压差，LED点亮，
左边为高电平3.3V，没有电压差，LED熄灭
限流电阻要接，一方面防止LED因电流过大而损坏，另一方面也可以调节LED的亮度（增大阻值）

![image-20240209105200354](C:\Users\25075\AppData\Roaming\Typora\typora-user-images\image-20240209105200354.png)

高电平驱动电路（高电平驱动能力弱，就不使用该方法）

高电平点亮，低电平熄灭



操作STM32的GPIO总共需要3个步骤：

1.使用RCC开启GPIO的时钟

2.使用GPIO——Init函数初始化GPIO

3.使用输出或者输入的函数控制GPIO口



多选引脚为什么是或？

将十六进制表示转换为二进制，然后使用按位或，

0001,0010,0100按位或得到0111，得以选中三个引脚



`GPIO_SetBits`函数的功能是设置指定GPIO（通用输入/输出）的特定输出位。 

具体的实现语义就是将指定的GPIO的一些特定bit设置为“高”电平状态。



ODR就是GPIOA16个叫输出值的寄存器



GPIO_Speed是GPIO的输出速度，在输入模式下没用

GPIO——ReadInputData：读取整个输入数据寄存器

GPIO——ReadInputDataBit：读取这里输入数据寄存器的某一位

GPIO——ReadOutputDataBit：读取这里输出数据寄存器的某一位

GPIO——ReadOutputData：读取整个输出数据寄存器



# LED初始化

推挽输出电路的功耗较低，效率较高。

**具体来说，对于LED灯，其工作原理是利用电流来发光的。当LED灯接通电源时，电流会从电源流过LED灯，从而使LED灯发光。因此，对于LED灯，需要使用具有较强驱动能力的输出模式来驱动它。推挽输出模式正好满足这一要求。**

此外，LED灯的正向压降一般为2V左右，而STM32的GPIO口的输出电压为3.3V。因此，在使用推挽输出模式驱动LED灯时，需要在LED灯的阳极和电源之间接一个限流电阻，以防止LED灯被烧坏。



# 按键初始化

[STM32怎么判断按键是不是低电平有效] https://blog.csdn.net/Romeo_tune/article/details/124145131

[关于STM32按键实验中连接按键的GPIO管脚是配置为上拉输入还是下拉输入的理解] https://blog.csdn.net/xuw_xy/article/details/95514042



# 上拉电阻和下拉电阻

[电路中上拉、下拉电阻的作用及原理 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/258321463#:~:text=简单来说，电源到,该引脚为低电平。)

上拉电阻的作用：辅助浮空状态输出高电平



# 标准库函数

## GPIO_WriteBit和GPIO_Write两个函数有什么区别，各自使用在什么情况下？

STM32标准库中的GPIO_WriteBit和GPIO_Write函数都是用于写入GPIO端口数据的函数，但它们之间存在一些区别：

**GPIO_WriteBit**

- **功能：**设置或清零指定的GPIO端口位。
- 参数：
  - GPIOx：要操作的GPIO端口。
  - GPIO_Pin：要操作的GPIO端口位。
  - BitVal：要设置的值，可以是GPIO_PIN_SET或GPIO_PIN_RESET。
- **返回值：**无。
- 使用场景：
  - 只需要设置或清零单个GPIO端口位时。
  - 需要在中断服务程序中快速设置或清零GPIO端口位时。

**GPIO_Write**

- **功能：**写入指定的GPIO端口数据。
- 参数：
  - GPIOx：要操作的GPIO端口。
  - PortData：要写入的端口数据，范围为0x00到0xFFFF。
- **返回值：**无。
- 使用场景：
  - 需要同时设置或清零多个GPIO端口位时。
  - 需要写入的数据不是单个端口位时。

**总结**

- **GPIO_WriteBit**用于设置或清零指定的GPIO端口位，**GPIO_Write**用于写入指定的GPIO端口数据。
- **GPIO_WriteBit**只适用于单个端口位，**GPIO_Write**可以同时适用于多个端口位。
- **GPIO_WriteBit**的速度通常比**GPIO_Write**快。

**示例**

以下是一个对端口位进行写操作，支持BIT_SET/BIT_RESET，写1或写0，可以选同端口多位

```c
GPIO_WriteBit(GPIOA, GPIO_Pin_1 | GPIO_Pin_2, BIT_SET);
```

以下是对整个端口直接进行写操作，0XFFFF代表16位全部写入1

```c
GPIO_Write(GPIOA, 0XFFFF);
```

**注意**

- 使用GPIO_WriteBit和GPIO_Write函数时，需要确保GPIO端口已经配置为<font color='red'>输出模式</font>。
- 使用GPIO_WriteBit函数时，BitVal参数只能是GPIO_PIN_SET或GPIO_PIN_RESET。



## GPIO_ReadOutputDataBit和GPIO_ReadOutputData函数的区别主要在哪里呢？

STM32标准库中的GPIO_ReadOutputDataBit和GPIO_ReadOutputData函数都是用于读取GPIO端口输出数据的函数，但它们之间存在一些区别：

**GPIO_ReadOutputDataBit**

- **功能：**读取指定的GPIO端口位输出电平。
- 参数：
  - GPIOx：要操作的GPIO端口。
  - GPIO_Pin：要操作的GPIO端口位。
- 返回值：
  - GPIO_PIN_SET：如果指定的GPIO端口位输出电平为高电平。
  - GPIO_PIN_RESET：如果指定的GPIO端口位输出电平为低电平。
- 使用场景：
  - 只需要读取单个GPIO端口位输出电平时。
  - 需要在中断服务程序中快速读取GPIO端口位输出电平时。

**GPIO_ReadOutputData**

- **功能：**读取指定的GPIO端口输出数据。
- 参数：
  - GPIOx：要操作的GPIO端口。
- 返回值：
  - 读取到的GPIO端口输出数据，范围为0x00到0xFFFF。
- 使用场景：
  - 需要同时读取多个GPIO端口位输出电平时。
  - 需要读取的数据不是单个端口位时。

**总结**

- **GPIO_ReadOutputDataBit**用于读取指定的GPIO端口位输出电平，**GPIO_ReadOutputData**用于读取指定的GPIO端口输出数据。
- **GPIO_ReadOutputDataBit**只适用于单个端口位，**GPIO_ReadOutputData**可以同时适用于多个端口位。
- **GPIO_ReadOutputDataBit**的速度通常比**GPIO_ReadOutputData**快。

**示例**

以下是一个使用GPIO_ReadOutputDataBit读取GPIO端口位12输出电平的示例：

C

```
uint8_t pin_level = GPIO_ReadOutputDataBit(GPIOA, GPIO_PIN_12);
```

以下是一个使用GPIO_ReadOutputData读取GPIO端口A输出数据的示例：

C

```
uint16_t port_data = GPIO_ReadOutputData(GPIOA);
```

**注意**

- 使用GPIO_ReadOutputDataBit和GPIO_ReadOutputData函数时，需要确保GPIO端口已经配置为输出模式。
