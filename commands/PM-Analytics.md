# PM-Analytics: 数据分析报告

分析产品数据并生成洞察报告。

## 调用的技能

```
1. skills/engines/analytics-engine
   ↓ 计算用户指标、转化率、留存等

2. skills/core/priority-evaluator
   ↓ 评估行动建议优先级

3. skills/engines/template-engine
   ↓ 使用 analytics-report.md 模板输出
```

## 分析能力

- **用户指标**: DAU、MAU、留存率 (D1/D7/D30)、增长趋势
- **转化分析**: 漏斗转化、流失分析
- **A/B 测试**: 统计显著性检验 (Z-test)、置信区间
- **收入分析**: ARPU、ARPPU、LTV、CAC、LTV/CAC
- **异常检测**: 识别数据异常点和原因

## 开始

请提供：
- 数据来源和分析周期
- 需要分析的具体指标
- 数据文件或描述
