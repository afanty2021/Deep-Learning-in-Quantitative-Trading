[根目录](../CLAUDE.md) > **Chapter3**

# Chapter 3 - 监督学习与神经网络

## 模块职责

本模块介绍监督学习的基础概念和各种神经网络架构，包括全连接网络、CNN、RNN、WaveNet和Transformer，为量化交易中的预测任务奠定基础。

## 入口文件

- `01_regression_classification.ipynb` - 回归与分类的损失函数和评估指标
- `02_regression_training.ipynb` - 神经网络训练实战

## 主要内容

### 01_regression_classification.ipynb
- 回归损失函数：MSE、RMSE、MSLE、MAE、Huber损失
- 分类评估指标：准确率、F1分数、混淆矩阵
- 分类报告生成

### 02_regression_training.ipynb
- 多种神经网络架构实现
- 时间序列数据预处理
- 模型训练与评估

### 已训练模型
- `model/best_cnn` - 卷积神经网络模型
- `model/best_lstm` - LSTM模型
- `model/best_mlp` - 多层感知机模型
- `model/best_transformer` - Transformer模型
- `model/best_wavenet` - WaveNet模型

## 关键依赖

### 基础库
```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.metrics import (mean_squared_error, mean_absolute_error,
                           accuracy_score, f1_score, confusion_matrix)
```

### 深度学习框架
```python
import torch
import torch.nn as nn
import torch.optim as optim
```

## 模型架构

### 支持的神经网络类型
1. **MLP (多层感知机)**: 基础全连接网络
2. **CNN (卷积神经网络)**: 适合提取局部特征
3. **LSTM**: 处理序列数据的经典RNN
4. **Transformer**: 基于注意力机制的先进模型
5. **WaveNet**: 专为序列设计的卷积网络

## 训练流程

1. 数据加载与预处理
2. 模型架构定义
3. 损失函数选择
4. 优化器配置
5. 训练循环实现
6. 早停机制应用
7. 模型保存与加载

## 测试与验证

- 使用scikit-learn的标准评估指标
- 支持回归和分类任务
- 可视化评估结果

## 常见问题 (FAQ)

1. **Q: 何时使用Huber损失？**
   A: Huber损失对异常值鲁棒，适合存在噪声的金融数据。

2. **Q: 如何选择合适的神经网络架构？**
   A: 根据数据特性选择：序列数据用LSTM/Transformer，局部特征用CNN。

## 相关文件清单

- `01_regression_classification.ipynb` - 损失函数与评估指标
- `02_regression_training.ipynb` - 模型训练
- `model/` - 训练好的模型参数
- `../Utilis/` - 工具函数库

## 变更记录 (Changelog)

### 2025-12-06 09:50:23
- ✨ 创建Chapter3模块文档
- 📝 记录支持的5种神经网络架构
- 📁 列出所有预训练模型