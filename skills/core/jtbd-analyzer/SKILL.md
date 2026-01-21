---
name: jtbd-analyzer
description: JTBD用户动机分析专家 - 待办任务识别、四力量分析(Push/Pull/Anxiety/Habit)、雇佣标准评估
version: 1.0.0
author: oh-my-pm-skills
tags: [core, pm, jtbd, user-research, jobs-to-be-done, user-motivation, hiring-criteria]
allowed-tools: Read, Write, Edit
model: inherit
---

# JTBD Analyzer

JTBD (Jobs-to-be-Done) 分析器负责深入理解用户真正的动机、待办任务和期望结果，帮助 PM 设计更贴合用户需求的产品。

## When to Use This Skill

用户请求以下功能时激活此技能：
- "分析用户需求"
- "用户真正想要什么"
- "JTBD 分析"
- "理解用户动机"
- "用户为什么会用这个产品"

## Core Process

### 步骤 1: 理解分析场景

```yaml
场景类型:
  产品探索:
    - 新产品想法验证
    - 市场机会识别
    - 用户痛点挖掘

  功能优化:
    - 现有功能改进
    - 用户流失分析
    - 使用率提升

  竞品分析:
    - 用户迁移原因
    - 竞争优势定位
    - 差异化机会

  用户细分:
    - 用户群体划分
    - 精准定位
    - 个性化策略
```

### 步骤 2: 收集用户上下文

```yaml
用户画像:
  人口统计:
    - 年龄、性别、位置
    - 职业、行业、收入

  心理特征:
    - 价值观、动机
    - 痛点、目标
    - 决策因素

  行为模式:
    - 使用场景
    - 使用频率
    - 替代方案

  技术熟练度:
    - 数字化程度
    - 工具偏好
    - 学习能力
```

### 步骤 3: 应用 JTBD 框架

#### JTBD 核心问题

```yaml
四个核心问题:
  1. 用户想要完成什么任务？
     - 具体的任务是什么？
     - 任务的上下文是什么？
     - 任务的触发条件？

  2. 用户为什么想要完成这个任务？
     - 深层动机是什么？
     - 期望的结果是什么？
     - 不想要的结果是什么？

  3. 用户现在如何完成这个任务？
     - 当前解决方案是什么？
     - 有哪些替代方案？
     - 有哪些痛点？

  4. 阻碍用户切换的因素是什么？
     - 切换成本？
     - 习惯和依赖？
     - 风险担忧？
```

#### 力场分析 (Force Field Analysis)

```yaml
推动力 (Driving Forces):
  - 痛点压力: 当前方案的痛点有多大
  - 期望拉动: 新方案的吸引力
  - 社会压力: 他人使用的影响
  - 财务激励: 成本节约或收益

阻力 (Restraining Forces):
  - 习惯力量: 现有方案的惯性
  - 切换成本: 时间、金钱、学习成本
  - 风险担忧: 失败风险、不确定性
  - 技术壁垒: 技术门槛、兼容性

切换决策:
  当推动力 > 阻力时，用户会切换
```

#### 四维 JTBD 框架

```yaml
1. 功能维度 (Functional):
   - 用户想要实现的具体功能
   - 问题: "我想做 X"

2. 社会维度 (Social):
   - 用户想给别人看的形象
   - 问题: "我想让别人觉得我是 Y"

3. 情感维度 (Emotional):
   - 用户想要的感觉
   - 问题: "我想感觉到 Z"

4. 支持维度 (Support):
   - 用户需要的支持系统
   - 问题: "我需要什么帮助来完成"
```

### 步骤 4: 生成 JTBD 分析

#### Job Statement 格式

```
格式:
  "当我 {{situation}}，
   我想要 {{motivation}}，
   以便 {{expected_outcome}}，
   避免 {{unwanted_outcome}}"

示例:
  "当我需要快速与团队同步项目进度时，
   我想要一个简洁的可视化仪表盘，
   以便一眼了解所有关键指标，
   避免在多个工具间切换浪费时间"
```

#### 机会评分矩阵

```yaml
机会维度:
  重要性 (Importance):
    1-10 分
    - 多少用户有这个需求？
    - 这个需求有多重要？

  满意度 (Satisfaction):
    1-10 分
    - 现有解决方案多好？
    - 用户有多满意？

机会分数 = 重要性 + (10 - 满意度)

机会等级:
  15-18: 高机会 - 重大未满足需求
  12-14: 中机会 - 明显改进空间
  9-11: 低机会 - 小幅优化
  < 9: 无机会 - 需求已满足或不重要
```

#### 替代方案分析

