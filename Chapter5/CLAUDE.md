[根目录](../CLAUDE.md) > **Chapter5**

# Chapter 5 - 动量策略与深度学习增强

## 模块职责

本模块介绍经典的量化交易策略，特别是动量策略，并展示如何使用深度学习方法来增强这些策略的表现。

## 入口文件

- `01_time_series_momentum.ipynb` - 时间序列动量策略
- `02_cross_sectional_momentum.ipynb` - 截面动量策略
- `03_deep_momentum_strategy.ipynb` - 深度学习增强的动量策略

## 主要内容

### 01_time_series_momentum.ipynb
- 时间序列动量策略原理
- 基于过去收益率的信号生成
- 策略回测与评估

### 02_cross_sectional_momentum.ipynb
- 截面动量（相对动量）策略
- 横截面资产排序
- 投资组合构建

### 03_deep_momentum_strategy.ipynb
- 深度神经网络直接优化夏普比率
- 特征工程（TSMOM、SMA、MACD等）
- 端到端策略训练

## 深度动量策略架构

### MLP模型结构
```python
class MLP(nn.Module):
    def __init__(self, seq_length, n_features):
        super().__init__()
        self.net = nn.Sequential(
            nn.Flatten(),
            nn.Linear(flat_dim, 64),
            nn.Softsign(),
            nn.Linear(64, 32),
            nn.Softsign(),
            nn.Linear(32, 1),
            nn.Softsign()
        )
```

### 特征工程
- **TSMOM**: 时间序列动量信号
- **SMA**: 简单移动平均线
- **MACD**: 多重指数平滑异同移动平均线

## 训练细节

- **损失函数**: SharpeLoss（直接优化夏普比率）
- **早停机制**: 防止过拟合
- **优化器**: Adam
- **批次大小**: 128
- **学习率**: 0.0001

## 已训练模型
- `model/best_mlp` - 深度动量策略模型

## 策略性能评估

### 关键指标
- 年化收益率 (Annual Return)
- 年化波动率 (Annual Volatility)
- 夏普比率 (Sharpe Ratio)

### 回测结果示例
- 年化收益: 2.84%
- 年化波动: 3.73%
- 夏普比率: 0.76

## 关键依赖

```python
import torch
import torch.nn as nn
import numpy as np
import pandas as pd
from Utilis.early_stopper import EarlyStopping
from Utilis.loss import SharpeLoss
from Utilis.metrics import report_metrics
```

## 常见问题 (FAQ)

1. **Q: 为什么使用Softsign激活函数？**
   A: Softsign相比tanh在输入较大时梯度下降更平滑，适合金融数据。

2. **Q: 直接优化夏普比率的优势是什么？**
   A: 直接优化风险调整后收益，避免了需要独立优化收益和风险的两步过程。

## 相关文件清单

- `01_time_series_momentum.ipynb` - 时间序列动量
- `02_cross_sectional_momentum.ipynb` - 截面动量
- `03_deep_momentum_strategy.ipynb` - 深度动量策略
- `model/best_mlp` - 训练好的模型
- `../Data/aapl.csv` - 股票数据
- `../Utilis/` - 工具函数

## 变更记录 (Changelog)

### 2025-12-06 09:50:23
- ✨ 创建Chapter5模块文档
- 📊 记录动量策略的实现细节
- 🎯 强调深度学习增强策略的优势