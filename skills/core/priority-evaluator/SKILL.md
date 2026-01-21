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

#### RICE 数据收集模板

```yaml
功能: {{feature_name}}

Reach (触达):
  问题: 每季度有多少用户/事务会用到？
  估算:
    - 总用户数: {{total_users}}
    - 使用频率: {{frequency}} (每日/每周/每月/每季度)
    - 计算: {{total_users}} × {{quarterly_periods}} = {{reach}}

  数据来源:
    - 现有数据分析
    - 市场规模估算
    - 用户调研

Impact (影响):
  问题: 对每个受影响用户有多大影响？
  评分标准:
    3 (巨大): 对 OKR 有决定性影响，显著改变用户行为
    2 (大): 显著推动目标，明显改善体验
    1 (中): 适度改善，有小幅提升
    0.5 (小): 轻微改善，几乎无感知
    0.25 (微): 几乎无影响

  选择: {{impact_score}}
  理由: {{rationale}}

Confidence (信心):
  问题: 对估算有多大把握？
  评分标准:
    100%: 有历史数据或 A/B 测试支持
    80%: 有部分数据和用户验证
    50%: 基于假设和经验，需要验证

  选择: {{confidence_percent}}%
  依据: {{basis}}

Effort (工作量):
  问题: 需要多少团队工作量？
  估算:
    - 设计: {{design_weeks}} 周
    - 开发: {{dev_weeks}} 周
    - 测试: {{qa_weeks}} 周
    - 部署: {{deploy_weeks}} 周
    - 总计: {{total_person_months}} 人月

  考虑因素:
    - 技术复杂度
    - 依赖关系
    - 风险因素

RICE 分数: ({{reach}} × {{impact}} × {{confidence}}%) / {{effort}} = {{rice_score}}
```

#### ICE 数据收集模板

```yaml
功能: {{feature_name}}

Impact (影响): {{score}} / 10
  9-10: 改变游戏规则，对 OKR 有决定性影响
  7-8: 显著改善，明显推动目标
  5-6: 适度提升，有正面影响
  3-4: 轻微改善，影响有限
  1-2: 几乎无影响

Confidence (信心): {{score}} / 10
  9-10: 有验证数据支持，高度确信
  7-8: 有部分验证，较有把握
  5-6: 基于经验，有把握
  3-4: 基于假设，有些不确定
  1-2: 纯猜测，高度不确定

Ease (容易度): {{score}} / 10
  9-10: 几乎零成本，快速实现
  7-8: 低成本，1-2 周内完成
  5-6: 中等成本，1-2 个冲刺
  3-4: 高成本，需要多个冲刺
  1-2: 极难实现，需要大量资源

ICE 分数: {{impact}} × {{confidence}} × {{ease}} = {{ice_score}}
```

#### MoSCoW 分类模板

```yaml
功能: {{feature_name}}

分类: {{category}}

Must Have (必须有):
  定义: 没有它产品无法发布或没有价值
  判断标准:
    - 是核心价值主张吗？
    - 用户会因为没有它而拒绝使用吗？
    - 是 MVP 定义的一部分吗？

Should Have (应该有):
  定义: 重要但非必需，可以推迟到后续版本
  判断标准:
    - 显著改善用户体验吗？
    - 有明确用户需求吗？
    - 付出与回报成正比吗？

Could Have (可以做):
  定义: 有了会更好，如果时间允许
  判断标准:
    - 不错的功能，但非关键
    - 实现成本低
    - 可以放入待办事项

Won't Have (不做):
  定义: 明确排除，当前版本不考虑
  判断标准:
    - 与当前战略不一致
    - 成本高于收益
    - 技术上不可行
```

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
{{#each high_priority}}
- {{name}} ({{score}})
{{/each}}

**中优先级** ({{medium_threshold}} - {{high_threshold}}): {{count}} 个功能
{{#each medium_priority}}
- {{name}} ({{score}})
{{/each}}

**低优先级** (< {{medium_threshold}}): {{count}} 个功能
{{#each low_priority}}
- {{name}} ({{score}})
{{/each}}

---

## 详细分析

{{#each features}}

### {{name}}

**评分**: {{score}}
**排名**: 第 {{rank}} 名

**评分明细**:
{{#if rice}}
- Reach: {{reach}} (每季度 {{formatted_reach}} 个用户/事务)
- Impact: {{impact}} ({{impact_description}})
- Confidence: {{confidence}}% ({{confidence_basis}})
- Effort: {{effort}} 人月 ({{effort_breakdown}})
{{/if}}

{{#if ice}}
- Impact: {{impact}}/10 ({{impact_description}})
- Confidence: {{confidence}}/10 ({{confidence_basis}})
- Ease: {{ease}}/10 ({{ease_description}})
{{/if}}

**理由**: {{rationale}}

**建议**: {{recommendation}}

---

{{/each}}

## 工作量分析

### 快速胜利 (低投入高回报)

{{#each quick_wins}}
- {{name}} ({{effort}} 人月, 评分: {{score}})
{{/each}}

### 大型项目 (高投入高回报)

{{#each big_bets}}
- {{name}} ({{effort}} 人月, 评分: {{score}})
{{/each}}

### 低优先级 (低投入低回报)

{{#each low_priority_items}}
- {{name}} ({{effort}} 人月, 评分: {{score}})
{{/each}}

## 敏感性分析

如果用户增长达到预期的 2 倍:
{{#each sensitivity_2x}}
- {{name}}: {{original}} → {{new}} (变化: {{delta}})
{{/each}}

如果信心水平下降 20%:
{{#each sensitivity_confidence}}
- {{name}}: {{original}} → {{new}} (变化: {{delta}})
{{/each}}

## 建议

### 立即开始 (冲刺 1-2)
{{#each immediate}}
1. {{name}} - {{reason}}
{{/each}}

### 近期规划 (冲刺 3-4)
{{#each short_term}}
1. {{name}} - {{reason}}
{{/each}}

### 中期考虑 (下一季度)
{{#each medium_term}}
1. {{name}} - {{reason}}
{{/each}}

### 暂缓实施
{{#each deferred}}
1. {{name}} - {{reason}}
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

✅ **DO**:
- 明确评分标准和假设
- 记录数据来源和依据
- 使用定性定量结合
- 定期回顾和调整评分
- 考虑团队容量和约束

❌ **DON'T**:
- 盲目信任分数忽略上下文
- 使用不一致的标准
- 忽视定性因素
- 不记录假设和推理
- 过度优化评分模型

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
