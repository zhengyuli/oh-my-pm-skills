# PM-Market-Research: 市场研究报告

全面的市场机会评估和竞争分析。

## 调用的技能

```
1. skills/core/research-assistant
   ↓ 市场规模、竞争格局、客户分析

2. skills/engines/forecast-engine
   ↓ TAM/SAM/SOM 计算、增长预测

3. skills/core/priority-evaluator
   ↓ 市场机会吸引力评估

4. skills/engines/template-engine
   ↓ 使用 market-research.md 模板输出
```

## 研究内容

- **市场规模**: TAM、SAM、SOM 计算
- **竞争分析**: 主要竞品深度分析 (3-5家)
- **客户洞察**: 用户画像、痛点分析
- **机会评估**: 市场空白、进入壁垒
- **投资分析**: 初期投资、ROI、盈亏平衡

## 输出

**⚠️ 重要**: 所有输出遵循 `skills/shared/output-paths.yaml` 中定义的统一路径规范

```
outputs/
├── market-research/
│   └── YYYY-MM-DD-[topic]-market-research.md         (主研究报告)
├── logs/
│   └── YYYY-MMDD-pm-market-research-[topic].log      (执行日志)
└── references/
    └── YYYY-MMDD-[topic]-urls.md                     (参考文献 URLs 清单)
```

**参考文献**:
- 所有搜索到的链接和引用汇总到独立的 URLs 清单文件
- 报告末尾包含完整的参考文献章节
- 每个数据点标注引用上标（如 `$42.5 亿 [Gartner 2024]¹`）

## 开始

请提供：
- 目标市场或产品领域
- 研究目标 (进入评估/投资决策/竞品监控)
