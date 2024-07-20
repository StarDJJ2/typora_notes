模型：Dehazeformer-s

![image-20240410202523523](F:\Typora导出文件\编码器解码器\assets\image-20240410202523523.png)



1.3×3Conv在PatchEmbed类中

2.







训练60epoch结果图：![image-20240405080944274](F:\Typora导出文件\编码器解码器\assets\image-20240405080944274.png)





# config：

## 1.

```
{
    "batch_size": 32,
    "patch_size": 256,
    "valid_mode": "valid",
    "edge_decay": 0,
    "only_h_flip": true,
    "optimizer": "adamw",
    "lr": 2e-4,
    "epochs":60,
    "eval_freq": 1
}
```

评价指标：

the_best_weights:

(R^2 Score): 0.17504798039758218

(MAE Score): 52.64473357518514

(MSE Score): 79.92402471593407

PLCC: 0.5124179986048417
SROCC: 0.6306797189162161
KROCC: 0.45162528448443934



epoch:60

the_last_weights:


Test Accuracy (R^2 Score): 0.4694905148632331

Test Accuracy (MAE Score): 40.68990782419841

Test Accuracy (MSE Score): 64.09284901298076

PLCC: 0.7074112253323621
SROCC: 0.7560104730644097
KROCC: 0.5642608470417096





直接使用encoder层进行回归任务试试，对比一下没有去雾权重参数的回归预测结果

结果：

评价指标：

epoch:

the_last_weights:

Test Accuracy (R^2 Score): 0.432800424331215

Test Accuracy (MAE Score): 44.0864751080672

Test Accuracy (MSE Score): 66.27213303625078

PLCC: 0.6679427963697674
SROCC: 0.7179560159308775
KROCC: 0.527437682359525







训练100epoch：

![image-20240423095729592](F:\Typora导出文件\编码器解码器\assets\image-20240423095729592.png)



Epoch 150/150, Train Loss: 34.7253, Valid Loss: 33.2064

![image-20240423094614128](F:\Typora导出文件\编码器解码器\assets\image-20240423094614128.png)



the best_weights:

Test Accuracy (R^2 Score): 0.5176454706604892
Test Accuracy (MAE Score): 39.22047842025757
Test Accuracy (MSE Score): 61.11476988538324
PLCC: 0.7367700963465567
SROCC: 0.7902096936060963
KROCC: 0.5953078290286495



the last_weights:
Test Accuracy (R^2 Score): 0.5220316534769681
Test Accuracy (MAE Score): 39.01058677037557
Test Accuracy (MSE Score): 60.83626858518292
PLCC: 0.7368336854271457
SROCC: 0.7893276837585153
KROCC: 0.5953078290286495



训练150epoch：

![image-20240423143243346](F:\Typora导出文件\编码器解码器\assets\image-20240423143243346.png)



Epoch 300/300, Train Loss: 29.2220, Valid Loss: 36.2907

![image-20240423152933833](F:\Typora导出文件\编码器解码器\assets\image-20240423152933833.png)

the best_weights:
Test Accuracy (R^2 Score): 0.4886231536246888
Test Accuracy (MAE Score): 41.43081386089325
Test Accuracy (MSE Score): 62.92649332189672
PLCC: 0.7328854769645283
SROCC: 0.760662363712135
KROCC: 0.5657048927155207



the last_weights:
Test Accuracy (R^2 Score): 0.5078946626439682
Test Accuracy (MAE Score): 41.11674892425537
Test Accuracy (MSE Score): 61.72939749522198
PLCC: 0.72232199267591
SROCC: 0.7512020967985654
KROCC: 0.5577626415095595



训练200epoch：

![image-20240424083512934](F:\Typora导出文件\编码器解码器\assets\image-20240424083512934.png)

Epoch：300

<img src="F:\Typora导出文件\编码器解码器\assets\image-20240424093235478.png" alt="image-20240424093235478" style="zoom: 50%;" />



the best_weights:
Test Accuracy (R^2 Score): 0.4956022988882781
Test Accuracy (MAE Score): 39.83466920018196
Test Accuracy (MSE Score): 62.49561550074874
PLCC: 0.7263514125037229
SROCC: 0.7501778272981486
KROCC: 0.5563185958357483



