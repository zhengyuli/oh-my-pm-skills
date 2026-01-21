# {{project_name}} - 数据分析报告

**报告日期**: {{date}}
**分析周期**: {{analysis_period}}
**分析师**: {{author}}

---

## 执行摘要

### 关键发现

{{#each key_findings}}
{{@index}}. {{finding}}
{{/each}}

### 核心指标速览

| 指标 | 当前值 | 上期 | 变化 | 趋势 |
|------|-------|------|------|------|
{{#each metrics_summary}}
| {{name}} | {{current}} | {{previous}} | {{change}} | {{trend}} |
{{/each}}

### 产品健康度评分

**总体评分**: {{health_score}} / 100

| 维度 | 评分 | 状态 |
|------|------|------|
| 用户增长 | {{growth_score}} | {{growth_status}} |
| 用户参与 | {{engagement_score}} | {{engagement_status}} |
| 用户留存 | {{retention_score}} | {{retention_status}} |
| 营收表现 | {{revenue_score}} | {{revenue_status}} |

---

## 用户分析

### 用户规模

#### 总体用户

| 指标 | 值 |
|------|---|
| 累计用户数 | {{total_users}} |
| 活跃用户数 (MAU) | {{mau}} |
| 日活跃用户数 (DAU) | {{dau}} |
| DAU/MAU 比率 | {{dau_mau_ratio}}% |

#### 用户增长

{{#if user_growth_chart}}
```chart
type: line
title: 用户增长趋势
x-axis: {{user_growth_chart.x_axis}}
y-axis: 用户数
series: {{user_growth_chart.series}}
```
{{/if}}

| 期间 | 新增用户 | 流失用户 | 净增长 | 增长率 |
|------|---------|---------|--------|--------|
{{#each user_growth_table}}
| {{period}} | {{new_users}} | {{churned_users}} | {{net_growth}} | {{growth_rate}}% |
{{/each}}

### 用户参与度

#### 会话分析

| 指标 | 平均值 | 中位数 | P90 |
|------|-------|--------|-----|
| 会话时长 | {{avg_duration}} | {{median_duration}} | {{p90_duration}} |
| 会话频率/周 | {{avg_frequency}} | {{median_frequency}} | {{p90_frequency}} |
| 页面深度 | {{avg_depth}} | {{median_depth}} | {{p90_depth}} |

#### 功能使用率

| 功能 | 使用用户 | 使用率 | 趋势 |
|------|---------|--------|------|
{{#each feature_usage}}
| {{feature}} | {{users}} | {{usage_rate}}% | {{trend}} |
{{/each}}

### 用户留存

#### 留存曲线

{{#if retention_chart}}
```chart
type: line
title: 留存率曲线
x-axis: 天数
y-axis: 留存率 (%)
series: {{retention_chart.series}}
```
{{/if}}

#### 同期群分析

| 获客周期 | D1 | D7 | D30 | D60 | D90 |
|---------|-----|-----|------|-----|-----|
{{#each cohort_table}}
| {{period}} | {{d1}}% | {{d7}}% | {{d30}}% | {{d60}}% | {{d90}}% |
{{/each}}

#### 留存热力图

{{#if retention_heatmap}}
```
{{retention_heatmap}}
```
{{/if}}

### 用户分层

#### 按活跃度

| 分层 | 定义 | 用户数 | 占比 | 特征 |
|------|------|--------|------|------|
{{#each engagement_segments}}
| {{name}} | {{definition}} | {{users}} | {{percentage}}% | {{characteristics}} |
{{/each}}

#### 按价值

| 分层 | 定义 | 用户数 | 营收贡献 | 留存率 |
|------|------|--------|---------|--------|
{{#each value_segments}}
| {{name}} | {{definition}} | {{users}} | {{revenue_contribution}}% | {{retention_rate}}% |
{{/each}}

---

## 转化分析

### 漏斗分析

#### {{funnel_name}} 漏斗

| 步骤 | 进入用户 | 完成用户 | 转化率 | 累计转化率 |
|------|---------|---------|--------|-----------|
{{#each funnel_steps}}
| {{name}} | {{enter}} | {{complete}} | {{conversion_rate}}% | {{cumulative_rate}}% |
{{/each}}

**总体转化率**: {{overall_conversion}}%

#### 漏斗可视化

```
{{funnel_visualization}}
```

#### 流失分析

| 步骤 | 流失用户 | 流失率 | 主要流失原因 |
|------|---------|--------|-------------|
{{#each dropoff_analysis}}
| {{step}} | {{dropped_users}} | {{dropoff_rate}}% | {{reasons}} |
{{/each}}

### 关键转化事件

#### 注册转化

| 指标 | 值 |
|------|---|
| 访问注册页 | {{signup_visits}} |
| 开始注册 | {{signup_started}} |
| 完成注册 | {{signup_completed}} |
| 注册转化率 | {{signup_rate}}% |

#### 付费转化

| 指标 | 值 |
|------|---|
| 活跃用户 | {{active_users}} |
| 访问付费页 | {{pricing_visits}} |
| 开始付费 | {{payment_started}} |
| 完成付费 | {{payment_completed}} |
| 付费转化率 | {{payment_rate}}% |

---

## A/B 测试分析

{{#each ab_tests}}

### {{name}}

**测试状态**: {{status}}
**测试周期**: {{start_date}} - {{end_date}}
**样本量**: {{sample_size}}

#### 结果对比

| 指标 | 对照组 | 实验组 | 绝对差异 | 相对提升 |
|------|--------|--------|----------|----------|
{{#each metrics}}
| {{metric}} | {{control}} | {{treatment}} | {{absolute_diff}} | {{relative_lift}}% |
{{/each}}

#### 统计显著性

| 维度 | 值 |
|------|---|
| P 值 | {{p_value}} |
| 显著性 | {{significance}} |
| 置信度 | {{confidence}}% |
| 置信区间 | [{{ci_lower}}, {{ci_upper}}] |
| 效应量 (Cohen's d) | {{effect_size}} |

#### 结论与建议

**结论**: {{conclusion}}

**建议**: {{recommendation}}

**下一步**: {{next_steps}}

{{/each}}

---

## 营收分析

### 营收概览

| 指标 | 当前期 | 上期 | 变化 | 同比 |
|------|-------|------|------|------|
| 总收入 | ${{total_revenue}} | ${{prev_revenue}} | {{revenue_change}}% | {{revenue_yoy}}% |
| ARPU | ${{arpu}} | ${{prev_arpu}} | {{arpu_change}}% | - |
| ARPPU | ${{arppu}} | ${{prev_arppu}} | {{arppu_change}}% | - |

### 营收构成

{{#if revenue_breakdown_chart}}
```chart
type: stacked_bar
title: 营收构成
x-axis: 月份
y-axis: 营收 ($)
series: {{revenue_breakdown_chart.series}}
```
{{/if}}

| 收入类型 | 本期收入 | 占比 | 上期收入 | 变化 |
|---------|---------|------|---------|------|
{{#each revenue_breakdown}}
| {{type}} | ${{amount}} | {{percentage}}% | ${{prev_amount}} | {{change}}% |
{{/each}}

### 用户分层营收

| 用户分层 | 用户数 | ARPU | 总营收 | 营收占比 |
|---------|--------|------|--------|---------|
{{#each segment_revenue}}
| {{segment}} | {{users}} | ${{arpu}} | ${{revenue}} | {{percentage}}% |
{{/each}}

### LTV & CAC

| 指标 | 值 |
|------|---|
| 平均 LTV | ${{ltv}} |
| CAC | ${{cac}} |
| LTV/CAC 比率 | {{ltv_cac_ratio}} |
| 回本周期 | {{payback_period}} 个月 |

---

## 异常检测

### 检测到的异常

{{#each anomalies}}

#### 异常: {{title}}

**类型**: {{type}}
**严重性**: {{severity}}
**发生时间**: {{detected_at}}

**描述**: {{description}}

**影响**:
- 影响指标: {{affected_metrics}}
- 影响范围: {{impact_scope}}
- 估计影响: {{estimated_impact}}

**可能原因**:
{{#each possible_causes}}
- {{cause}}
{{/each}}

**建议行动**:
{{#each recommended_actions}}
- [ ] {{action}}
{{/each}}

{{/each}}

---

## 用户行为洞察

### 用户路径分析

**最常见路径**:
{{#each common_paths}}
{{@index}}. {{path}} ({{percentage}}% 用户)
{{/each}}

**意外发现**:
{{#each unexpected_paths}}
- {{path}}: {{insight}}
{{/each}}

### 使用模式

#### 使用时间分布

| 时段 | 活跃用户 | 占比 | 主要行为 |
|------|---------|------|---------|
{{#each time_distribution}}
| {{time_slot}} | {{active_users}} | {{percentage}}% | {{main_behavior}} |
{{/each}}

#### 使用设备分布

| 设备类型 | 活跃用户 | 占比 | 会话时长 |
|---------|---------|------|---------|
{{#each device_distribution}}
| {{device}} | {{users}} | {{percentage}}% | {{avg_duration}} |
{{/each}}

---

## 竞品对比

### 关键指标对比

| 指标 | 我们 | 竞品 A | 竞品 B |
|------|------|--------|--------|
{{#each competitor_comparison}}
| {{metric}} | {{us}} | {{competitor_a}} | {{competitor_b}} |
{{/each}}

### 市场份额

| 期间 | 我们的市场份额 | 变化 |
|------|--------------|------|
{{#each market_share}}
| {{period}} | {{share}}% | {{change}}% |
{{/each}}

---

## 行动建议

### 立即行动 (本周)

{{#each immediate_actions}}
- [ ] **{{title}}**
  - 理由: {{rationale}}
  - 预期影响: {{expected_impact}}
  - 负责人: {{owner}}
  - 截止: {{due_date}}
{{/each}}

### 短期优化 (本月)

{{#each short_term_actions}}
- [ ] **{{title}}**
  - 理由: {{rationale}}
  - 预期影响: {{expected_impact}}
  - 负责人: {{owner}}
{{/each}}

### 中期规划 (本季度)

{{#each medium_term_actions}}
- [ ] **{{title}}**
  - 理由: {{rationale}}
  - 预期影响: {{expected_impact}}
  - 负责人: {{owner}}
{{/each}}

---

## 附录

### 数据说明

**数据来源**: {{data_sources}}

**数据质量**:
- 完整性: {{completeness}}%
- 准确性: {{accuracy}}%
- 时效性: {{timeliness}}

**统计说明**:
- 置信水平: {{confidence_level}}%
- 显著性阈值: {{significance_threshold}}

### 技术说明

**分析方法**:
{{#each analysis_methods}}
- {{method}}: {{description}}
{{/each}}

**工具**:
{{#each tools}}
- {{name}}: {{purpose}}
{{/each}}

---

*本报告由 Analytics Engine 自动生成*
*分析框架: 数据驱动产品决策*
