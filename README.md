# URFC2019_Preliminary
2019 The 5th Baidu & XJTU Big Data Contest The First IKCEST “The Belt and Road” International Big Data Contest

## 线上测试准确率 
- 单模型单次训练， online:0.7117
- 单模型十折融合， online:0.7199

## 网络结构及改进
- 复现[ABadCandy Pytorch版本的baseline](https://github.com/ABadCandy/BaiDuBigData19-URFC)，online：0.6678。
- 采用 image，visit 双网络，分别生成256维特征，concat 后得到512维特征全连接到9维输出。
- image 采用 imagenet 上预训练的 ResNet-50 提取特征。
- visit 采用手动搭建的无预训练的简单网络提取特征（2个inception module和2个residual block）。
- visit 先经过简单预处理保存为24×182×1的ndarray格式，我们将visit经过归一化，标准化等5种不同的预处理，得到shape为24×182×5的数据，送入visit网络。
- 对image和visit均进行了数据增强，应对过拟合（visit增强的方式：变换到0-255的像素范围内将其当作图片进行数据增强）。
- visit和image网络采用不同的学习率。
- 可以选择使用mixup，默认未使用。

## 运行环境
- Ubuntu16.04
- Pytorch 1.1.0
- NVIDIA GTX 1080Ti×2
## 运行说明
### 1. 准备数据
同ABadCandy Pytorch版本的baseline
```
cd URFC2019_Preliminary
mkdir data
cd data
mkdir train test  #创建训练image文件夹train, 测试图片文件夹test
mkdir -p npy/train npy/test  #创建训练visit文件夹npy/train, 测试visit文件夹npy/test
```
分别将去噪后的image和ndarray格式的visit数据放入相应文件夹中。
 
### 2. 运行程序
数据准备好后，运行multimain.py文件即可进行单模型单次训练。
 
- data/ 数据文件夹
- preliminary/ 存放初赛数据csv文件
- multimain.py 主程序
- multimodal.py 网络模型
- preprocess.py 数据增强
- config.py 参数配置
- utils.py 通用模块

注：
1. 可在config.py中更改参数配置。
2. 可在multimodal.py中更改网络结构。
3. 默认采用sgd训练60epoches，带warmup的cos学习率策略，训练时间大约3hours，为加速可以选择更换优化器，减少epoch数。
