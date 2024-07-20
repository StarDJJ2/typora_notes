# 1.AlexNet + SVR

首先，使用PyTorch搭建一个AlexNet网络模型，然后定义一个自定义的模型，其中包含AlexNet和SKLearn的支持向量机回归（SVR）。

注意：PyTorch不能直接整合SKLearn中的SVR，因此需要在训练和推理阶段分别处理AlexNet输出的特征和SVR模型。

这里是一个示例：

```python
import torch
import torch.nn as nn
import torchvision.models as models
from sklearn.svm import SVR
from torch.autograd import Variable
import numpy as np

# 加载预训练的AlexNet模型
alexnet = models.alexnet(pretrained=True)

# 删除AlexNet最后一层全连接（分类）层
features_extractor = nn.Sequential(*(list(alexnet.children())[:-1]))

# 定义带AlexNet特征提取和SVR回归器的自定义模型
class CustomModel:
    def __init__(self, features_extractor, svr):
        self.features_extractor = features_extractor
        self.svr = svr

    def fit(self, X, y):
        # 从AlexNet模型中提取特征
        features = self.features_extractor(X)
        features = features.view(features.size(0), -1).detach().numpy()
        
        # 使用提取的特征训练SVR模型
        self.svr.fit(features, y)

    def predict(self, X):
        # 从AlexNet模型中提取特征
        features = self.features_extractor(X)
        features = features.view(features.size(0), -1).detach().numpy()
        
        # 使用SVR模型进行预测
        return self.svr.predict(features)

# 创建SVR实例
svr = SVR(kernel='linear')

# 创建自定义模型实例
custom_model = CustomModel(features_extractor, svr)

# 用法示例：训练和预测
# 假设train_data是一个已准备好的训练数据张量，train_labels是对应的标签
train_data = torch.randn(100, 3, 224, 224)
train_labels = np.random.rand(100)

# 将输入数据转化为PyTorch变量，进行训练
inputs = Variable(train_data)
custom_model.fit(inputs, train_labels)

# 使用相同的数据进行预测
predictions = custom_model.predict(inputs)
print(predictions)
```

这个示例展示了如何创建一个自定义模型`CustomModel`，它结合了AlexNet（作为特征提取器）和一个SVR回归器。请注意，你需要根据你的实际任务和数据准备`train_data`和`train_labels`。训练和预测示例部分仅作为如何使用自定义模型的演示。在实际情况中，你需要将训练数据输入到`fit`方法，然后使用测试数据进行预测。

# 2.

你的需求有点特殊，因为通常我们不会将深度学习模型和传统的机器学习模型（如SVR）混合使用。但是，如果你确实想这样做，你可以将AlexNet的最后一个全连接层的输出特征数改为1，然后使用这个特征作为SVR的输入。

首先，定义一个AlexNet模型，并修改最后的全连接层的输出特征为1：

```python
import torch
import torch.nn as nn
from torchvision.models import alexnet

class ModifiedAlexNet(nn.Module):
    def __init__(self):
        super(ModifiedAlexNet, self).__init__()
        self.features = alexnet(pretrained=True).features
        self.avgpool = alexnet(pretrained=True).avgpool
        self.classifier = nn.Sequential(*list(alexnet(pretrained=True).classifier.children())[:-1])
        self.classifier[6] = nn.Linear(4096, 1)

    def forward(self, x):
        x = self.features(x)
        x = self.avgpool(x)
        x = torch.flatten(x, 1)
        x = self.classifier(x)
        return x
```

然后，你需要单独训练一个SVR模型，将AlexNet的输出作为输入特征。你需要用到`sklearn.svm.SVR`，但是注意，你需要将每一批的Tensor数据转换为numpy数组，然后再输入到SVR模型中。

```python
from sklearn.svm import SVR

# 假设我们的数据集是dataset，数据加载器是dataloader
model = ModifiedAlexNet()
model = model.to(device)
optimizer = torch.optim.SGD(model.parameters(), lr=0.001, momentum=0.9)
loss_fn = nn.MSELoss()

for epoch in range(num_epochs): # num_epochs是你设定的训练轮数
    for inputs, targets in dataloader:
        inputs = inputs.to(device)
        targets = targets.to(device)

        optimizer.zero_grad()
        outputs = model(inputs)
        loss = loss_fn(outputs, targets)
        loss.backward()
        optimizer.step()

        outputs = outputs.detach().cpu().numpy()
        targets = targets.detach().cpu().numpy()

        svr = SVR()
        svr.fit(outputs, targets)
```

注意，这个设置非常特殊，可能需要对数据进行一些特殊的预处理，例如归一化，以便让SVR能够有效地处理AlexNet的输出。同时，因为SVR是一个和数据规模相关的计算复杂度比较高的模型，所以在大规模数据上可能会遇到性能问题。

# 3.

