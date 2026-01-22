---
name: priority-evaluator
description: 功能优先级评估专家 - RICE/ICE评分、MoSCoW分类、价值复杂度矩阵、路线图规划
version: 1.0.0
author: oh-my-pm-skills
tags: [core, pm, prioritization, rice, ice, moscow, backlog, roadmapping, value-effort]
allowed-tools: Read, Write, Edit
model: inherit
---

# Priority Evaluator

优先级评估器负责使用多种评分模型评估功能优先级，帮助 PM 做出数据驱动的决策。

## When to Use This Skill

用户请求以下功能时激活此技能：
- "评估这些功能的优先级"
- "功能优先级排序"
- "RICE 评分"
- "ICE 评分"
- "应该先做哪个功能"
- "prioritize features"

## Core Process

### 步骤 1: 理解评估需求

```yaml
收集信息:
  功能列表:
    - 功能名称
    - 简短描述

  上下文:
    - 产品阶段 (MVP/成长/成熟)
    - 团队容量
    - 时间约束
    - 战略目标

  数据可用性:
    - 是否有用户数据？
    - 是否可以估算工作量？
    - 是否有验证数据？
```

### 步骤 2: 选择评分模型

```yaml
模型选择决策树:

有用户数据 + 可估算工作量？
  ├─ 是 → 使用 RICE (跨产品对比)
  └─ 否 ↓

需要快速决策 + 缺少数据？
  ├─ 是 → 使用 ICE (快速评估)
  └─ 否 ↓

确定发布范围 + 资源硬约束？
  └─ 是 → 使用 MoSCoW (必须/应该/可以/不做)

多维度权衡 + 复杂决策？
  └─ 是 → 使用加权评分 (自定义维度)
```

### 步骤 3: 收集评分数据

#### RICE 数据收集

使用 RICE 评分模型（定义详见 `shared/scoring-models.yaml#RICE`）：

**快速参考**：
- **Reach**: 每季度影响用户数 (0-∞)
- **Impact**: 影响程度 (0.25=微, 0.5=小, 1=中, 2=大, 3=巨大)
- **Confidence**: 信心程度 (0-100%)
- **Effort**: 工作量 (人月)

**数据收集模板**：
```yaml
功能: {{feature_name}}

Reach (触达):
  估算: {{total_users}} × {{frequency}} × {{quarterly_periods}}
  数据来源: 现有数据/市场规模/用户调研

Impact (影响):
  选择: {{impact_score}}
  理由: {{rationale}}

Confidence (信心):
  选择: {{confidence_percent}}%
  依据: {{basis}}

Effort (工作量):
  总计: {{total_person_months}} 人月
  考虑因素: 技术复杂度/依赖关系/风险因素
```

#### ICE 数据收集

使用 ICE 评分模型（定义详见 `shared/scoring-models.yaml#ICE`）：

**快速参考**：
- **Impact**: 1-10 (1-2=几乎无影响, 9-10=改变游戏规则)
- **Confidence**: 1-10 (1-2=纯猜测, 9-10=有验证数据)
- **Ease**: 1-10 (1-2=极难实现, 9-10=几乎零成本)

**数据收集模板**：
```yaml
功能: {{feature_name}}

Impact: {{score}} / 10
Confidence: {{score}} / 10
Ease: {{score}} / 10
```

#### MoSCoW 分类

使用 MoSCoW 分类（定义详见 `shared/scoring-models.yaml#MoSCoW`）：

**快速参考**：
- **Must Have**: 没有它产品无法发布
- **Should Have**: 重要但非必需
- **Could Have**: 有了会更好
- **Won't Have**: 明确排除

### 步骤 4: 调用 Scoring Engine

```yaml
scoring_engine:
  action: "calculate"
  model: "{{selected_model}}"

  items:
    - name: "{{feature_name}}"
      {{#if rice}}
      reach: {{reach}}
      impact: {{impact}}
      confidence: {{confidence}}
      effort: {{effort}}
      {{/if}}

      {{#if ice}}
      impact: {{impact}}
      confidence: {{confidence}}
      ease: {{ease}}
      {{/if}}

      {{#if moscow}}
      category: "{{category}}"
      rationale: "{{rationale}}"
      {{/if}}
```

### 步骤 5: 生成评估报告

