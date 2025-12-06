[根目录](../CLAUDE.md) > **Chapter2**

# Chapter 2 - 统计分析与时间序列建模

## 模块职责

本模块介绍金融时间序列的基础统计分析方法，包括正态性检验、平稳性检验、自相关分析等，为后续的深度学习应用打下基础。

## 入口文件

- `01_statistics.ipynb` - 统计分析与正态性检验
- `02_time_series_models.ipynb` - 时间序列模型
- `03_volatility_clustering.ipynb` - 波动率聚类分析

## 主要内容

### 01_statistics.ipynb
- 使用yfinance获取AAPL股票数据
- 计算和对数收益率
- 绘制直方图和Q-Q图
- Jarque-Bera正态性检验
- ACF和PACF自相关分析
- ADF平稳性检验

### 关键依赖
```python
import numpy as np
import matplotlib.pyplot as plt
import yfinance as yf
import scipy.stats as stats
from statsmodels.stats.stattools import jarque_bera
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
from statsmodels.tsa.stattools import adfuller
import pandas as pd
```

## 测试与验证

- 通过p-value检验正态性假设
- ADF检验确认序列平稳性
- 自相关函数分析时间依赖性

## 常见问题 (FAQ)

1. **Q: 为什么金融收益率通常不符合正态分布？**
   A: 金融收益率常表现出尖峰厚尾特征，存在极端事件风险。

2. **Q: ACF和PACF的区别是什么？**
   A: ACF测量总相关性，PACF测量排除中间变量影响后的直接相关性。

## 相关文件清单

- `01_statistics.ipynb` - 统计分析notebook
- `02_time_series_models.ipynb` - 时间序列模型
- `03_volatility_clustering.ipynb` - 波动率聚类
- `../Data/aapl.csv` - AAPL股票数据（通过yfinance获取）

## 变更记录 (Changelog)

### 2025-12-06 09:50:23
- ✨ 创建Chapter2模块文档
- 📝 记录各notebook的主要内容和功能