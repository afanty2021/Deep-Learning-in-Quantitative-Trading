[根目录](../CLAUDE.md) > **Utilis**

# 工具函数库

## 模块职责

Utilis模块包含项目各章节共享的工具函数和辅助类，提供通用的数据处理、模型训练、评估指标等功能。

## 工具函数清单

### 1. 早停机制 (early_stopper.py)
- **功能**: 防止模型过拟合的早停实现
- **特性**:
  - 监控验证损失
  - 耐心参数设置
  - 最小增量阈值
  - 自动保存最佳模型
  - 详细日志输出

### 2. 损失函数 (loss.py)
- **功能**: 实现金融特定的损失函数
- **主要函数**:
  - `SharpeLoss`: 直接优化夏普比率
  - 其他自定义损失函数

### 3. 评估指标 (metrics.py)
- **功能**: 提供金融策略评估指标
- **主要函数**:
  ```python
  def report_metrics(ret):
      res = {}
      res['annual_ret'] = np.mean(ret) * 252
      res['annual_std'] = np.std(ret) * np.sqrt(252)
      res['annual_sharpe'] = (np.mean(ret) / np.std(ret)) * np.sqrt(252)
      return res
  ```
- **指标说明**:
  - 年化收益率 (Annual Return)
  - 年化波动率 (Annual Volatility)
  - 年化夏普比率 (Annual Sharpe Ratio)

### 4. 数据处理 (torch_data.py)
- **功能**: PyTorch数据处理工具
- **主要类**:
  - `MyDataset`: 自定义数据集类
  - 数据加载器辅助函数

### 5. 包初始化 (__init__.py)
- **功能**: 模块初始化文件
- **导出**: 公开主要函数和类

## 使用示例

### 早停机制使用
```python
from Utilis.early_stopper import EarlyStopping

# 创建早停器
early_stopper = EarlyStopping(
    savepath='model/best_model',
    patience=100,
    min_delta=1e-4,
    verbose=True
)

# 在训练循环中使用
for epoch in range(epochs):
    # ... 训练代码 ...
    val_loss = compute_validation_loss()

    early_stopper(model, val_loss)
    if early_stopper.early_stop:
        print("Early stopping triggered!")
        break
```

### Sharpe损失函数使用
```python
from Utilis.loss import SharpeLoss

# 创建损失函数
criterion = SharpeLoss()

# 在训练中使用
loss = criterion(predictions, targets)
loss.backward()
```

### 评估指标使用
```python
from Utilis.metrics import report_metrics

# 计算策略收益的评估指标
metrics = report_metrics(strategy_returns)
print(f"年化收益率: {metrics['annual_ret']:.2%}")
print(f"年化波动率: {metrics['annual_std']:.2%}")
print(f"夏普比率: {metrics['annual_sharpe']:.2f}")
```

## 设计原则

### 1. 模块化
- 每个功能独立文件
- 清晰的接口定义
- 最小化依赖

### 2. 可复用性
- 通用函数设计
- 参数化配置
- 跨章节共享

### 3. 金融特异性
- 针对金融数据优化
- 考虑时间序列特性
- 金融指标实现

## 扩展建议

### 可能添加的工具
1. **特征工程函数**:
   - 技术指标计算
   - 时间序列特征提取
   - 滚动窗口计算

2. **可视化工具**:
   - 收益曲线图
   - 相关性热图
   - 风险度量图

3. **回测框架**:
   - 更完整的回测引擎
   - 交易成本计算
   - 基准比较

4. **数据下载器**:
   - 多数据源支持
   - 自动数据更新
   - 数据缓存机制

## 最佳实践

### 1. 函数设计
- 清晰的文档字符串
- 类型提示
- 错误处理

### 2. 性能优化
- 向量化操作
- 避免不必要的循环
- 内存管理

### 3. 测试覆盖
- 单元测试
- 边界条件测试
- 性能测试

## 常见问题 (FAQ)

1. **Q: 早停机制如何判断模型改进？**
   A: 通过验证损失的最小增量阈值判断，只有显著改进才保存模型。

2. **Q: Sharpe损失函数的原理？**
   A: 将夏普比率作为损失函数进行优化，最大化风险调整后收益。

## 相关文件清单

- `__init__.py` - 模块初始化
- `early_stopper.py` - 早停机制实现
- `loss.py` - 损失函数定义
- `metrics.py` - 评估指标计算
- `torch_data.py` - PyTorch数据处理

## 变更记录 (Changelog)

### 2025-12-06 09:50:23
- ✨ 创建Utilis模块文档
- 🔧 详细记录5个工具模块的功能
- 💡 提供使用示例和扩展建议