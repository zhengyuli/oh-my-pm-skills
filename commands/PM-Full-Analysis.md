# PM-Full-Analysis: 一站式产品分析

全面的产品机会评估，从市场到执行的完整分析。

## 调用的技能

```
阶段 1: 市场研究
skills/core/research-assistant
↓ 市场规模、竞争格局、客户分析

阶段 2: 用户洞察
skills/core/jtbd-analyzer
↓ 待办任务、四力量分析、雇佣标准

阶段 3: 增长预测
skills/engines/forecast-engine
↓ TAM/SAM/SOM、用户增长、收入预测

阶段 4: 风险评估
skills/security/threat-modeling
↓ STRIDE 威胁、DREAD 评分、合规检查

阶段 5: 优先级排序
skills/core/priority-evaluator
↓ 功能 RICE、市场 ICE、执行优先级

阶段 6: 文档生成
skills/core/prd-generator
skills/engines/template-engine
↓ 生成完整文档包
```

## 输出文档包

**⚠️ 重要**: 所有输出遵循 `skills/shared/output-paths.yaml` 中定义的统一路径规范

```
outputs/
├── prds/
│   ├── YYYY-MM-DD-[project]-full-analysis-prd.md  (主 PRD 文档)
│   └── EXECUTIVE_SUMMARY.md                       (执行摘要，覆盖写入)
├── market-research/
│   └── YYYY-MM-DD-[project]-market-research.md     (市场研究报告)
├── jtbd/
│   └── YYYY-MM-DD-[project]-jtbd-analysis.md       (JTBD 分析报告)
├── forecasts/
│   └── YYYY-MM-DD-[project]-growth-forecast.md     (增长预测报告)
├── threat-models/
│   └── YYYY-MM-DD-[project]-threat-model.md        (威胁建模报告)
├── logs/
│   └── YYYY-MMDD-pm-full-analysis-[project].log    (执行日志)
└── references/
    └── YYYY-MMDD-[project]-urls.md                 (参考文献 URLs 清单)
```

**参考文献**:
- 所有搜索到的链接和引用汇总到 `outputs/references/YYYY-MMDD-[project]-urls.md`
- 每个子报告末尾包含完整的参考文献章节
- 主 PRD 文档汇总所有引用

## 开始

请描述：
- 产品想法或市场机会
- 目标市场和用户
- 分析深度偏好
