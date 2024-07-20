# 1.导入库

import torch.distributed as dist 

from torch.nn.parallel import DistributedDataParallel as DDP

# 2.相关参数

group，进程组。默认情况下只有一个组，

world size: 全局的并行数，

torch.distributed.get_world_size()

rank: 表示当前进程的序号，用于进程间通讯。从0开始，rank=0的进程是master进程

torch.distributed.get_rank()

local_rank: 每台机子上的进程的序号。

比方说， `rank=3`，`local_rank=0` 表示第 3 个进程内的第 1 块 GPU。

一般情况下，用local_rank来手动设置模型是跑在当前机器的哪块GPU上。

torch.distributed.local_rank()

# 3.具体步骤

1.在使用 distributed 包前，用 init_process_group 初始化进程组，同时初始化 distributed 包;

2.如果需要进行小组内集体通信，用 new_group 创建子分组;

3.创建分布式并行模型 DDP(model, device_ids=device_ids);

4.为数据集创建 Sampler;

5.使用启动工具 torch.distributed.launch 在每个主机上执行一次脚本，开始训练;

6.使用 destory_process_group() 销毁进程组;

# 4.mp.spawn（）

`mp.spawn(fn, args, nprocs, join, daemon)`函数：

> - fn：派生程序入口；
> - nprocs: 派生进程个数；
> - join: 是否加入同一进程池；
> - daemon：是否创建守护进程；

![图片1-removebg-preview](E:\chrome下载内容\图片1-removebg-preview.png)