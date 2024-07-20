# 1.主要模数转换器类型

[模数转换器(ADC)的几种主要类型简介_模数转换adc有几种类型-CSDN博客](https://blog.csdn.net/whereismatrix/article/details/81814431)

[STM32学习之ADC（模拟数字转换器）_stm32 adc-CSDN博客](https://blog.csdn.net/weixin_58716963/article/details/126637018?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-126637018-blog-81814431.235^v43^pc_blog_bottom_relevance_base5&spm=1001.2101.3001.4242.1&utm_relevant_index=3)

## 1.1.逐次逼近型

[逐次逼近ADC – 模数转换器工作原理 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/664348480)

逐次逼近型ADC是应用非常广泛的模/数转换方法，它包括1个比较器、1个数模转换器、1个逐次逼近寄存器（SAR）和1个逻辑控制单元

# 2.ADC校准

STM32 ADC的校准过程包括以下两个步骤：

1. **复位校准寄存器**：将校准寄存器中的值清零。
2. **开始校准程序**：ADC会自动进行校准，并更新校准寄存器中的值。



在STM32中，ADC的校准寄存器是一个**位标志寄存器**，其位0用于指示ADC的校准状态。

- **当位0为0时**，表示ADC正在进行校准，不能对ADC进行任何操作。
- **当位0为1时**，表示ADC校准完成，可以对ADC进行操作。

因此，**while循环的判断条件是ADC_GetResetCalibrationStatus(ADC1) == SET**，是为了确保ADC校准完成，然后再进行下一步操作。

**以下是一些可能的下一步操作：**

- **开始ADC转换**
- **读取ADC转换结果**
- **配置ADC参数**

如果在ADC校准完成之前进行这些操作，可能会导致ADC工作异常。

**总结**

**while循环的判断条件是ADC_GetResetCalibrationStatus(ADC1) == SET**，是为了确保ADC校准完成，然后再进行下一步操作，避免ADC工作异常。



显示的ADC数值末尾有抖动，是正常的输出波动



# ADC数据右对齐和左对齐

[ADC数据存储：左对齐和右对齐 | 风逍遥 (hyxhe.com)](https://www.hyxhe.com/archives/a1f79e07.html)