```markdown
# 功能优先级评估报告

**评估方法**: {{model}}
**评估日期**: {{date}}
**功能数量**: {{total_features}}

---

## 评估结果总览

### 优先级排序

| 排名 | 功能 | 评分 | 类别 | 关键理由 |
|------|------|------|------|----------|
{{#each rankings}}
| {{rank}} | {{name}} | {{score}} | {{category}} | {{rationale}} |
{{/each}}

### 评分分布

**高优先级** ({{high_threshold}}+): {{count}} 个功能
**中优先级** ({{medium_threshold}} - {{high_threshold}}): {{count}} 个功能
**低优先级** (< {{medium_threshold}}): {{count}} 个功能

---

## 详细分析

{{#each features}}
### {{name}}
**评分**: {{score}}
**排名**: 第 {{rank}} 名
**理由**: {{rationale}}
**建议**: {{recommendation}}
{{/each}}

---

*报告由 Priority Evaluator 自动生成*
```

## 交互示例

### 示例 1: RICE 评分

```
用户: 帮我用 RICE 评估这些功能的优先级：
1. 用户批量导入
2. 移动端支持
3. API 限流
4. 实时通知

Priority Evaluator:
  1. 为每个功能收集 RICE 数据
  2. 调用 Scoring Engine 计算
  3. 生成排序报告
  4. 提供实施建议
```

### 示例 2: ICE 快速评估

```
用户: 快速评估这 5 个想法，我们缺少详细数据

Priority Evaluator:
  1. 切换到 ICE 模型
  2. 基于团队经验快速评分
  3. 生成相对优先级
  4. 标记需要验证的假设
```

### 示例 3: MoSCoW 范围决策

```
用户: 我们只有 2 个月时间，如何确定 v1 范围？

Priority Evaluator:
  1. 使用 MoSCoW 分类
  2. 识别 Must Have 功能
  3. 匹配团队容量
  4. 生成 v1 功能清单
```

## 集成点

**使用的引擎**:
- **qa-engine**: 验证评分数据完整性
- **scoring-engine**: 执行评分计算
- **template-engine**: 渲染评估报告
- **document-engine**: 生成最终报告

**与其他技能协作**:
- **prd-generator**: PRD 中的功能优先级
- **jtbd-analyzer**: 机会优先级评估

## 最佳实践

核心原则（详见 `shared/common-sections.yaml#best_practices.scoring`）：

✅ **DO**:
- 明确评分标准和假设
- 记录数据来源和依据
- 使用定性定量结合
- 定期回顾和调整评分

❌ **DON'T**:
- 盲目信任分数，忽略上下文
- 使用不一致的标准
- 忽视定性因素
- 不记录假设和推理

## 数据验证规则

```yaml
RICE 验证:
  - Reach 必须 ≥ 0
  - Impact 必须是 [0.25, 0.5, 1, 2, 3]
  - Confidence 必须 ≤ 100%
  - Effort 必须 > 0

ICE 验证:
  - 所有维度必须在 [1, 10]
  - 至少有一个维度 ≥ 5

MoSCoW 验证:
  - 每个功能必须分类
  - Must Have 不超过总量的 50%
  - 提供分类理由
```

## 输出格式

### 成功输出

```yaml
result:
  success: true
  model: "{{model}}"
  total_features: {{count}}

  rankings:
    - rank: 1
      name: "{{feature_name}}"
      score: {{score}}
      category: "high_priority"

  summary:
    high_priority: {{count}}
    medium_priority: {{count}}
    low_priority: {{count}}

  recommendations:
    immediate: ["{{feature1}}", "{{feature2}}"]
    short_term: ["{{feature3}}"]
    deferred: ["{{feature4}}"]
```

### 缺失数据

```yaml
result:
  success: false
  reason: "missing_data"

  missing:
    - feature: "{{feature_name}}"
      fields: ["reach", "effort"]
      priority: "P0"

  next_action:
    - "提供缺失数据"
    - "或切换到 ICE 快速评估"
```

## 测试场景

```bash
# RICE 评分
priority-evaluator score \
  --model rice \
  --features features.json

# ICE 快速评估
priority-evaluator score \
  --model ice \
  --features ideas.json

# MoSCoW 分类
priority-evaluator classify \
  --features backlog.json \
  --capacity 12

# 对比分析
priority-evaluator compare \
  --features features.json \
  --models rice,ice
```

## 参考

- 评分模型定义: shared/scoring-models.yaml
  - RICE: shared/scoring-models.yaml#RICE
  - ICE: shared/scoring-models.yaml#ICE
  - MoSCoW: shared/scoring-models.yaml#MoSCoW
  - Weighted: shared/scoring-models.yaml#Weighted
- 最佳实践: shared/common-sections.yaml#best_practices.scoring
