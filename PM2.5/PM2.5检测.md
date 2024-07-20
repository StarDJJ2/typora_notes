# 多模态融合方法

多模态深度学习在计算机视觉的许多领域得到了广泛的应用。现有的融合方法可分为信号级融合、特征级融合和评分级融合模型

信号级融合、特征级融合和分数级融合是指在多模态（例如语音、图像、文本等）信息处理中，将来自不同模态的信息进行融合以提高综合性能的方法。

## 信号级融合

信号级融合是指将来自不同传感器或模态的原始信号进行融合。例如，在人脸识别任务中，可以使用RGB相机捕获的图像和深度相机捕获的深度信息，通过信号级融合将两种类型的数据进行融合，得到更准确的人脸识别结果。

## 特征级融合

特征级融合是指将不同模态的特征进行融合。例如，在情感识别任务中，可以将从文本和语音中提取的不同特征进行融合，得到更准确的情感分类结果。

## 分数级融合

分数级融合是指将来自不同模态的分类概率进行融合。例如，在多模态的情感识别任务中，可以将从文本和语音中分别得到的情感分类概率进行加权平均，得到最终的情感分类结果。

这三种融合模型各有优缺点，具体应用需要根据实际情况进行选择。例如，在某些任务中，信号级融合可能比特征级融合更高效，但在其他任务中，特征级融合可能表现更好。



# PM2.5对图像的影响

PM2.5在影响图像结构和颜色信息的同时，也会影响图像的深度信息



# 卷积层输出特征图的两个可视化怎么做？



## RGB和IR卷积层输出特征



## Add和concat操作的去区别

add操作经典代表网络是ResNet,concat操作经典代表网络是Inception系统网络中的Inception结构和DenseNet。

正如之前的回答有人说的，add操作相当于加入一种先验知识。我觉得也就是相当于你对原始特征进行人为的特征融合。而你选择的特征处理的操作是element-wise add。通过add操作，会得到新的特征，这个新的特征可以反映原始特征的一些特性，但是原始特征的一些信息也会在这个过程中损失。

但是concate就是将原始特征直接拼接，让网络去学习，应该如何融合特征，这个过程中信息不会损失。

所以我认为add其实只是concate的一种特殊情况。但是concate带来的计算量较大，在明确原始特征的关系可以使用add操作融合的话，使用add操作可以节省计算代价。


# 全局平均池化层

![img](https://img-blog.csdn.net/20180530220844573?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTQyNjQzNzM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)



# 我现在有一组图像，一张是有空气污染的图像，一张是没有空气污染的图像，如何得到两张图像的HSV相关值？

处理图像数据通常使用的Python库是OpenCV。你可以使用它来加载图像，然后将这些图像从RGB颜色空间转换到HSV颜色空间，然后分别提取出这两幅图像的HSV值。以下是一个例子：

```python
import cv2
import numpy as np

# 加载图像
image1 = cv2.imread('polluted_image.jpg')  # 替换为你的图像路径
image2 = cv2.imread('clean_image.jpg')  # 替换为你的图像路径

# 转换颜色空间到HSV
hsv_image1 = cv2.cvtColor(image1, cv2.COLOR_BGR2HSV)
hsv_image2 = cv2.cvtColor(image2, cv2.COLOR_BGR2HSV)

# 提取HSV值。hsv_image[:,:,i]获取第i通道（H=0, S=1, V=2）的值
h1, s1, v1 = np.mean(hsv_image1[:,:,0]), np.mean(hsv_image1[:,:,1]), np.mean(hsv_image1[:,:,2])
h2, s2, v2 = np.mean(hsv_image2[:,:,0]), np.mean(hsv_image2[:,:,1]), np.mean(hsv_image2[:,:,2])

print("Polluted Image HSV Values: H: {}, S: {}, V: {}".format(h1, s1, v1))
print("Clean Image HSV Values: H: {}, S: {}, V: {}".format(h2, s2, v2))
```

这段代码会输出两幅图像的平均的HSV值。请注意将'polluted_image.jpg'和'clean_image.jpg'替换为你真正的图像文件路径。

要抽取每个像素的HSV值，你可以直接使用`hsv_image1`和`hsv_image2`变量，这两个变量是NumPy数组，其中包含了图像的所有像素的HSV值。

需要说明的是，OpenCV默认读取图像的颜色空间为BGR而不是通常我们所说的RGB，所以在转换到HSV的时候我们用的是`cv2.COLOR_BGR2HSV`。

# 计算机视觉中的视觉特征主要描述图像的颜色、形状、纹理等底层信息

收集数据方法：一个地方测六组，每组10分钟。

收数据集的地点:

1.18号楼4楼阳台

2.18号楼2楼平台

3.18号楼对面新大楼2楼和五楼平台

4.18号楼顶楼

5.
