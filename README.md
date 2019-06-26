# URFC2019_Preliminary
2019 The 5th Baidu & XJTU Big Data Contest The First IKCEST “The Belt and Road” International Big Data Contest

## 线上测试准确率 
单模型单次训练， online:0.7117
单模型十折融合， online:0.7197

## 网络结构
- 复现abadcandy pytorch版本的baseline，online：0.6623
- 采用image，visit双网络，分别生成256d特征，concat后全连接到9维输出
- image采用imagenet上预训练的 ResNet-50 提取特征
- visit采用手动搭建的简单网络提取特征（2个inception module和2个residual block）
