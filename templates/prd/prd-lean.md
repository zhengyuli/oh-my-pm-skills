# {{project_name}} 产品需求文档 (Lean PRD)

**版本**: {{version}}
**日期**: {{date}}
**作者**: {{author}}
**状态**: {{status}}
**PRD 类型**: Lean (精简版)

---

## 1. 问题陈述

### 1.1 当前问题

{{problem_statement}}

### 1.2 影响范围

**影响用户**: {{affected_users}}
**发生频率**: {{frequency}}
**业务影响**: {{business_impact}}

### 1.3 为什么现在解决

{{urgency_rationale}}

---

## 2. 目标用户

### 2.1 用户画像

#### 主要用户

**姓名**: {{primary_persona_name}}

**角色**: {{primary_role}}

**痛点**:
{{#each primary_pain_points}}
- {{.}}
{{/each}}

**目标**:
{{#each primary_goals}}
- {{.}}
{{/each}}

**当前解决方案**: {{current_solution}}

### 2.2 用户细分

| 细分 | 描述 | 占比 | 优先级 |
|------|------|------|--------|
{{#each user_segments}}
| {{name}} | {{description}} | {{percentage}} | {{priority}} |
{{/each}}

---

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

---

## 4. 成功指标

### 4.1 关键指标

| 指标 | 当前值 | 目标值 | 测量方式 |
|------|--------|--------|---------|
{{#each success_metrics}}
| {{name}} | {{current}} | {{target}} | {{measurement}} |
{{/each}}

### 4.2 MVP 成功标准

{{#each mvp_success_criteria}}
- [ ] {{criterion}}
{{/each}}

---

## 5. 技术考量

### 5.1 技术栈

| 层级 | 技术 | 说明 |
|------|------|------|
{{#each tech_stack}}
| {{layer}} | {{technology}} | {{description}} |
{{/each}}

### 5.2 约束条件

{{#each constraints}}
- **{{type}}**: {{constraint}}
{{/each}}

### 5.3 风险评估

| 风险 | 可能性 | 影响 | 缓解措施 |
|------|--------|------|---------|
{{#each risks}}
| {{risk}} | {{probability}} | {{impact}} | {{mitigation}} |
{{/each}}

---

## 6. 用户体验

### 6.1 核心用户流程

```
{{#each user_flow}}
{{step_number}}. {{step}}
   {{#if condition}}
   条件: {{condition}}
   {{/if}}
   行动: {{action}}
   结果: {{outcome}}
{{/each}}
```

### 6.2 设计要求

{{#each design_requirements}}
- **{{aspect}}**: {{requirement}}
{{/each}}

---

## 7. 发布计划

### 7.1 MVP 范围

**目标发布日期**: {{mvp_launch_date}}

**包含功能**:
{{#each mvp_features}}
- {{feature}}
{{/each}}

**不包含功能**:
{{#each out_of_scope}}
- {{feature}} (原因: {{reason}})
{{/each}}

### 7.2 后续版本

| 版本 | 预期发布 | 主要功能 |
|------|---------|---------|
{{#each roadmap}}
| {{version}} | {{date}} | {{features}} |
{{/each}}

---

## 8. 风险和依赖

### 8.1 主要风险

{{#each major_risks}}
- **{{risk_title}}**
  - 描述: {{description}}
  - 概率: {{probability}}
  - 影响: {{impact}}
  - 缓解: {{mitigation}}
{{/each}}

### 8.2 依赖关系

{{#each dependencies}}
- **{{dependency}}**: {{description}} (截止: {{due_date}})
{{/each}}

### 8.3 假设清单

{{#each assumptions}}
- [ ] {{assumption}}
{{/each}}

---

## 附录

### A. 术语表

| 术语 | 定义 |
|------|------|
{{#each glossary}}
| {{term}} | {{definition}} |
{{/each}}

### B. 参考资料

{{#each references}}
- {{title}}: {{url}}
{{/each}}

### C. 变更历史

| 版本 | 日期 | 变更 | 作者 |
|------|------|------|------|
{{#each change_log}}
| {{version}} | {{date}} | {{changes}} | {{author}} |
{{/each}}

---

*本 PRD 由 PRD Generator 自动生成*
*模板类型: Lean PRD (8 节)*
