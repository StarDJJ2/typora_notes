# InceptionV3中不同的Inception模块各有什么区别

InceptionV3中主要包含了三种类型的Inception模块：Inception模块A、Inception模块B和Inception模块C。 每种Inception模块都有其特点，并且在网络的不同位置起到不同的作用： 

1. Inception模块A：主要处理较小空间尺寸的特征图，但使用多种不同尺寸的卷积核进行卷积运算，再将结果合并，以此增加了网络对尺寸变化的适应性。    
2. Inception模块B：主要进行低维度的嵌入，以减少计算压力，使网络能处理更大尺寸的特征图。在Inception模块B中，主要利用了1x7和7x1的卷积核代替了7x7的卷积核，减少了参数量和计算量。 
3. Inception模块C：主要用于对高维度的特征进行分解并且增强模型对大尺寸对象的检测能力。Inception模块C中，主要使用了1x3和3x1的卷积核代替了3x3的卷积核，进一步减少了参数量和计算压力。 

通过Inception模块的设计，InceptionV3旨在提供多尺度特征提取能力，增强模型对输入空间和通道（特征）空间的抽象能力，同时降低计算复杂度。

