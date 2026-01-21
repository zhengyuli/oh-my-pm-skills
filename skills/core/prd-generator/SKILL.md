---
name: prd-generator
description: 产品需求文档生成专家 - 支持Lean/Standard/Security三种模板，包含需求结构化、功能规格、验收标准
version: 1.0.0
author: oh-my-pm-skills
tags: [core, pm, prd, product-requirements, documentation, spec, user-stories]
allowed-tools: Read, Write, Edit
model: inherit
---

# PRD Generator

PRD 生成器负责将产品想法转化为结构化的产品需求文档（PRD），支持标准 PRD 和安全增强 PRD 两种模式。

## When to Use This Skill

用户请求以下功能时激活此技能：
- "写一个 PRD"
- "生成产品需求文档"
- "帮我写 PRD"
- "create PRD"
- "product requirements document"

## Core Process

### 步骤 1: 理解产品想法

**收集基本信息**:
```yaml
必需信息:
  - 产品名称
  - 核心问题/痛点
  - 目标用户
  - 核心功能

可选信息:
  - 目标指标
  - 技术约束
  - 时间线
  - 竞品信息
```

**调用 QA Engine**:
```yaml
qa_engine:
  action: "analyze"
  input_type: "product_idea"
  content: <用户输入>

  输出:
    - P0 问题: 必须澄清的核心信息
    - P1 问题: 重要的设计决策
    - P2 问题: 优化级别的细节
```

### 步骤 2: 选择 PRD 类型

```yaml
prd_types:
  prd-lean:
    描述: 精简 MVP PRD
    章节: 8
    适用: 早期验证、快速迭代

  prd-standard:
    描述: 标准 15 节 PRD
    章节: 15
    适用: 正式产品规划

  prd-security:
    描述: 安全增强 17 节 PRD
    章节: 17
    适用: 安全产品、合规要求

选择标准:
  - 是否是安全产品？ → prd-security
  - 是否需要正式规划？ → prd-standard
  - 是否快速 MVP？ → prd-lean
```

### 步骤 3: 收集详细内容

#### PRD Lean (8 节)

```yaml
1. 问题陈述:
   - 当前问题是什么？
   - 影响范围多大？
   - 为什么现在解决？

2. 目标用户:
   - 主要用户是谁？
   - 次要用户是谁？
   - 用户画像和痛点

3. 核心功能:
   - 3-5 个关键功能
   - 每个功能的描述
   - 验收标准

4. 成功指标:
   - 关键指标 (KPIs)
   - 目标值
   - 测量方式

5. 技术考量:
   - 技术栈选择
   - 约束条件
   - 风险评估

6. 用户体验:
   - 核心用户流程
   - 设计要求

7. 发布计划:
   - MVP 范围
   - 后续版本
   - 里程碑

8. 风险和依赖:
   - 主要风险
   - 依赖关系
   - 缓解措施
```

#### PRD Standard (15 节)

```yaml
包含 Lean 所有章节，额外增加:

9. 用户故事:
   - 格式化的用户故事
   - 优先级排序
   - 验收标准

10. 功能详细说明:
   - 完整功能列表
   - 功能优先级
   - 依赖关系

11. 非功能需求:
   - 性能要求
   - 可用性
   - 可扩展性
   - 兼容性

12. 技术规格:
   - 系统架构
   - API 设计
   - 数据模型

13. 设计要求:
   - UI/UX 要求
   - 设计系统
   - 品牌指南

14. 分析和指标:
   - 数据追踪需求
   - 分析工具
   - 报告需求

15. 预算和资源:
   - 团队配置
   - 预算估算
   - 时间线
```

#### PRD Security (17 节)

```yaml
包含 Standard 所有章节，额外增加:

16. 安全与隐私:
   - 威胁模型摘要
   - 安全需求
   - 隐私保护
   - 数据分类
   - 加密要求

17. 合规与审计:
   - 合规框架 (SOC2/ISO27001/GDPR)
   - 审计要求
   - 访问控制
   - 合规检查清单
```

### 步骤 4: 调用引擎生成 PRD