在你的要求中有一点需要先澄清：PyTorch是一个深度学习框架，用于构建和训练神经网络，而SVR（支持向量回归）通常是由Scikit-learn这样的传统机器学习库实现的，两者并不直接兼容。具体来说，��法将SVR直接添加到PyTorch神经网络的后面。

不过，你可以首先使用PyTorch训练的AlexNet模型提取特征，然后用这些特征来训练SVR模型。下面是一种可能的方法：

```python
import torch
import torch.nn as nn
import torchvision.models as models
from sklearn.svm import SVR
from torch.autograd import Variable
import numpy as np

# 加载预训练的AlexNet模型
alexnet = models.alexnet(pretrained=True)

# 修改AlexNet的最后一个全连接层，让其输出特征数为1
num_ftrs = alexnet.classifier[6].in_features
alexnet.classifier[6] = nn.Linear(num_ftrs, 1)

# 创建SVR实例
svr = SVR(kernel='linear')

# 训练和预测的流程可能会像这样：
#   1. 将输入数据传递给AlexNet模型，得到特征
#   2. 将得到的特征转换为Numpy数组，然后用于训练SVR模型
#   3. 使用AlexNet模型提取测试数据的特征
#   4. 将提取的特征用于SVR模型的预测

# 例如，如果你有一些训练数据和标签：
# train_data = ... # 形状为[N, 3, 224, 224]的PyTorch张量
# train_labels = ... # 形状为[N]的Numpy数组

# 你可以这样训练你的模型：
# alexnet_outputs = alexnet(train_data)
# svr.fit(alexnet_outputs.detach().numpy(), train_labels)

# 然后，你可以这样预测新的数据：
# test_data = ... # 形状为[M, 3, 224, 224]的PyTorch张量
# alexnet_outputs = alexnet(test_data)
# predictions = svr.predict(alexnet_outputs.detach().numpy())
```

在上面的代码中，我们首先加载了预训练的AlexNet模型，然后更改了其最后一个全连接层的输出特征数为1。然后我们创建了一个SVR模型实例。

在训练和预测的过程中，我们将输入数据传递给AlexNet模型，得到的输出再被用于训练或预测SVR模型。这个过程需要手动完成，因为PyTorch并不能直接处理在神经网络中使用传统的机器学习模型。

再次强调，这只是一个示例，并没有实际运行的代码。你需要根据你的实际数据和问题来填写和调整上述代码。



# 4.vgg+svr

在PyTorch中实现VGG16和支持向量回在PyTorch中实现VGG16和支持向量回归（SVR）的流程大致如下。首先，我们需要定义VGG16网络，然后，我们将该网络的输出连接到我们的SVR模型。注意，我们不能直接在PyTorch中实现SVR，因此我们需要使用sklearn库来完成这部分。

下面是一个示例代码：

```python
import torch
import torch.nn as nn
import torchvision.models as models
from sklearn.svm import SVR
from sklearn.model_selection import train_test_split
import numpy as np

# 使用预训练的VGG16模型
vgg16 = models.vgg16(pretrained=True)

# 删除最后一层
modules = list(vgg16.children())[:-1] 
vgg16 = nn.Sequential(*modules)

for p in vgg16.parameters():
    p.requires_grad = False

# 将你的数据加载进来，这里暂时使用随机数据代替
data = np.random.rand(1000, 3, 224, 224) # 假设有1000个样本
labels = np.random.rand(1000) # 对应的标签

# 将数据分为训练集和测试集
X_train, X_test, y_train, y_test = train_test_split(data, labels, test_size=0.2)

# 准备训练数据
X_train = torch.from_numpy(X_train).float()
y_train = torch.from_numpy(y_train).float()

# 通过VGG16提取特征
X_train = vgg16(X_train)

# 准备SVR模型
svr = SVR()

# 用SVR模型进行训练
svr.fit(X_train.detach().numpy(), y_train.detach().numpy())

# 测试模型
X_test = torch.from_numpy(X_test).float()
y_test = torch.from_numpy(y_test).float()

X_test = vgg16(X_test)
predictions = svr.predict(X_test.detach().numpy())

print("Predictions: ", predictions)
```

注意：这个代码没有包含数据的预处理，也没有考虑优化和模型性能的监控，你需要根据你的问题对其进行修改。例如，你可能需要添加数据增强、模型调优等步骤。

此外，VGG16模型需要的输入是224x224的图像，这是在ImageNet数据库上预训练的模型的要求。如果你的输入图像大小不同，你可能需要调整它们的大小或修改网络结构。

## VGG+SVR无法训练的问题：

![sunlogin_20230721112433](F:\研一下课题资料\暑假资料\sunlogin_20230721112433.bmp)

output.detach()).cpu().numpy()和target.detach().cpu().numpy()要放在svr.fit（）当中  不要在之前就定义
