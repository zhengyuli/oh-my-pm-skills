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

> 所有评分模型的详细定义参见 `shared/scoring-models.yaml`

### RICE 评分

- **公式**: RICE = (Reach × Impact × Confidence) / Effort
- **用途**: 跨产品/功能对比优先级
- **详细定义**: shared/scoring-models.yaml#RICE

### ICE 评分

- **公式**: ICE = Impact × Confidence × Ease
- **用途**: 快速优先级评估，缺少数据时使用
- **详细定义**: shared/scoring-models.yaml#ICE

### MoSCoW 分析

- **用途**: 必须交付的功能集决策
- **分类**: Must Have > Should Have > Could Have > Won't Have
- **详细定义**: shared/scoring-models.yaml#MoSCoW

### DREAD 风险评估

- **公式**: DREAD = (Damage + Reproducibility + Exploitability + Affected + Discoverability) / 5
- **用途**: 安全威胁风险评估
- **详细定义**: shared/scoring-models.yaml#DREAD

### CVSS 漏洞评分

- **用途**: 安全漏洞影响评估
- **详细定义**: shared/scoring-models.yaml#CVSS

### 加权评分

- **公式**: Score = ∑(Weight_i × Score_i)
- **用途**: 多维度权衡的复杂决策
- **详细定义**: shared/scoring-models.yaml#Weighted

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

  使用 DREAD 当:
    - 安全威胁评估
    - 需要风险量化

  使用 CVSS 当:
    - 漏洞影响评估
    - 安全评分

  使用加权评分当:
    - 多维度权衡
    - 需要定制标准
```

### 步骤 2: 收集数据

使用评分模型的数据收集模板（参见 `shared/scoring-models.yaml`）

**快速参考**：

**RICE 数据收集**：
- Reach: 现有数据/市场规模/用户调研
- Impact: 3(巨大) / 2(大) / 1(中) / 0.5(小) / 0.25(微)
- Confidence: 100%(高) / 80%(中) / 50%(低)
- Effort: 人月，包含设计/开发/测试/部署

**ICE 数据收集**：
- Impact: 1-10 (9-10=改变游戏规则)
- Confidence: 1-10 (9-10=有验证数据)
- Ease: 1-10 (9-10=几乎零成本)

### 步骤 3: 计算评分

```python
# RICE 计算
def calculate_rice(reach, impact, confidence, effort):
    return (reach * impact * confidence) / effort

# ICE 计算
def calculate_ice(impact, confidence, ease):
    return impact * confidence * ease

# DREAD 计算
def calculate_dread(damage, reproducibility, exploitability, affected, discoverability):
    return (damage + reproducibility + exploitability + affected + discoverability) / 5

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
```

#### 敏感性分析

```markdown
## 假设变化影响

如果用户增长达到预期的 2 倍:
- 功能 A 的 RICE 从 800 → 1600
- 功能 B 的 RICE 从 600 → 1200
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
```

## 最佳实践

核心原则（详见 `shared/common-sections.yaml#best_practices.scoring`）：

✅ **DO**:
- 明确评分标准和假设
- 记录数据来源和依据
- 定期回顾和调整评分
- 使用定性定量结合

❌ **DON'T**:
- 盲目信任分数，忽略上下文
- 使用不一致的标准
- 忽视定性因素
- 不记录假设和推理

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

## 参考

- 评分模型定义: shared/scoring-models.yaml
  - RICE: shared/scoring-models.yaml#RICE
  - ICE: shared/scoring-models.yaml#ICE
  - MoSCoW: shared/scoring-models.yaml#MoSCoW
  - DREAD: shared/scoring-models.yaml#DREAD
  - CVSS: shared/scoring-models.yaml#CVSS
  - Weighted: shared/scoring-models.yaml#Weighted
- 最佳实践: shared/common-sections.yaml#best_practices.scoring
