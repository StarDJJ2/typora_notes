# 1.ResNet34

![bandicam 2023-06-10 09-42-30-747](C:\Users\25075\Pictures\AQI-Prediction\bandicam 2023-06-10 09-42-30-747.png)

# 2.ResNet18预测结果

## 1.学习率=0.001

![image-20230704093505057](C:\Users\25075\AppData\Roaming\Typora\typora-user-images\image-20230704093505057.png)

## 2.学习率=0.003

![image-20230704101145027](C:\Users\25075\AppData\Roaming\Typora\typora-user-images\image-20230704101145027.png)

## 3.学习率0.01



## 4.学习率0.03

![image-20230704102244711](C:\Users\25075\AppData\Roaming\Typora\typora-user-images\image-20230704102244711.png)





## 5.将Adam改成SGD

Loss的输出值全为nan

# 3.ResNet34

## 1.未加Normalize预测结果

![image-20230704093623551](C:\Users\25075\AppData\Roaming\Typora\typora-user-images\image-20230704093623551.png)

## 2.加Normalize预测结果第一次

![image-20230704094909426](C:\Users\25075\AppData\Roaming\Typora\typora-user-images\image-20230704094909426.png)

## 3.加Normalize预测结果第二次

![image-20230704101036993](C:\Users\25075\AppData\Roaming\Typora\typora-user-images\image-20230704101036993.png)

# 4.回归预测评价指标

1.r2_score

2.f1_score    这是分类评价指标
