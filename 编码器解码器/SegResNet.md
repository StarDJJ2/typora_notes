PSNR / L :6.021229402683122,  SSIM / L :0.25111088544213317,  MSE / L :0.29076754977247427

learning_rate: 2e-4, train_batch_size: 32, val_batch_size: 32

```python
criterion = nn.L1Loss()
optimizer = optim.Adam(model.parameters(), lr=opt.Learning_Rate, weight_decay=1e-4)
```



PSNR / L :6.0337502501287155, SSIM / L :0.25689459980308715, MSE / L :0.28993440395172704

learning_rate: 1e-4, train_batch_size: 32, val_batch_size: 32   epoch: 75

```python
criterion = nn.L1Loss()
optimizer = optim.Adam(model.parameters(), lr=opt.Learning_Rate, weight_decay=1e-4)
```



<font color='red'>train，val和test所用的数据集都是不同的数据集，在收集时的图片指标可能都不相同。（将不同的数据集进行打乱然后重新划分成8:1:1）</font>



---------------------------------------------------------
PSNR / L :5.67268457292995, SSIM / L :0.2723872117674763, MSE / L :0.32031236003217456

learning_rate: 1e-4, train_batch_size: 32, val_batch_size: 32   epoch: 200     resolution：512*512

![image-20240421091814925](F:\Typora导出文件\编码器解码器\assets\image-20240421091814925.png)

PSNR / L :5.659331507605952, SSIM / L :0.2720825219979857, MSE / L :0.3212959661892375

learning_rate: 1e-4, train_batch_size: 32, val_batch_size: 32   epoch: 220     resolution：512*512



PSNR / L : , SSIM / L : , MSE / L : 

learning_rate: 1e-4, train_batch_size: 32, val_batch_size: 32   epoch: 200     resolution：256*256
