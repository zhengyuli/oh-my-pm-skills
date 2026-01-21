# {{project_name}} 产品需求文档 (Standard PRD)

**版本**: {{version}}
**日期**: {{date}}
**作者**: {{author}}
**状态**: {{status}}
**PRD 类型**: Standard (标准版)

---

## 文档控制

| 属性 | 值 |
|------|---|
| 项目名称 | {{project_name}} |
| 文档版本 | {{version}} |
| 创建日期 | {{date}} |
| 最后更新 | {{last_updated}} |
| 作者 | {{author}} |
| 审核者 | {{reviewers}} |
| 状态 | {{status}} |

---

## 变更历史

| 版本 | 日期 | 变更说明 | 作者 |
|------|------|---------|------|
{{#each change_log}}
| {{version}} | {{date}} | {{changes}} | {{author}} |
{{/each}}

---

## 1. 问题陈述

### 1.1 背景 context

{{background_context}}

### 1.2 当前问题

{{problem_statement}}

**问题类型**:
{{#each problem_types}}
- {{type}}
{{/each}}

### 1.3 影响分析

| 维度 | 描述 | 量化指标 |
|------|------|---------|
| 用户影响 | {{user_impact}} | {{user_impact_metric}} |
| 业务影响 | {{business_impact}} | {{business_impact_metric}} |
| 市场机会 | {{market_opportunity}} | {{market_size}} |

### 1.4 解决方案概述

{{solution_overview}}

**核心价值主张**: {{value_proposition}}

---

## 2. 目标用户

### 2.1 用户画像

{{#each personas}}

#### {{name}}

**基本信息**:
- 年龄: {{age}}
- 职业: {{occupation}}
- 行业: {{industry}}
- 技术水平: {{tech_level}}

**目标**:
{{#each goals}}
- {{.}}
{{/each}}

**痛点**:
{{#each pain_points}}
- {{.}}
{{/each}}

**行为特征**:
{{#each behaviors}}
- {{.}}
{{/each}}

**使用场景**:
{{#each use_cases}}
- {{scenario}}
{{/each}}

{{/each}}

### 2.2 用户细分

| 细分 | 描述 | 占比 | 优先级 | 特殊需求 |
|------|------|------|--------|---------|
{{#each user_segments}}
| {{name}} | {{description}} | {{percentage}} | {{priority}} | {{special_needs}} |
{{/each}}

### 2.3 用户旅程地图

```
阶段 1: {{stage_1_name}}
  触发: {{stage_1_trigger}}
  行为: {{stage_1_action}}
  痛点: {{stage_1_pain}}
  机会: {{stage_1_opportunity}}

阶段 2: {{stage_2_name}}
  触发: {{stage_2_trigger}}
  行为: {{stage_2_action}}
  痛点: {{stage_2_pain}}
  机会: {{stage_2_opportunity}}

阶段 3: {{stage_3_name}}
  触发: {{stage_3_trigger}}
  行为: {{stage_3_action}}
  痛点: {{stage_3_pain}}
  机会: {{stage_3_opportunity}}
```

---

## 3. 目标设定

### 3.1 产品目标

**产品愿景**: {{product_vision}}

**长期目标 (1-3 年)**:
{{#each long_term_goals}}
- {{goal}} (目标: {{target}}, 时间: {{timeline}})
{{/each}}

**短期目标 (3-6 个月)**:
{{#each short_term_goals}}
- {{goal}} (目标: {{target}}, 时间: {{timeline}})
{{/each}}

### 3.2 成功指标

#### 北极星指标

**核心指标**: {{north_star_metric}}

**定义**: {{north_star_definition}}

**当前值**: {{north_star_current}}
**目标值**: {{north_star_target}}
**目标时间**: {{north_star_timeline}}

#### 关键结果 (Key Results)

{{#each key_results}}

**KR {{@index}}**: {{title}}

| 指标 | 当前值 | 目标值 | 测量方式 |
|------|--------|--------|---------|
| 指标 | {{metric}} | {{current}} | {{target}} | {{measurement}} |

{{/each}}

### 3.3 反指标 (Guardrail Metrics)

{{#each guardrail_metrics}}
- **{{metric}}**: 不超过 {{threshold}}
{{/each}}

---

## 4. 用户故事

{{#each user_stories}}

### {{title}}

**格式**: 作为 {{role}}，我想要 {{want}}，以便 {{benefit}}

**优先级**: {{priority}}
**故事点**: {{story_points}}
**史诗**: {{epic}}

**验收标准**:
{{#each acceptance_criteria}}
- [ ] {{criterion}}
{{/each}}

**依赖**:
{{#each dependencies}}
- {{dependency}}
{{/each}}

**冲刺**: {{sprint}}

**笔记**: {{notes}}

{{/each}}

---

## 5. 功能详细说明

### 5.1 功能清单

| 功能 ID | 名称 | 优先级 | 复杂度 | 状态 | 负责人 |
|---------|------|--------|--------|------|--------|
{{#each feature_list}}
| {{id}} | {{name}} | {{priority}} | {{complexity}} | {{status}} | {{owner}} |
{{/each}}

### 5.2 功能详细

{{#each feature_details}}

#### {{feature_name}}

**功能 ID**: {{feature_id}}
**优先级**: {{priority}}
**复杂度**: {{complexity}}

**描述**:
{{description}}

**用户价值**:
{{user_value}}

**业务价值**:
{{business_value}}

**功能流程**:
```
{{#each flow_steps}}
{{step}}. {{description}}
  输入: {{input}}
  处理: {{process}}
  输出: {{output}}
{{/each}}
```

**验收标准**:
{{#each acceptance_criteria}}
- [ ] {{criterion}}
{{/each}}

**边缘情况**:
{{#each edge_cases}}
- {{case}}
{{/each}}

**依赖**:
{{#each dependencies}}
- {{dependency}}
{{/each}}

**技术考虑**:
{{technical_considerations}}

{{/each}}

### 5.3 功能优先级矩阵

```
高价值 + 低复杂度 (快速胜利):
{{#each quick_wins}}
- {{feature}}
{{/each}}

高价值 + 高复杂度 (大赌注):
{{#each big_bets}}
- {{feature}}
{{/each}}

低价值 + 低复杂度 (填充):
{{#each fill_ins}}
- {{feature}}
{{/each}}

低价值 + 高复杂度 (放弃):
{{#each wont_do}}
- {{feature}} (原因: {{reason}})
{{/each}}
```

---

## 6. 非功能需求

### 6.1 性能要求

| 指标 | 要求 | 测量方法 |
|------|------|---------|
{{#each performance_requirements}}
| {{metric}} | {{requirement}} | {{measurement}} |
{{/each}}

### 6.2 可用性

| 指标 | 目标 | 当前 |
|------|------|------|
{{#each availability_targets}}
| {{metric}} | {{target}} | {{current}} |
{{/each}}

### 6.3 可扩展性

{{#each scalability_requirements}}
- **{{aspect}}**: {{requirement}}
{{/each}}

### 6.4 兼容性

**浏览器支持**:
{{#each browser_support}}
- {{browser}} {{version_min}}+
{{/each}}

**设备支持**:
{{#each device_support}}
- {{device_type}} ({{os}} {{version_min}}+)
{{/each}}

### 6.5 安全性

{{#each security_requirements}}
- **{{aspect}}**: {{requirement}}
{{/each}}

### 6.6 可访问性

**合规标准**: {{accessibility_standard}}

{{#each accessibility_features}}
- {{feature}}
{{/each}}

---

## 7. 技术规格

### 7.1 系统架构

```
{{architecture_diagram}}
```

**架构层次**:
{{#each architecture_layers}}
- **{{layer}}**: {{description}}
{{/each}}

### 7.2 技术栈

| 层级 | 技术 | 版本 | 用途 |
|------|------|------|------|
{{#each tech_stack}}
| {{layer}} | {{technology}} | {{version}} | {{purpose}} |
{{/each}}

### 7.3 API 设计

#### REST API 端点

{{#each api_endpoints}}

##### {{endpoint}}

**方法**: `{{method}}`
**路径**: `{{path}}`
**描述**: {{description}}

**请求**:
```json
{{request_example}}
```

**响应**:
```json
{{response_example}}
```

**认证**: {{authentication}}
**速率限制**: {{rate_limit}}

{{/each}}

### 7.4 数据模型

{{#each data_models}}

#### {{model_name}}

**描述**: {{description}}

**字段**:
| 字段 | 类型 | 约束 | 描述 |
|------|------|------|------|
{{#each fields}}
| {{name}} | {{type}} | {{constraints}} | {{description}} |
{{/each}}

**关系**:
{{#each relationships}}
- 与 {{related_model}} 的 {{relationship_type}} 关系
{{/each}}

{{/each}}

### 7.5 数据存储

| 数据类型 | 存储 | 容量 | 备份 |
|---------|------|------|------|
{{#each data_storage}}
| {{type}} | {{technology}} | {{capacity}} | {{backup}} |
{{/each}}

---

## 8. 设计要求

### 8.1 设计系统

**设计规范**: {{design_system}}

### 8.2 UI/UX 要求

{{#each ux_requirements}}
- **{{aspect}}**: {{requirement}}
{{/each}}

### 8.3 品牌指南

{{#each brand_guidelines}}
- **{{element}}**: {{guideline}}
{{/each}}

### 8.4 响应式设计

**断点**:
{{#each breakpoints}}
- {{device}}: {{width}}px
{{/each}}

---

## 9. 分析和指标

### 9.1 数据追踪

**追踪工具**: {{analytics_tool}}

### 9.2 关键事件

{{#each tracking_events}}
| 事件 | 参数 | 触发条件 |
|------|------|---------|
| {{event_name}} | {{parameters}} | {{trigger}} |
{{/each}}

### 9.3 仪表盘

**必看指标**:
{{#each dashboard_metrics}}
- {{metric}} ({{type}})
{{/each}}

### 9.4 报告需求

{{#each reporting_requirements}}
- **{{report}}**: {{frequency}} ({{format}})
{{/each}}

---

## 10. 发布计划

### 10.1 里程碑

| 阶段 | 目标 | 日期 | 状态 |
|------|------|------|------|
{{#each milestones}}
| {{phase}} | {{objective}} | {{date}} | {{status}} |
{{/each}}

### 10.2 MVP 定义

**MVP 范围**:
{{#each mvp_features}}
- {{feature}}
{{/each}}

**MVP 成功标准**:
{{#each mvp_success_criteria}}
- [ ] {{criterion}}
{{/each}}

### 10.3 Alpha 版本

**目标用户**: {{alpha_users}}
**功能**: {{alpha_features}}
**日期**: {{alpha_date}}

### 10.4 Beta 版本

**目标用户**: {{beta_users}}
**功能**: {{beta_features}}
**日期**: {{beta_date}}

### 10.5 正式发布

**发布日期**: {{launch_date}}
**发布策略**: {{launch_strategy}}

### 10.6 后续版本

| 版本 | 预期发布 | 主要功能 |
|------|---------|---------|
{{#each future_versions}}
| {{version}} | {{date}} | {{features}} |
{{/each}}

---

## 11. 风险评估

### 11.1 技术风险

| 风险 | 可能性 | 影响 | 缓解措施 | 负责人 |
|------|--------|------|---------|--------|
{{#each technical_risks}}
| {{risk}} | {{probability}} | {{impact}} | {{mitigation}} | {{owner}} |
{{/each}}

### 11.2 产品风险

| 风险 | 可能性 | 影响 | 缓解措施 | 负责人 |
|------|--------|------|---------|--------|
{{#each product_risks}}
| {{risk}} | {{probability}} | {{impact}} | {{mitigation}} | {{owner}} |
{{/each}}

### 11.3 业务风险

| 风险 | 可能性 | 影响 | 缓解措施 | 负责人 |
|------|--------|------|---------|--------|
{{#each business_risks}}
| {{risk}} | {{probability}} | {{impact}} | {{mitigation}} | {{owner}} |
{{/each}}

---

## 12. 预算和资源

### 12.1 团队配置

| 角色 | 人数 | 负责内容 |
|------|------|---------|
{{#each team}}
| {{role}} | {{count}} | {{responsibilities}} |
{{/each}}

### 12.2 预算估算

| 类别 | 预算 | 说明 |
|------|------|------|
{{#each budget}}
| {{category}} | ${{amount}} | {{description}} |
{{/each}}

**总预算**: ${{total_budget}}

### 12.3 时间线

| 阶段 | 开始 | 结束 | 天数 |
|------|------|------|------|
{{#each timeline}}
| {{phase}} | {{start}} | {{end}} | {{days}} |
{{/each}}

**总工期**: {{total_duration}}

---

## 13. 依赖关系

### 13.1 内部依赖

{{#each internal_dependencies}}
- **{{dependency}}**: {{description}} (负责人: {{owner}}, 截止: {{due_date}})
{{/each}}

### 13.2 外部依赖

{{#each external_dependencies}}
- **{{dependency}}**: {{description}} (供应商: {{vendor}}, 截止: {{due_date}})
{{/each}}

### 13.3 技术依赖

{{#each technical_dependencies}}
- **{{library}}**: {{version}} (用途: {{purpose}})
{{/each}}

---

## 14. 假设和约束

### 14.1 假设

{{#each assumptions}}
- **{{assumption}}**: {{rationale}}
{{/each}}

### 14.2 约束

{{#each constraints}}
- **{{constraint_type}}**: {{constraint}}
{{/each}}

---

## 15. 附录

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

### C. 相关文档

{{#each related_documents}}
- [{{title}}]({{url}})
{{/each}}

### D. 审批记录

| 角色 | 姓名 | 审批意见 | 日期 |
|------|------|---------|------|
{{#each approvals}}
| {{role}} | {{name}} | {{comment}} | {{date}} |
{{/each}}

---

*本 PRD 由 PRD Generator 自动生成*
*模板类型: Standard PRD (15 节)*