the last_weights:

Test Accuracy (R^2 Score): 0.542368495026972
Test Accuracy (MAE Score): 40.24162254810333
Test Accuracy (MSE Score): 59.52795428137603
PLCC: 0.7502852623393166
SROCC: 0.7608330752955378
KROCC: 0.5620947785309929





载入dehazeformer-s-source的权重，  在全连接层后添加Dropout层  

Epoch：300

![image-20240425163834007](F:\Typora导出文件\编码器解码器\assets\image-20240425163834007.png)

the best_weights:

Test Accuracy (R^2 Score): 0.4767843202303492
Test Accuracy (MAE Score): 39.161524005730946
Test Accuracy (MSE Score): 61.86352802884219
PLCC: 0.756450529982759
SROCC: 0.805104279257987
KROCC: 0.6162464912989112

the last_weights:
Test Accuracy (R^2 Score): 0.31452183267517064
Test Accuracy (MAE Score): 50.03447410662969
Test Accuracy (MSE Score): 70.89050126726005
PLCC: 0.7188033350142673
SROCC: 0.700216237222274
KROCC: 0.5324918422178642





载入dehazeformer-s-source的权重，  在全连接层后添加Dropout层， 冻结全连接层以外的参数 

epoch100：

![image-20240425165322359](F:\Typora导出文件\编码器解码器\assets\image-20240425165322359.png)

the best_weights:
Test Accuracy (R^2 Score): 0.006287714294922697
Test Accuracy (MAE Score): 54.04713557680448
Test Accuracy (MSE Score): 86.82708317557811
PLCC: 0.39813474634365537
SROCC: 0.5437875229642108
KROCC: 0.3916973890212764



the last_weights:
Test Accuracy (R^2 Score): 0.28342118323816345
Test Accuracy (MAE Score): 47.68276307543119
Test Accuracy (MSE Score): 73.60931946189434
PLCC: 0.5804726162677347
SROCC: 0.669559282036195
KROCC: 0.4805061979606625





载入dehazeformer-s-source的权重，  在全连接层后添加Dropout层  seed=12

epoch100：

the best_weights:

Test Accuracy (R^2 Score): 0.5352275629055925
Test Accuracy (MAE Score): 36.53682093938192
Test Accuracy (MSE Score): 57.05753581848482
PLCC: 0.7915036054025782
SROCC: 0.8240959429115442
KROCC: 0.6379071764060786



the last_weights:

Test Accuracy (R^2 Score): 0.5352275629055925
Test Accuracy (MAE Score): 36.53682093938192
Test Accuracy (MSE Score): 57.05753581848482
PLCC: 0.7915036054025782
SROCC: 0.8240959429115442
KROCC: 0.6379071764060786



epoch150：

the best_weights:
Test Accuracy (R^2 Score): 0.5276487571131947
Test Accuracy (MAE Score): 37.74365908940633
Test Accuracy (MSE Score): 59.53372793004597
PLCC: 0.7957024575722453
SROCC: 0.8321478392620411
KROCC: 0.6537916788180014



the last_weights:
Test Accuracy (R^2 Score): 0.549016930885428
Test Accuracy (MAE Score): 36.256893215179446
Test Accuracy (MSE Score): 58.19751866253171
PLCC: 0.8019353834291495
SROCC: 0.8281361170520762
KROCC: 0.6465714504489456



epoch200：

the best_weights:
Test Accuracy (R^2 Score): 0.557456825955063
Test Accuracy (MAE Score): 36.09512476285299
Test Accuracy (MSE Score): 57.611333169197756
PLCC: 0.8045905250007924
SROCC: 0.8293880019970297
KROCC: 0.64584942761204



the last_weights:

Test Accuracy (R^2 Score): 0.557456825955063
Test Accuracy (MAE Score): 36.09512476285299
Test Accuracy (MSE Score): 57.611333169197756
PLCC: 0.8045905250007924
SROCC: 0.8293880019970297
KROCC: 0.64584942761204





