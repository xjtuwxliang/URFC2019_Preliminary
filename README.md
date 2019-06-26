# URFC2019_Preliminary
2019 The 5th Baidu & XJTU Big Data Contest The First IKCEST “The Belt and Road” International Big Data Contest

## 线上测试准确率 
- 单模型单次训练， online:0.7117
- 单模型十折融合， online:0.7197

## 网络结构
- 复现abadcandy pytorch版本的baseline，online：0.6623。
- 采用image，visit双网络，分别生成256维特征，concat后得到512维特征全连接到9维输出。
- image采用imagenet上预训练的 ResNet-50 提取特征。
- visit采用手动搭建的无预训练的简单网络提取特征（2个inception module和2个residual block）。
- visit先经过简单处理为24×182×1的ndarray格式，然后经过归一化，标准化等5种不同的预处理，生成shape为24×182×5的数据，送入visit网络。
- 对image和visit均进行了数据增强，应对过拟合（visit增强的方式：变换到0-255的像素范围内将其当作图片进行数据增强）。

## 运行环境
- Ubuntun16.04
- Pytorch 1.1.0
- NVIDIA GTX 1080Ti
## 运行说明
```
cd URFC2019_Preliminary
mkdir data
```
- data/ 数据文件夹
- preliminary/初赛数据csv文件
- multimain.py 主程序
- multimodal.py 网络模型
- preprocess.py 数据增强
- config.py 参数配置
- utils.py 通用模块
