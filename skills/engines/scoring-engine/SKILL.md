---
name: scoring-engine
description: 评分计算引擎 - RICE/ICE/DREAD评分、MoSCoW分类、价值复杂度矩阵、ROI计算
version: 1.0.0
author: oh-my-pm-skills
tags: [engine, scoring, prioritization, rice, ice, dread, moscow, roi, value-matrix]
allowed-tools: Read, Write, Edit
model: inherit
---

# Scoring Engine

评分引擎负责实现各种优先级评分算法，帮助决策功能优先级和资源分配。

## When to Use This Engine

其他技能需要以下功能时调用此引擎：
- 功能优先级排序
- 影响力评估
- 复杂度分析
- 投资回报计算
- 风险评分

## 支持的评分模型

### RICE 评分

**用途**: 跨产品/功能对比优先级

**公式**:
```
RICE = (Reach × Impact × Confidence) / Effort
```

**评分维度**:

| 维度 | 范围 | 说明 | 示例问题 |
|------|------|------|---------|
| **Reach** | 0-∞ | 每季度影响用户/事务数 | "每季度有多少用户会用到？" |
| **Impact** | 1-3 | 对每个受影响用户的影响 | "巨(3) / 大(2) / 中(1) / 小(0.5) / 微(0.25)" |
| **Confidence** | 0-100% | 对数据的信心程度 | "高(100%) / 中(80%) / 低(50%)" |
| **Effort** | 月/人 | 团队所需工作量 | "需要多少人月？" |

**示例**:
```yaml
功能: "用户批量导入"
Reach: 2000      # 每季度 2000 个用户使用
Impact: 3        # 巨大影响
Confidence: 80%  # 中等信心
Effort: 3        # 需要 3 人月

RICE = (2000 × 3 × 0.8) / 3 = 1600
```

### ICE 评分

**用途**: 快速优先级评估，缺少数据时使用

**公式**:
```
ICE = Impact × Confidence × Ease
```

**评分维度**:

| 维度 | 范围 | 说明 | 示例问题 |
|------|------|------|---------|
| **Impact** | 1-10 | 对目标指标的影响 | "多大程度推动 OKR？" |
| **Confidence** | 1-10 | 成功/数据的确信度 | "有多大把握？" |
| **Ease** | 1-10 | 实施的难易程度 | "需要多少资源？" |

**示例**:
```yaml
功能: "移动端优化"
Impact: 8       # 高影响
Confidence: 7   # 较高信心
Ease: 5         # 中等难度

ICE = 8 × 7 × 5 = 280
```

### MoSCoW 分析

**用途**: 必须交付的功能集决策

**分类**:

| 类别 | 含义 | 标准 |
|------|------|------|
| **Must Have** | 必须有 | 没有它产品无法发布或没有价值 |
| **Should Have** | 应该有 | 重要但非必需，可以推迟到后续版本 |
| **Could Have** | 可以有 | 有了会更好，如果时间允许 |
| **Won't Have** | 不会有 | 明确排除，当前版本不考虑 |

**优先级排序**:
```
Must Have > Should Have > Could Have > Won't Have
```

### 加权评分

**用途**: 考虑多维度权衡的复杂决策

**公式**:
```
Score = ∑(Weight_i × Score_i)
```

**示例维度**:
```yaml
战略价值 (Strategy): 25%
用户价值 (Customer): 30%
技术成本 (Tech Cost): 20%
商业价值 (Business): 15%
风险 (Risk): 10%
```

## Core Process

### 步骤 1: 选择评分模型

```yaml
选择标准:
  使用 RICE 当:
    - 有用户数据
    - 可以估算工作量
    - 需要跨团队对比

  使用 ICE 当:
    - 早期探索阶段
    - 缺少定量数据
    - 需要快速决策

  使用 MoSCoW 当:
    - 确定发布范围
    - 资源硬约束
    - 时间紧迫

  使用加权评分当:
    - 多维度权衡
    - 需要定制标准
    - 复杂战略决策
```

### 步骤 2: 收集数据

#### RICE 数据收集

```yaml
Reach 评估方法:
  - 现有用户数据分析
  - 市场规模估算
  - 用户调研反馈
  - A/B 测试结果

Impact 评估标准:
  3 (巨大): 对 OKR 有决定性影响
  2 (大): 显著推动目标
  1 (中): 适度改善
  0.5 (小): 轻微改善
  0.25 (微): 几乎无影响

Confidence 评估:
  100%: 有历史数据支持
  80%: 有部分数据和验证
  50%: 基于假设和经验

Effort 评估:
  - 包含设计、开发、测试、部署
  - 以人月为单位
  - 考虑依赖和风险
```

#### ICE 数据收集

```yaml
快速评估指南:
  Impact (1-10):
    9-10: 改变游戏规则
    7-8: 显著改善
    5-6: 适度提升
    3-4: 轻微改善
    1-2: 几乎无影响

  Confidence (1-10):
    9-10: 有验证数据
    7-8: 有部分验证
    5-6: 基于经验
    3-4: 有假设
    1-2: 纯猜测

  Ease (1-10):
    9-10: 几乎零成本
    7-8: 低成本快速
    5-6: 中等成本
    3-4: 高成本
    1-2: 极难实现
```

