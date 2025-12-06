[根目录](../CLAUDE.md) > **Chapter6**

# Chapter 6 - 风险管理与投资组合优化

## 模块职责

本模块专注于投资组合优化和风险管理，展示如何使用深度学习技术来改进传统的投资组合构建方法，并提供更好的风险预测。

## 入口文件

- `01_classical_portfolio_optimization.ipynb` - 经典投资组合优化理论
- `02_deep_portfolio_optimization.ipynb` - 深度学习投资组合优化

## 主要内容

### 01_classical_portfolio_optimization.ipynb
- 马科维茨均值-方差模型
- 有效前沿理论
- 风险平价策略
- 最大分散化投资组合

### 02_deep_portfolio_optimization.ipynb
- 深度学习预测资产风险
- 端到端投资组合优化
- 动态风险管理
- 交易成本考虑

## 经典理论回顾

### 马科维茨模型
- 目标：最小化组合方差
- 约束：权重和为1，目标收益率
- 问题：需要估计协方差矩阵，误差放大

### 风险度量
- **波动率**: 收益率标准差
- **VaR**: 风险价值
- **CVaR**: 条件风险价值
- **最大回撤**: 历史最大损失

## 深度学习方法

### 优势
1. **非线性建模**: 捕捉资产间复杂依赖关系
2. **端到端优化**: 直接优化目标函数
3. **动态调整**: 适应市场变化
4. **特征学习**: 自动发现有用特征

### 实现细节
```python
class PortfolioNet(nn.Module):
    def __init__(self, n_assets, lookback_period):
        super().__init__()
        # 特征提取层
        self.feature_extractor = nn.Sequential(...)
        # 组合权重生成层
        self.weight_generator = nn.Sequential(...)
```

## 风险预测模型

### 深度学习模型类型
1. **MLP**: 基础全连接网络
2. **LSTM**: 时间序列风险预测
3. **GAN**: 生成极端情景
4. **VAE**: 风险因子学习

### 训练目标
- 波动率预测精度
- 风险极端值捕捉
- 稳定性（过参数化控制）

## 已训练模型
- `model/best_mlp` - 投资组合优化模型

## 关键依赖

```python
import torch
import torch.nn as nn
import numpy as np
import pandas as pd
from cvxpy import *  # 凸优化
import pypfopt as pf  # 投资组合优化库
```

## 实施注意事项

### 数据要求
- 资产价格历史数据
- 交易成本数据
- 约束条件（如做空限制）

### 实际挑战
1. **交易成本**: 频繁调整增加成本
2. **估计误差**: 输入参数的估计误差
3. **模型风险**: 模型假设失效
4. **执行风险**: 滑点和延迟

## 常见问题 (FAQ)

1. **Q: 深度学习方法相比传统方法的优势？**
   A: 能处理非高诺分布，捕捉非线性关系，动态适应市场变化。

2. **Q: 如何处理交易成本？**
   A: 在损失函数中加入交易成本项，使用L1正则化控制换手率。

## 相关文件清单

- `01_classical_portfolio_optimization.ipynb` - 经典方法
- `02_deep_portfolio_optimization.ipynb` - 深度学习方法
- `model/best_mlp` - 训练好的模型
- `../Data/portfolio_data.csv` - 投资组合数据
- `../Utilis/` - 工具函数

## 变更记录 (Changelog)

### 2025-12-06 09:50:23
- ✨ 创建Chapter6模块文档
- 📈 记录投资组合优化的经典与深度学习方法
- ⚖️ 强调风险管理的重要性