```yaml
现有解决方案评估:
  方案 A:
    名称: {{name}}
    类型: {{type}} (竞品/手工流程/不作为)
    优点:
      - {{pro}}
    缺点:
      - {{con}}
    切换成本: {{switching_cost}}
    用户粘性: {{stickiness}}

  对比分析:
    维度: [功能、价格、易用性、性能、支持]
    我们的定位: {{positioning}}
```

### 步骤 5: 调用引擎生成报告

```yaml
工作流:
  1. qa_engine:
      action: "deep_dive"
      context: "user_motivation"
      生成深层探索问题

  2. scoring_engine:
      action: "opportunity_scoring"
      model: "jtbd_opportunity"
      评分: 重要性 × (10 - 满意度)

  3. template_engine:
      action: "render"
      template: "jtbd-analysis"
      生成结构化报告

  4. document_engine:
      action: "create"
      type: "jtbd_analysis"
      输出最终报告
```

## JTBD 分析模板

```markdown
# JTBD 分析报告: {{product_name}}

**分析日期**: {{date}}
**分析师**: {{author}}

---

## 执行摘要

{{summary}}

**核心发现**:
{{#each key_findings}}
- {{finding}}
{{/each}}

**机会评分**: {{opportunity_score}} / 18
**机会等级**: {{opportunity_level}}

---

## 用户画像

### 主要用户

**姓名**: {{persona_name}}
**年龄**: {{age}}
**职业**: {{occupation}}

**背景**:
{{background}}

**目标**:
{{#each goals}}
- {{.}}
{{/each}}

**痛点**:
{{#each pain_points}}
- {{.}}
{{/each}}

**当前解决方案**:
{{current_solution}}

---

## 核心待办任务

### 主任务 (Main Job)

{{#each jobs}}

#### {{title}}

**任务描述**:
{{description}}

**Job Statement**:
```
当我 {{situation}}，
我想要 {{motivation}}，
以便 {{expected_outcome}}，
避免 {{unwanted_outcome}}
```

**触发场景**:
{{#each triggers}}
- {{.}}
{{/each}}

**完成频率**: {{frequency}}

**重要性**: {{importance}} / 10

**现有满意度**: {{satisfaction}} / 10

**机会分数**: {{opportunity_score}} / 18

**任务维度**:
- 功能维度: {{functional}}
- 社会维度: {{social}}
- 情感维度: {{emotional}}
- 支持维度: {{support}}

{{/each}}

---

## 力场分析

### 推动用户的力量

{{#each driving_forces}}
#### {{name}}

**强度**: {{strength}} / 10

**描述**:
{{description}}

**影响**:
{{impact}}

{{/each}}

**总推动力**: {{total_driving}} / 40

### 阻碍用户的力量

{{#each restraining_forces}}
#### {{name}}

**强度**: {{strength}} / 10

**描述**:
{{description}}

**影响**:
{{impact}}

**缓解策略**:
{{mitigation}}

{{/each}}

**总阻力**: {{total_restraining}} / 40

### 切换决策

```
推动力: {{total_driving}}
阻力: {{total_restraining}}
净推力: {{net_force}}