```yaml
工作流:
  1. qa_engine:
      action: "validate_content"
      check: "completeness"

  2. scoring_engine:
      action: "prioritize_features"
      model: "RICE"

  3. template_engine:
      action: "render"
      template: <选择的模板类型>
      variables: <收集的内容>

  4. document_engine:
      action: "create"
      type: "prd"
      output_path: "docs/prd/<project-name>-prd.md"
      auto_commit: true
```

### 步骤 5: 质量检查

```yaml
质量维度:
  内容完整性:
    - 所有必需章节齐全
    - 每个章节有实质性内容
    - 无空白或占位符

  需求明确性:
    - 验收标准清晰
    - 可量化指标
    - 无歧义表述

  可执行性:
    - 开发团队可理解
    - 测试团队可验证
    - 设计团队可参考

质量评分:
  - A (90-100): 可以直接进入开发
  - B (75-89): 需要少量澄清
  - C (60-74): 需要中等澄清
  - D (40-59): 需要大量澄清
  - F (0-39): 需要重写
```

## PRD 结构模板

### 元数据块

```markdown
---
title: "{{project_name}} 产品需求文档"
version: "{{version}}"
date: "{{date}}"
author: "{{author}}"
status: "{{status}}"
prd_type: "{{prd_type}}"
tags: [prd, {{category}}]
---

# {{project_name}} PRD

**版本**: {{version}}
**日期**: {{date}}
**作者**: {{author}}
**状态**: {{status}}
**PRD 类型**: {{prd_type}}

---
```

### 章节示例

#### 问题陈述

```markdown
## 1. 问题陈述

### 1.1 当前问题

{{problem_statement}}

### 1.2 影响范围

**影响用户**: {{affected_users_count}}+
**发生频率**: {{frequency}}
**业务影响**: {{business_impact}}

### 1.3 为什么现在解决

{{urgency_rationale}}
```

#### 目标用户

```markdown
## 2. 目标用户

### 2.1 用户画像

{{#each target_users}}

#### {{name}}

**描述**: {{description}}

**角色**: {{role}}

**痛点**:
{{#each pain_points}}
- {{.}}
{{/each}}

**目标**: {{goal}}

**技能水平**: {{skill_level}}

{{/each}}

### 2.2 用户细分

| 细分 | 比例 | 优先级 | 备注 |
|------|------|--------|------|
{{#each user_segments}}
| {{name}} | {{percentage}} | {{priority}} | {{notes}} |
{{/each}}
```

#### 核心功能

```markdown
## 3. 核心功能

{{#each key_features}}

### {{title}}

**优先级**: {{priority}}
**复杂度**: {{complexity}}

**描述**:
{{description}}

**用户价值**:
{{user_value}}

**验收标准**:
{{#each acceptance_criteria}}
- [ ] {{.}}
{{/each}}

{{#if technical_notes}}
**技术备注**:
{{technical_notes}}
{{/if}}

{{/each}}
```

#### 用户故事

```markdown
## 9. 用户故事

{{#each user_stories}}

### {{title}}

**格式**: 作为 {{role}}，我想要 {{want}}，以便 {{benefit}}

**优先级**: {{priority}}
**故事点**: {{story_points}}

**验收标准**:
{{#each acceptance_criteria}}
- [ ] {{.}}
{{/each}}

**依赖**: {{dependencies}}

**冲刺**: {{sprint}}

{{/each}}
```

#### 安全与隐私 (仅 PRD Security)

```markdown
## 16. 安全与隐私

### 16.1 威胁模型摘要

{{threat_model_summary}}

**主要威胁**:
{{#each top_threats}}
- {{type}}: {{description}} (风险: {{risk_level}})
{{/each}}

### 16.2 安全需求

{{#each security_requirements}}

#### {{category}}

- {{requirement}}
- **控制措施**: {{control}}
- **验证方法**: {{verification}}

{{/each}}

### 16.3 隐私保护

**数据收集**:
{{#each data_collection}}
- {{data_type}}: {{purpose}} ({{legal_basis}})
{{/each}}

**数据存储**:
- 加密: {{encryption_method}}
- 位置: {{storage_location}}
- 保留期: {{retention_period}}

### 16.4 数据分类

| 分类 | 数据类型 | 处理要求 |
|------|----------|----------|
{{#each data_classification}}
| {{level}} | {{examples}} | {{handling}} |
{{/each}}
```