载入dehazeformer-s-source的权重，  在全连接层后添加Dropout层  seed=13

![image-20240425210242783](F:\Typora导出文件\编码器解码器\assets\image-20240425210242783.png)

the best_weights:
Test Accuracy (R^2 Score): 0.3483078871871176
Test Accuracy (MAE Score): 47.40434485912323
Test Accuracy (MSE Score): 71.64124743592193
PLCC: 0.7358265098876251
SROCC: 0.70347398327221
KROCC: 0.5339358878916753



the last_weights:
Test Accuracy (R^2 Score): 0.3842606537796477
Test Accuracy (MAE Score): 45.016321020523705
Test Accuracy (MSE Score): 69.68900716106306
PLCC: 0.7357878028226229
SROCC: 0.7150965969088815
KROCC: 0.544766230445259



载入dehazeformer-s-source的权重，  在全连接层后添加Dropout层  MSELoss()   lr == 1e-4 

<img src="F:\Typora导出文件\编码器解码器\assets\image-20240426142815343.png" alt="image-20240426142815343" style="zoom:50%;" />



the best_weights:
Test Accuracy (R^2 Score): 0.5978082074940485
Test Accuracy (MAE Score): 35.439086011250815
Test Accuracy (MSE Score): 51.90532948082933
PLCC: 0.8151160335822953
SROCC: 0.8227160242790384
KROCC: 0.6256327881786838



the last_weights:
Test Accuracy (R^2 Score): 0.6277721516444441
Test Accuracy (MAE Score): 36.056195894082386
Test Accuracy (MSE Score): 50.263905330140446
PLCC: 0.826037142525525
SROCC: 0.8292315163789105
KROCC: 0.6191345826465336



载入dehazeformer-s-source的权重，  在全连接层后添加Dropout层  MSELoss()   lr == 2e-5

<img src="F:\Typora导出文件\编码器解码器\assets\image-20240426151331872.png" alt="image-20240426151331872" style="zoom:50%;" />



the last_weights:
Test Accuracy (R^2 Score): 0.5437127839823148
Test Accuracy (MAE Score): 38.3973184967041
Test Accuracy (MSE Score): 56.61213728659927
PLCC: 0.7764210037550758
SROCC: 0.7830824849990309
KROCC: 0.5902536691703104



the best_weights:

Test Accuracy (R^2 Score): 0.5732853545637185
Test Accuracy (MAE Score): 38.9241599782308
Test Accuracy (MSE Score): 55.305638744889634
PLCC: 0.7789885394277646
SROCC: 0.8000540615823221
KROCC: 0.599639966050083



载入dehazeformer-s-source的权重，  在全连接层后添加Dropout层  MSELoss()   lr == 2e-4

<img src="F:\Typora导出文件\编码器解码器\assets\image-20240426153102850.png" alt="image-20240426153102850" style="zoom:50%;" />

the last_weights:
Test Accuracy (R^2 Score): 0.6297518073987709
Test Accuracy (MAE Score): 36.62980292081833
Test Accuracy (MSE Score): 51.55617032184647
PLCC: 0.8223852799734619
SROCC: 0.8342106042281577
KROCC: 0.6328530165477396



the best_weights:

Test Accuracy (R^2 Score): 0.5786242974282545
Test Accuracy (MAE Score): 37.64523483276367
Test Accuracy (MSE Score): 54.68019160670617
PLCC: 0.7884200115227712
SROCC: 0.7868381398338916
KROCC: 0.5837554636381602



载入dehazeformer-s-source的权重，  在全连接层后添加Dropout层  MSELoss()   lr == 3e-4

<img src="F:\Typora导出文件\编码器解码器\assets\image-20240426212929664.png" alt="image-20240426212929664" style="zoom:50%;" />

the best_weights:
Test Accuracy (R^2 Score): 0.6358946393122227
Test Accuracy (MAE Score): 32.116754926045736
Test Accuracy (MSE Score): 50.908139086430054
PLCC: 0.8198770806322455
SROCC: 0.849844940074794
KROCC: 0.6754523639251687