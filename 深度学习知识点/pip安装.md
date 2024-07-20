[python pip 换国内源的办法（永久和临时两种办法）_pip换源-CSDN博客](https://blog.csdn.net/skyyzq/article/details/113417832)



pip install -i https://pypi.tuna.tsinghua.edu.cn/simple scikit-image   暂时更换为清华源安装scikit-image包



pip install -i https://pypi.tuna.tsinghua.edu.cn/simple tqdm==4.32.2

pip install -i https://pypi.tuna.tsinghua.edu.cn/simple tensorboard==1.14.0

pip install -i https://pypi.tuna.tsinghua.edu.cn/simple thop



```python
import numpy as np

import torch

#假设label是某个NumPy数组

#使用astype确保数组的类型是int64，这是PyTorch支持的类型之一

label = np.array(label, dtype=np.int32).astype(np.int64)  
#从int32转换为int64

label_tensor = torch.from_numpy(label).long()  # 转换为torch.LongTensor\n`


```

