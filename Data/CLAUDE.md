[根目录](../CLAUDE.md) > **Data**

# 数据集模块

## 模块职责

本模块包含项目使用的所有数据集，为各个章节提供实验数据。

## 数据清单

### 1. AAPL股票数据
- **文件**: `aapl.csv`
- **描述**: 苹果公司股票历史价格数据
- **时间范围**: 历史数据（从1980年开始）
- **字段说明**:
  - `Close`: 收盘价
  - `High`: 最高价
  - `Low`: 最低价
  - `Open`: 开盘价
  - `Volume`: 成交量
  - `Ticker`: 股票代码

### 2. 限价订单簿数据
- **文件**: `limit_order_book_data.csv`
- **描述**: 高频限价订单簿数据
- **数据结构**: 40列特征
  - `AskPrice1-10`: 卖方价格（10档）
  - `BidPrice1-10`: 买方价格（10档）
  - `AskVolume1-10`: 卖方成交量（10档）
  - `BidVolume1-10`: 买方成交量（10档）
- **用途**: Chapter7高频交易分析

### 3. 投资组合数据
- **文件**: `portfolio_data.csv`
- **描述**: 多资产投资组合数据
- **用途**: Chapter6投资组合优化

## 数据格式

### CSV文件格式
所有数据文件均采用CSV格式，使用标准的逗号分隔。

### 数据质量
- 已清洗去除异常值
- 缺失值已处理
- 数据格式标准化

## 使用示例

### 加载AAPL数据
```python
import pandas as pd

# 读取数据
df = pd.read_csv('../Data/aapl.csv')

# 计算收益率
df['returns'] = np.log(df['Close']/df['Close'].shift(1))

# 显示前5行
print(df.head())
```

### 加载LOB数据
```python
# 定义列名
COLsP = sum([['AskPrice'+str(i), 'BidPrice'+str(i)] for i in range(1, 11)], [])
COLsV = sum([['AskVolume'+str(i), 'BidVolume'+str(i)] for i in range(1, 11)], [])

# 读取数据
df = pd.read_csv('../Data/limit_order_book_data.csv')

# 计算中价
df['MidPrice'] = (df['AskPrice1'] + df['BidPrice1']) / 2
```

## 数据来源

1. **AAPL数据**: 通过yfinance从Yahoo Finance获取
2. **LOB数据**: 高频数据提供商（需注意使用许可）
3. **投资组合数据**: 合成数据或公开数据集

## 数据更新

- 股票数据可通过yfinance实时更新
- LOB数据需要特定的数据源
- 建议定期更新数据以保持时效性

## 注意事项

1. **数据许可**: 使用前确认数据使用权限
2. **存储空间**: LOB数据文件较大，注意磁盘空间
3. **内存使用**: 加载大数据集时注意内存管理
4. **备份建议**: 重要数据建议备份

## 常见问题 (FAQ)

1. **Q: 如何获取更多股票数据？**
   A: 使用yfinance或alpha_vantage等API获取。

2. **Q: LOB数据是否需要特殊处理？**
   A: 需要标准化和特征工程，参考Chapter7示例。

## 相关文件清单

- `aapl.csv` - 苹果股票数据
- `limit_order_book_data.csv` - 限价订单簿数据
- `portfolio_data.csv` - 投资组合数据

## 变更记录 (Changelog)

### 2025-12-06 09:50:23
- ✨ 创建Data模块文档
- 📋 记录所有数据集的详细信息
- 💾 提供数据加载示例代码