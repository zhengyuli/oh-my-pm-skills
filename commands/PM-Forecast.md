# PM-Forecast: 增长预测报告

用户增长和收入预测建模。

## 调用的技能

```
1. skills/engines/analytics-engine
   ↓ 历史数据分析

2. skills/engines/forecast-engine
   ↓ 预测建模 (Logistic/Bass/ARIMA)

3. skills/engines/scoring-engine
   ↓ 风险评估

4. skills/engines/template-engine
   ↓ 使用 forecast-report.md 模板输出
```

## 预测模型

- **市场规模**: TAM/SAM/SOM (Bottom-up / Top-down)
- **用户增长**: Logistic Growth / Bass Diffusion
- **收入预测**: 基于用户的收入模型
- **场景分析**: 乐观/基准/悲观
- **敏感性分析**: 关键驱动因素影响
- **蒙特卡洛**: 10,000+ 次模拟

## 开始

请提供：
- 预测类型 (用户增长/收入/市场规模)
- 预测时间范围 (1-5年)
- 历史数据或基准