### 步骤 3: 计算评分

```python
# RICE 计算
def calculate_rice(reach, impact, confidence, effort):
    return (reach * impact * confidence) / effort

# ICE 计算
def calculate_ice(impact, confidence, ease):
    return impact * confidence * ease

# 加权评分
def calculate_weighted(scores, weights):
    total = sum(s * w for s, w in zip(scores, weights))
    return total / sum(weights)
```

### 步骤 4: 生成报告

#### 评分排序

```markdown
## 功能优先级排序（RICE）

| 排名 | 功能 | RICE 分 | Reach | Impact | Confidence | Effort |
|------|------|---------|--------|--------|------------|--------|
| 1 | 用户批量导入 | 1600 | 2000 | 3 | 80% | 3 |
| 2 | 移动端优化 | 1200 | 5000 | 2 | 90% | 7.5 |
| 3 | API 限流 | 800 | 10000 | 1 | 100% | 12.5 |
```

#### 可视化

```markdown
## 优先级分布

**高优先级 (RICE > 1000)**: 3 个功能
**中优先级 (500 < RICE ≤ 1000)**: 5 个功能
**低优先级 (RICE ≤ 500)**: 8 个功能

## 工作量分布

**快速胜利 (Effort < 2)**: 4 个功能
**中等项目 (2 ≤ Effort < 6)**: 7 个功能
**大型项目 (Effort ≥ 6)**: 5 个功能
```

#### 敏感性分析

```markdown
## 假设变化影响

如果用户增长达到预期的 2 倍:
- 功能 A 的 RICE 从 800 → 1600
- 功能 B 的 RICE 从 600 → 1200

如果信心水平下降:
- 功能 C 的优先级可能下降到 D 类
```

## Scoring API

### 调用格式 - RICE

```yaml
scoring_engine:
  model: "RICE"
  items:
    - name: "用户批量导入"
      reach:
        value: 2000
        period: "quarter"
        source: "user_analytics"
      impact:
        value: 3
        rationale: "大幅提升用户留存"
      confidence:
        value: 80
        basis: "部分验证数据"
      effort:
        value: 3
        unit: "person_months"
        breakdown:
          design: 0.5
          development: 2
          testing: 0.3
          deployment: 0.2

    - name: "移动端优化"
      # ...
```

### 返回格式

```yaml
result:
  model: "RICE"
  total_items: 3
  scored_at: "[评分时间]"

  rankings:
    - rank: 1
      name: "用户批量导入"
      score: 1600
      components:
        reach: 2000
        impact: 3
        confidence: 0.8
        effort: 3
      category: "high_priority"

  summary:
    high_priority: 1
    medium_priority: 1
    low_priority: 1

  recommendations:
    - "优先实施 '用户批量导入'"
    - "'移动端优化' 可作为第二优先级"
    - "重新评估 'API 限流' 的收益假设"
```

## 安全风险评分

### CVSS 基础评分

**用途**: 安全漏洞风险评估

```yaml
基础指标:
  Attack Vector (AV):
    Network (N): 0.85
    Adjacent (A): 0.62
    Local (L): 0.55
    Physical (P): 0.2

  Attack Complexity (AC):
    Low (L): 0.77
    High (H): 0.44

  Privileges Required (PR):
    None (N): 0.85
    Low (L): 0.62
    High (H): 0.27

  User Interaction (UI):
    None (N): 0.85
    Required (R): 0.62

  Impact (C/I/A):
    High (H): 0.56
    Low (L): 0.22
    None (N): 0

公式:
  BaseScore = min(10, (((Impact) × 10) + Base) )

等级:
  9.0-10.0: 严重
  7.0-8.9: 高危
  4.0-6.9: 中危
  0.1-3.9: 低危
  0.0: 信息级
```

### DREAD 风险评估

**用途**: 威胁建模中的风险评估

```yaml
DREAD = (Damage + Reproducibility + Exploitability + Affected + Discoverability) / 5

各维度 (1-10 分):
  Damage: 潜在损害程度
  Reproducibility: 可复现性
  Exploitability: 可利用性
  Affected Users: 受影响用户比例
  Discoverability: 可发现性

等级:
  8-10: 高风险 - 必须修复
  5-7: 中风险 - 应该修复
  1-4: 低风险 - 可接受
```

## 最佳实践

✅ **DO**:
- 明确评分标准和假设
- 记录数据来源和依据
- 定期回顾和调整评分
- 使用定性定量结合
- 考虑团队容量和约束

❌ **DON'T**:
- 盲目信任分数，忽略上下文
- 使用不一致的标准
- 忽视定性因素
- 不记录假设和推理
- 过度优化评分模型

## 集成点

此引擎被以下技能使用：
- **priority-evaluator**: 功能优先级排序
- **impact-analyzer**: 漏洞影响评估
- **threat-modeling**: DREAD 风险评分
- **jtbd-analyzer**: 机会评分

## 测试示例

```bash
# RICE 评分
echo '{
  "model": "RICE",
  "items": [...]
}' | scoring-engine calculate

# ICE 快速评分
scoring-engine quick-score \
  --impact 8 \
  --confidence 7 \
  --ease 5

# MoSCoW 分类
scoring-engine moscow \
  --features features.json \
  --capacity 12
```
