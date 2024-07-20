![image-20231101141151153](C:\Users\Starr Bruce\AppData\Roaming\Typora\typora-user-images\image-20231101141151153.png)

![image-20231101141157048](C:\Users\Starr Bruce\AppData\Roaming\Typora\typora-user-images\image-20231101141157048.png)

![image-20231101141205309](C:\Users\Starr Bruce\AppData\Roaming\Typora\typora-user-images\image-20231101141205309.png)

![image-20231101141210357](C:\Users\Starr Bruce\AppData\Roaming\Typora\typora-user-images\image-20231101141210357.png)

![image-20231101141218005](C:\Users\Starr Bruce\AppData\Roaming\Typora\typora-user-images\image-20231101141218005.png)





具体来说，假设$d$是两个特征向量之间的距离，相似度$S$可以通过下面的式子计算： $$ S = \frac{1}{1 + e^{d}} $$ 或者更常见的，为了确保当$d$增加时，$S$减少，我们会对$d$取负值，即： $$ S = \frac{1}{1 + e^{-d}} $$ 这样，当$d$很小（即两个特征向量非常相似）时，$e^{-d}$接近于0，$S$接近于1，表示高相似度。反之，当$d$很大时，$e^{-d}$会非常大，导致$S$接近于0，表示低相似度。这样的处理使得相似度的计算更加符合直觉。



抱歉，我的表述有误。你是正确的，当距离$d$增加时，相似度$S$应该接近于0而不是1。让我重新表述一下：

当我们使用sigmoid函数来将距离映射到相似度时，我们通常会先对距离进行一些转换，使得距离更大时，相似度更低。一个常见的做法是先对距离取负值，然后再应用sigmoid函数。

具体来说，假设$d$是两个特征向量之间的距离，相似度$S$可以通过下面的式子计算： $$ S = \frac{1}{1 + e^{-d}} $$

这样，当$d$很小（即两个特征向量非常相似）时，$e^{-d}$接近于0，$S$接近于1，表示高相似度。反之，当$d$很大时，$e^{-d}$会非常大，导致$S$接近于0，表示低相似度。这样的处理使得相似度的计算更加符合直觉。感谢你的指正！







1.得到特征差

2.再通过全连接层回归到一维的输出，这个输出也会受到损失函数的影响，因此越相似输出向量越大，反之则越小

3.使用sigmoid函数进行归一化