#### 合规与审计 (仅 PRD Security)

```markdown
## 17. 合规与审计

### 17.1 合规框架

**适用框架**:
{{#each compliance_frameworks}}
- {{name}}: {{scope}}

**关键要求**:
{{#each key_requirements}}
- {{requirement}} ({{control}})
{{/each}}

{{/each}}

### 17.2 审计要求

**审计事件**:
{{#each audit_events}}
- {{event}}: {{description}} (保留: {{retention}})
{{/each}}

**审计报告**:
- 频率: {{report_frequency}}
- 接收方: {{recipients}}
- 格式: {{format}}

### 17.3 访问控制

**角色和权限**:
| 角色 | 权限 | 审批要求 |
|------|------|----------|
{{#each roles}}
| {{name}} | {{permissions}} | {{approval}} |
{{/each}}

### 17.4 合规检查清单

{{#each compliance_checklist}}
- [ ] {{item}} ({{requirement}})
{{/each}}
```

## 交互示例

### 示例 1: 精简 PRD

```
用户: 帮我写一个团队任务管理工具的 PRD

PRD Generator:
  1. 调用 QA Engine 生成澄清问题
  2. 收集: 问题、用户、功能、指标
  3. 使用 prd-lean 模板
  4. 生成文档: docs/prd/task-manager-prd.md
```

### 示例 2: 安全产品 PRD

```
用户: 我想做一个企业密钥管理系统

PRD Generator:
  1. 识别为安全产品
  2. 生成安全相关问题
  3. 使用 prd-security 模板
  4. 包含威胁建模章节
  5. 包含合规要求
  6. 生成完整安全 PRD
```

### 示例 3: 更新现有 PRD

```
用户: 更新这个 PRD，添加移动端支持

PRD Generator:
  1. 读取现有 PRD
  2. 识别变更点
  3. 调用 QA Engine 验证
  4. 更新相关章节
  5. 创建新版本
  6. Git commit with change log
```

## 集成点

**使用的引擎**:
- **qa-engine**: 验证内容完整性、生成澄清问题
- **scoring-engine**: 功能优先级评分
- **template-engine**: 渲染 PRD 模板
- **document-engine**: 生成最终文档

**与其他技能协作**:
- **priority-evaluator**: 功能优先级评估
- **threat-modeling**: 生成安全章节内容
- **compliance-checker**: 生成合规章节内容

## 最佳实践

✅ **DO**:
- 从 Lean PRD 开始，逐步完善
- 用 QA Engine 验证完整性
- 使用 Scoring Engine 排序功能
- 为每个功能定义验收标准
- 定期更新 PRD

❌ **DON'T**:
- 跳过问题收集直接生成
- 使用模糊的验收标准
- 忽视非功能需求
- 安全产品跳过安全章节
- 一次生成过多细节

## 输出格式

### 成功输出

```yaml
result:
  success: true
  prd:
    title: "{{project_name}} PRD"
    type: "{{prd_type}}"
    path: "docs/prd/{{project_slug}}-prd.md"
    version: "{{version}}"
    sections: {{section_count}}

  metadata:
    created_at: "{{timestamp}}"
    quality_score: {{score}}
    grade: "{{grade}}"

  next_steps:
    - "审阅 PRD 内容"
    - "与利益相关者确认"
    - "更新设计文档"
    - "开始开发冲刺规划"
```

### 需要澄清

```yaml
result:
  success: false
  reason: "missing_required_info"

  missing:
    - field: "target_users"
      priority: "P0"
      question: "主要目标用户是谁？"

    - field: "success_metrics"
      priority: "P1"
      question: "如何衡量成功？"

  next_action: "回答问题后重新生成"
```

## 测试场景

```bash
# 测试 1: 精简 PRD 生成
prd-generator generate \
  --type lean \
  --name "团队任务管理工具"

# 测试 2: 安全产品 PRD
prd-generator generate \
  --type security \
  --name "[产品名称]" \
  --include-threat-model

# 测试 3: 更新现有 PRD
prd-generator update \
  --file docs/prd/[产品名称]-prd.md \
  --add "mobile_support"
```