{{#if net_force > 0}}
✅ 用户倾向切换
{{else}}
❌ 用户倾向保持现状
{{/if}}
```

---

## 替代方案分析

### 现有解决方案

{{#each alternatives}}

#### {{name}}

**类型**: {{type}}

**描述**:
{{description}}

**优点**:
{{#each pros}}
- {{.}}
{{/each}}

**缺点**:
{{#each cons}}
- {{.}}
{{/each}}

**使用场景**:
{{use_case}}

**切换成本**:
{{switching_cost}}

**用户粘性**: {{stickiness}} / 10

{{/each}}

### 我们的机会

**差异化定位**:
{{differentiation}}

**切入角度**:
{{#each entry_points}}
- {{angle}} ({{opportunity}} 分)
{{/each}}

---

## 机会矩阵

| 待办任务 | 重要性 | 满意度 | 机会分数 | 优先级 |
|---------|-------|--------|----------|--------|
{{#each opportunity_matrix}}
| {{job}} | {{importance}} | {{satisfaction}} | {{opportunity_score}} | {{priority}} |
{{/each}}

### 高机会区域 (15-18 分)

{{#each high_opportunities}}
- **{{job}}**: {{opportunity_score}} 分
  - 重要性: {{importance}}
  - 满意度: {{satisfaction}}
  - 策略: {{strategy}}
{{/each}}

### 中机会区域 (12-14 分)

{{#each medium_opportunities}}
- **{{job}}**: {{opportunity_score}} 分
  - 重要性: {{importance}}
  - 满意度: {{satisfaction}}
  - 策略: {{strategy}}
{{/each}}

---

## 用户旅程

### 当前旅程

```
{{#each journey_steps}}
{{step_number}}. {{name}}
   触发: {{trigger}}
   行为: {{action}}
   痛点: {{pain_point}}
   情绪: {{emotion}}
{{/each}}
```

### 改进后旅程

```
{{#each improved_steps}}
{{step_number}}. {{name}}
   触发: {{trigger}}
   行为: {{action}}
   价值: {{value}}
   情绪: {{emotion}} (从 {{previous_emotion}} 改善)
{{/each}}
```

---

## 产品建议

### 功能优先级

基于 JTBD 分析的功能优先级：

**立即实现** (高机会 + 高推动力):
{{#each immediate_features}}
- {{feature}} - {{job_addressed}}
{{/each}}

**近期规划** (中机会):
{{#each short_term_features}}
- {{feature}} - {{job_addressed}}
{{/each}}

**长期考虑** (低机会):
{{#each long_term_features}}
- {{feature}} - {{job_addressed}}
{{/each}}

### 营销信息

**核心价值主张**:
{{value_proposition}}

**目标营销语**:
{{#each marketing_messages}}
- {{message}} (针对 {{target_audience}})
{{/each}}

### 成功指标

{{#each success_metrics}}
- {{metric}}: {{target}} (当前: {{current}})
{{/each}}

---

## 附录

### 研究方法

{{research_methodology}}

### 数据来源

{{#each data_sources}}
- {{source}} ({{date}})
{{/each}}

### 假设和限制

{{#each assumptions}}
- {{assumption}}
{{/each}}

---

*本报告由 JTBD Analyzer 自动生成*
```

## 交互示例

### 示例 1: 新产品探索

```
用户: 分析一下企业协作工具的 JTBD 机会

JTBD Analyzer:
  1. 识别目标用户群体
  2. 深挖各群体的待办任务
  3. 分析现有方案的痛点
  4. 计算机会评分
  5. 生成产品机会建议
```

### 示例 2: 功能优化

```
用户: 用户为什么不常用我们的分享功能？

JTBD Analyzer:
  1. 分析分享任务的触发场景
  2. 评估当前方案的满意度
  3. 识别阻碍因素
  4. 提出改进建议
```

### 示例 3: 用户流失分析

```
用户: 用户为什么流失到竞品？

JTBD Analyzer:
  1. 力场分析
  2. 对比竞品的吸引力
  3. 识别我们的阻力点
  4. 提出挽留策略
```

## 集成点

**使用的引擎**:
- **qa-engine**: 深层动机探索问题
- **scoring-engine**: 机会评分
- **template-engine**: 报告渲染
- **document-engine**: 报告生成

**与其他技能协作**:
- **prd-generator**: PRD 中的用户洞察章节
- **priority-evaluator**: 基于机会分数的优先级

## 最佳实践

✅ **DO**:
- 关注"为什么"而非"是什么"
- 研究实际行为而非口头表达
- 考虑社交和情感因素
- 分析替代方案和切换成本
- 用数据验证假设

❌ **DON'T**:
- 只关注功能需求
- 忽视情感和社会因素
- 假设用户是理性的
- 忽视现有方案的惯性
- 只问"要什么"不问"为什么"

## 研究问题库

### 探索性问题

```yaml
任务理解:
  - "请描述上一次你做 {{task}} 的情况"
  - "你当时在想什么？"
  - "你希望达成什么结果？"

动机深挖:
  - "为什么这对你很重要？"
  - "如果不能完成这个任务会怎样？"
  - "完成这个任务给你带来了什么？"

痛点探索:
  - "现有方案有什么不满意的地方？"
  - "什么时候会觉得特别麻烦？"
  - "有没有想过放弃这个任务？"

切换因素:
  - "什么样的新产品会让你切换？"
  - "切换最大的顾虑是什么？"
  - "什么情况下会推荐给别人？"
```

## 输出格式

```yaml
result:
  success: true
  analysis:
    total_jobs: {{count}}
    high_opportunity: {{count}}
    medium_opportunity: {{count}}
    low_opportunity: {{count}}

  key_findings:
    - {{finding_1}}
    - {{finding_2}}

  recommendations:
    immediate:
      - {{recommendation_1}}
    short_term:
      - {{recommendation_2}}
```

## 测试场景

```bash
# 完整 JTBD 分析
jtbd-analyzer analyze \
  --product "企业协作工具" \
  --users "knowledge_workers"

# 机会评分
jtbd-analyzer score \
  --job "快速同步项目进度" \
  --importance 9 \
  --satisfaction 4

# 力场分析
jtbd-analyzer force-field \
  --product "我们的产品" \
  --alternative "竞品X"
```
