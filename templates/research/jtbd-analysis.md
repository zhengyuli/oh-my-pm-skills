# {{project_name}} - JTBD 分析报告

**版本**: {{version}}
**日期**: {{date}}
**作者**: {{author}}
**分析方法**: JTBD (Jobs-to-be-Done)
**分析周期**: {{analysis_period}}

---

## 执行摘要

### 核心洞察

{{#each key_insights}}
{{@index}}. {{insight}}
   - 重要性: {{importance}}
   - 置信度: {{confidence}}
{{/each}}

### 待办任务摘要

**主要待办任务**: {{primary_job}}

**任务类型**: {{job_type}}

**动机强度**: {{motivation_strength}}/10

### 战略建议

{{#each strategic_recommendations}}
- **{{recommendation}}** (优先级: {{priority}})
{{/each}}

---

## 1. 研究背景

### 1.1 研究目标

{{research_objective}}

### 1.2 研究问题

{{#each research_questions}}
- **{{question}}**
  - 重要性: {{importance}}
{{/each}}

### 1.3 研究方法

**数据收集**:
{{#each data_collection}}
- **{{method}}**: {{description}} (样本量: {{sample_size}})
{{/each}}

**分析方法**:
{{#each analysis_methods}}
- {{method}}
{{/each}}

### 1.4 目标用户

{{#each target_users}}
- **{{segment}}**: {{description}}
  - 代表用户: {{representative_users}}
{{/each}}

---

## 2. 待办任务识别

### 2.1 主任务 (Main Job)

**任务陈述**: {{main_job_statement}}

**任务维度**:
- **功能性**: {{functional_dimension}}
- **情感性**: {{emotional_dimension}}
- **社会性**: {{social_dimension}}

### 2.2 任务背景

**触发情境**:
{{#each trigger_contexts}}
- **{{context}}**
  - 触发条件: {{trigger}}
  - 频率: {{frequency}}
  - 紧迫性: {{urgency}}
{{/each}}

**任务环境**:
{{#each job_context}}
- **{{aspect}}**: {{description}}
{{/each}}

### 2.3 任务类型分类

**任务类型**: {{job_type}}

**分类标准**:
{{#each classification_criteria}}
- **{{criterion}}**: {{value}}
{{/each}}

---

## 3. 待办任务拆解

### 3.1 任务结构

```
{{job_structure_diagram}}
```

### 3.2 核心任务

{{#each core_jobs}}

#### {{job_name}}

**任务描述**: {{job_description}}

**执行频率**: {{frequency}}

**重要性**: {{importance}}/10

**成功标准**:
{{#each success_criteria}}
- {{criterion}}
{{/each}}

**执行步骤**:
{{#each execution_steps}}
{{step}}. {{action}}
   - 前置条件: {{precondition}}
   - 输入: {{input}}
   - 输出: {{output}}
{{/each}}

**相关需求**:
{{#each related_needs}}
- **{{need}}** (强度: {{intensity}})
{{/each}}

{{/each}}

### 3.3 相关任务

**前置任务**:
{{#each prerequisite_jobs}}
- **{{job}}**: {{relationship}}
{{/each}}

**后置任务**:
{{#each subsequent_jobs}}
- **{{job}}**: {{relationship}}
{{/each}}

**并行任务**:
{{#each parallel_jobs}}
- **{{job}}**: {{relationship}}
{{/each}}

---

## 4. 用户动机分析

### 4.1 推动力 (Push)

**现状痛点**:
{{#each current_pain_points}}
- **{{pain_point}}**
  - 严重性: {{severity}}/10
  - 发生频率: {{frequency}}
  - 影响范围: {{impact_scope}}
  - 情绪反应: {{emotional_response}}
{{/each}}

**不满程度**: {{dissatisfaction_level}}/10

**改变动力**: {{change_motivation}}/10

### 4.2 吸引力 (Pull)

**解决方案吸引力**:
{{#each solution_appeal}}
- **{{appeal_factor}}**
  - 重要性: {{importance}}/10
  - 期望程度: {{desirability}}/10
{{/each}}

**理想状态**:
{{#each ideal_state}}
- {{aspect}}
{{/each}}

**憧憬价值**: {{aspiration_value}}/10

### 4.3 焦虑感 (Anxiety)

**采用障碍**:
{{#each adoption_barriers}}
- **{{barrier}}**
  - 担心程度: {{concern_level}}/10
  - 发生概率: {{probability}}/10
  - 缓解因素: {{mitigation}}
{{/each}}

**风险感知**: {{risk_perception}}/10

### 4.4 习惯性 (Habit)

**现有习惯**:
{{#each existing_habits}}
- **{{habit}}**
  - 强度: {{strength}}/10
  - 替代难度: {{substitution_difficulty}}/10
{{/each}}

**路径依赖**: {{path_dependency_level}}/10

### 4.5 动机综合评估

**四力量分析**:
```
推动力 (Push): {{push_score}}/10
吸引力 (Pull): {{pull_score}}/10
焦虑感 (Anxiety): {{anxiety_score}}/10 (反向)
习惯性 (Habit): {{habit_score}}/10 (反向)

净动机强度 = ({{push_score}} + {{pull_score}}) - ({{anxiety_score}} + {{habit_score}}) = {{net_motivation}}/20
```

**动机强度等级**: {{motivation_level}}

---

## 5. 雇佣标准分析

### 5.1 雇佣标准清单

{{#each hiring_criteria}}

#### {{criterion_name}}

**标准类型**: {{criterion_type}}

**重要性**: {{importance}}/10

**当前满意度**: {{current_satisfaction}}/10

**改进空间**: {{improvement_gap}}/10

**描述**: {{description}}

**评估指标**:
{{#each evaluation_metrics}}
- {{metric}} (权重: {{weight}}%)
{{/each}}

**衡量方法**:
{{#each measurement_methods}}
- {{method}}
{{/each}}

{{/each}}

### 5.2 标准优先级矩阵

| 优先级 | 标准 | 重要性 | 满意度 | 改进空间 |
|--------|------|--------|--------|---------|
{{#each prioritized_criteria}}
| {{priority}} | {{criterion}} | {{importance}}/10 | {{satisfaction}}/10 | {{gap}}/10 |
{{/each}}

### 5.3 必须具备 vs. 锦上添花

**必须具备 (Must-have)**:
{{#each must_have}}
- **{{criterion}}**:
  - 最低要求: {{minimum_requirement}}
  - 不满足后果: {{consequence}}
{{/each}}

**锦上添花 (Nice-to-have)**:
{{#each nice_to_have}}
- **{{criterion}}}}: {{description}}
{{/each}}

---

## 6. 解决方案评估

### 6.1 现有解决方案分析

{{#each existing_solutions}}

#### {{solution_name}}

**解决方案类型**: {{solution_type}}

**市场定位**: {{market_positioning}}

**雇佣标准满足度**:
| 标准 | 表现 | 评分 |
|------|------|------|
{{#each criterion_performance}}
| {{criterion}} | {{performance}} | {{score}}/10 |
{{/each}}

**优势**:
{{#each strengths}}
- {{.}}
{{/each}}

**劣势**:
{{#each weaknesses}}
- {{.}}
{{/each}}

**雇佣场景**:
{{#each hiring_scenarios}}
- **{{scenario}}**: {{description}}
  - 用户类型: {{user_type}}
  - 使用频率: {{frequency}}
{{/each}}

**不雇佣原因**:
{{#each non_hiring_reasons}}
- {{reason}} (频率: {{frequency}})
{{/each}}

**用户满意度**: {{satisfaction_score}}/10

**推荐意愿**: {{nps_score}}

{{/each}}

### 6.2 替代方案

**非产品类替代**:
{{#each non_product_alternatives}}
- **{{alternative}}}}
  - 采用率: {{adoption_rate}}%
  - 优缺点: {{pros_and_cons}}
{{/each}}

**不作为 (Do nothing)**:
- 比例: {{do_nothing_percentage}}%
- 原因: {{do_nothing_reasons}}

---

## 7. 用户旅程与触点

### 7.1 用户旅程地图

**旅程阶段**:
{{#each journey_stages}}

#### {{stage_name}}

**阶段目标**: {{stage_goal}}

**用户情绪**: {{user_emotion}} (1-10)

**关键活动**:
{{#each activities}}
- {{activity}}
{{/each}}

**触点**:
{{#each touchpoints}}
- **{{touchpoint}}**
  - 类型: {{type}}
  - 频率: {{frequency}}
  - 满意度: {{satisfaction}}/10
{{/each}}

**痛点**:
{{#each stage_pain_points}}
- {{pain_point}} (严重性: {{severity}})
{{/each}}

**机会**:
{{#each stage_opportunities}}
- {{opportunity}}
{{/each}}

**时间投入**: {{time_investment}}

**决策点**:
{{#each decision_points}}
- **{{decision}}**: {{description}}
  - 选择: {{options}}
{{/each}}

{{/each}}

### 7.2 关键时刻

**正向时刻**:
{{#each positive_moments}}
- **{{moment}}**
  - 重要性: {{importance}}/10
  - 当前表现: {{current_performance}}/10
  - 改进潜力: {{improvement_potential}}/10
{{/each}}

**负向时刻**:
{{#each negative_moments}}
- **{{moment}}**
  - 影响程度: {{impact}}/10
  - 解决紧迫性: {{urgency}}/10
{{/each}}

---

## 8. 用户细分

### 8.1 基于待办任务的细分

{{#each job_based_segments}}

#### {{segment_name}}

**待办任务**: {{job_to_be_done}}

**任务背景**: {{job_context}}

**任务紧迫性**: {{job_urgency}}/10

**任务频率**: {{job_frequency}}

**关键动机**:
{{#each key_motivations}}
- **{{motivation}}** (强度: {{intensity}}/10)
{{/each}}

**雇佣标准优先级**:
| 标准 | 重要性 |
|------|--------|
{{#each criteria_priorities}}
| {{criterion}} | {{importance}}/10 |
{{/each}}

**典型场景**:
{{#each typical_scenarios}}
- **{{scenario}}**: {{description}}
{{/each}}

**人口特征**:
{{#each demographics}}
- {{characteristic}}
{{/each}}

**占比**: {{segment_percentage}}%

**市场规模**: ${{market_size}}

{{/each}}

### 8.2 细分选择

**目标细分**: {{target_segment}}

**选择理由**:
{{#each target_segment_rationale}}
- {{reason}}
{{/each}}

---

## 9. 创新机会

### 9.1 未满足需求

{{#each unmet_needs}}

#### {{need_title}}

**需求描述**: {{need_description}}

**未满足程度**: {{unmet_level}}/10

**影响范围**: {{impact_scope}}

**出现频率**: {{frequency}}

**用户原话**:
{{#each user_quotes}}
- "{{quote}}"
{{/each}}

**解决方案方向**: {{solution_direction}}

**潜在价值**: {{potential_value}}

{{/each}}

### 9.2 雇佣标准差距

**最大差距**:
{{#each biggest_gaps}}
- **{{criterion}}**
  - 重要性: {{importance}}/10
  - 当前满意度: {{satisfaction}}/10
  - 差距: {{gap}}/10
  - 竞争对手表现: {{competitor_performance}}/10
{{/each}}

### 9.3 创新方向

**功能创新**:
{{#each functional_innovations}}
- **{{innovation}}**
  - 价值: {{value}}
  - 可行性: {{feasibility}}
  - 差异化: {{differentiation}}
{{/each}}

**情感创新**:
{{#each emotional_innovations}}
- **{{innovation}}**
  - 情感价值: {{emotional_value}}
  - 目标情绪: {{target_emotion}}
{{/each}}

**流程创新**:
{{#each process_innovations}}
- **{{innovation}}**
  - 效率提升: {{efficiency_gain}}
  - 体验改善: {{experience_improvement}}
{{/each}}

---

## 10. 价值主张设计

### 10.1 价值主张画布

**客户概况**:
{{#each customer_profile}}
- **{{aspect}}**: {{description}}
{{/each}}

**价值图谱**:
{{#each value_map}}
- **{{aspect}}**: {{description}}
{{/each}}

**契合度**:
{{#each fit_analysis}}
- **{{product_service}}** → **{{customer_need}}}}
  - 契合程度: {{fit_level}}/10
{{/each}}

### 10.2 价值主张陈述

**核心价值**: {{core_value_proposition}}

**支持要点**:
{{#each supporting_points}}
- **{{point}}**: {{description}}
{{/each}}

**独特性**: {{uniqueness}}

**可信证据**:
{{#each evidence}}
- {{evidence_item}}
{{/each}}

### 10.3 定位声明

**目标客户**: {{target_customer}}

**待办任务**: {{job_to_be_done}}

**差异化优势**: {{differentiation}}

**品牌个性**: {{brand_personality}}

---

## 11. 产品建议

### 11.1 产品功能优先级

**MVP 功能 (P0)**:
{{#each mvp_features}}
- **{{feature}}**
  - 雇佣标准: {{hiring_criterion}}
  - 用户价值: {{user_value}}
  - 业务价值: {{business_value}}
  - 开发成本: {{development_cost}}
{{/each}}

**次要功能 (P1)**:
{{#each secondary_features}}
- **{{feature}}**
  - 优先级: {{priority}}
  - 依赖: {{dependencies}}
{{/each}}

**未来功能 (P2)**:
{{#each future_features}}
- **{{feature}}}}
  - 时间表: {{timeline}}
{{/each}}

### 11.2 产品设计原则

{{#each design_principles}}
- **{{principle}}**: {{description}}
  - 应用场景: {{application}}
{{/each}}

### 11.3 成功指标

| 指标 | 目标值 | 测量方法 |
|------|--------|---------|
{{#each success_metrics}}
| {{metric}} | {{target}} | {{measurement}} |
{{/each}}

---

## 12. GTM 策略建议

### 12.1 目标市场

**初始市场**: {{initial_market}}

**市场进入策略**: {{entry_strategy}}

**扩张路径**:
{{#each expansion_path}}
- **{{stage}}**: {{market}} (时间: {{timeline}})
{{/each}}

### 12.2 营销信息

**核心信息**: {{core_message}}

**信息层级**:
{{#each message_hierarchy}}
- **{{level}}**: {{message}}
  - 目标受众: {{target_audience}}
  - 触发场景: {{trigger_context}}
{{/each}}

### 12.3 渠道策略

**推荐渠道**:
{{#each recommended_channels}}
- **{{channel}}**
  - 理由: {{rationale}}
  - 触达效率: {{reach_efficiency}}
  - 成本效益: {{cost_effectiveness}}
{{/each}}

---

## 13. 风险与挑战

### 13.1 产品风险

{{#each product_risks}}
- **{{risk}}**
  - 可能性: {{probability}}
  - 影响: {{impact}}
  - 缓解措施: {{mitigation}}
{{/each}}

### 13.2 市场风险

{{#each market_risks}}
- **{{risk}}**
  - 可能性: {{probability}}
  - 影响: {{impact}}
  - 应对策略: {{response}}
{{/each}}

### 13.3 验证假设

**关键假设**:
{{#each key_hypotheses}}
- **{{hypothesis}}**
  - 验证方法: {{validation_method}}
  - 验证时间: {{validation_timeline}}
  - 成功标准: {{success_criteria}}
{{/each}}

---

## 14. 下一步行动

### 14.1 验证计划

**待验证项**:
{{#each validation_items}}
- [ ] **{{item}}**
  - 方法: {{method}}
  - 负责人: {{owner}}
  - 截止: {{deadline}}
{{/each}}

### 14.2 开发优先级

**Sprint 1 (2周)**:
{{#each sprint1}}
- {{task}}
{{/each}}

**Sprint 2 (2周)**:
{{#each sprint2}}
- {{task}}
{{/each}}

### 14.3 研究跟进

**进一步研究**:
{{#each further_research}}
- **{{topic}}**
  - 目的: {{purpose}}
  - 方法: {{method}}
  - 预算: {{budget}}
{{/each}}

---

## 附录

### A. 访谈记录摘要

{{#each interview_summaries}}
- **{{participant}}** ({{role}}, {{company}})
  - 关键洞察: {{key_insights}}
  - 代表性语录: {{representative_quote}}
{{/each}}

### B. 调研数据

**样本量**: {{total_sample_size}}

**人口统计**:
{{#each demographics_data}}
- **{{segment}}}: {{count}} ({{percentage}}%)
{{/each}}

### C. 雇佣标准详细分析

{{#each detailed_criteria_analysis}}
- **{{criterion}}**
  - 测量方法: {{measurement_method}}
  - 基准: {{benchmark}}
  - 优秀表现: {{excellent_performance}}
{{/each}}

### D. 术语表

| 术语 | 定义 |
|------|------|
{{#each glossary}}
| {{term}} | {{definition}} |
{{/each}}

### E. 参考资料

{{#each references}}
- {{title}}: {{url}}
{{/each}}

---

*本报告由 JTBD Analyzer 自动生成*
*分析方法: Jobs-to-be-Done Framework*
*分析周期: {{analysis_period}}*
