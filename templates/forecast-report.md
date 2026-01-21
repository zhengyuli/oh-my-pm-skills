# {{project_name}} - 预测报告

**报告日期**: {{date}}
**预测期间**: {{forecast_period}}
**分析师**: {{author}}

---

## 执行摘要

### 预测概览

| 维度 | 基准情景 | 乐观情景 | 悲观情景 |
|------|---------|---------|---------|
{{#each forecast_summary}}
| {{metric}} | {{baseline}} | {{optimistic}} | {{pessimistic}} |
{{/each}}

### 核心假设

{{#each key_assumptions}}
- {{assumption}} (基准: {{baseline_value}})
{{/each}}

### 置信区间

| 指标 | P50 | P80 | P95 |
|------|-----|-----|-----|
{{#each confidence_intervals}}
| {{metric}} | {{p50}} | {{p80}} | {{p95}} |
{{/each}}

---

## 市场规模预测

### TAM (总可寻址市场)

#### 方法

**方法**: {{tam_methodology}}
**数据来源**: {{tam_data_sources}}

#### TAM 计算

{{#if tam_approach_bottomup}}

**自下而上法**:

| 细分市场 | 客户数量 | 人均年消费 | 市场规模 |
|---------|---------|-----------|---------|
{{#each tam_segments}}
| {{name}} | {{customer_count}} | {{arpu}} | ${{market_size}} |
{{/each}}

**TAM 总计**: ${{tam_total}}

{{/if}}

{{#if tam_approach_topdown}}

**自上而下法**:

| 层级 | 定义 | 规模 |
|------|------|------|
{{#each tam_topdown}}
| {{level}} | {{definition}} | ${{size}} |
{{/each}}

**TAM 总计**: ${{tam_total}}

{{/if}}

#### TAM 增长预测

| 年份 | TAM | 增长率 | 驱动因素 |
|------|-----|--------|---------|
{{#each tam_forecast}}
| {{year}} | ${{size}} | {{growth_rate}}% | {{drivers}} |
{{/each}}

### SAM (可服务市场)

#### 可触达性分析

**可触达比例**: {{reachable_percentage}}%

| 限制因素 | 影响 | 应对策略 |
|---------|------|---------|
{{#each sam_constraints}}
| {{factor}} | {{impact}} | {{mitigation}} |
{{/each}}

#### SAM 计算

**SAM = TAM × 可触达比例**

| 年份 | TAM | 可触达比例 | SAM |
|------|-----|-----------|-----|
{{#each sam_forecast}}
| {{year}} | ${{tam}} | {{reachable}}% | ${{sam}} |
{{/each}}

### SOM (可获得市场)

#### 市场份额目标

| 年份 | SAM | 目标份额 | SOM |
|------|-----|---------|-----|
{{#each som_forecast}}
| {{year}} | ${{sam}} | {{market_share}}% | ${{som}} |
{{/each}}

#### 市场份额策略

{{#each market_share_strategy}}
- **{{phase}}**: {{description}}
  - 目标份额: {{target_share}}%
  - 关键行动: {{key_actions}}
{{/each}}

### 竞争格局

| 竞争对手 | 当前份额 | 预测份额 | 策略 |
|---------|---------|---------|------|
{{#each competitors}}
| {{name}} | {{current_share}}% | {{forecast_share}}% | {{strategy}} |
{{/each}}

---

## 用户增长预测

### 预测模型

**模型选择**: {{growth_model}}

**选择理由**: {{model_rationale}}

**模型参数**:
{{#each model_parameters}}
- {{name}}: {{value}}
{{/each}}

### 增长预测

#### 基准情景

| 月份 | 用户数 | 新增 | 流失 | 净增长 | 增长率 |
|------|-------|------|------|--------|--------|
{{#each baseline_growth}}
| {{month}} | {{total_users}} | {{new_users}} | {{churned}} | {{net_growth}} | {{growth_rate}}% |
{{/each}}

#### 情景对比

{{#if growth_comparison_chart}}
```chart
type: line
title: 用户增长情景对比
x-axis: 月份
y-axis: 用户数
series: {{growth_comparison_chart.series}}
```
{{/if}}

| 月份 | 悲观 | 基准 | 乐观 |
|------|------|------|------|
{{#each growth_scenarios}}
| {{month}} | {{pessimistic}} | {{baseline}} | {{optimistic}} |
{{/each}}

### 关键增长驱动因素

| 驱动因素 | 影响 | 敏感性 | 优化空间 |
|---------|------|--------|---------|
{{#each growth_drivers}}
| {{name}} | {{impact}} | {{sensitivity}} | {{optimization_potential}} |
{{/each}}

### 用户分层预测

{{#if user_segments_forecast}}

#### 按用户类型

| 用户类型 | 当前期 | 预测期 | 增长率 | 主要策略 |
|---------|-------|--------|--------|---------|
{{#each segment_forecast}}
| {{segment}} | {{current}} | {{forecast}} | {{growth_rate}}% | {{strategy}} |
{{/each}}

#### 按获客渠道

| 渠道 | 当前期 | 预测期 | CAC | ROI |
|------|-------|--------|-----|-----|
{{#each channel_forecast}}
| {{channel}} | {{current}} | {{forecast}} | ${{cac}} | {{roi}}% |
{{/each}}

{{/if}}

### 流失预测

| 期间 | 新增用户 | 预计流失 | 流失率 | 留存率 |
|------|---------|---------|--------|--------|
{{#each churn_forecast}}
| {{period}} | {{new_users}} | {{churned}} | {{churn_rate}}% | {{retention_rate}}% |
{{/each}}

---

## 收入预测

### 预测方法

**方法**: {{revenue_methodology}}
**粒度**: {{granularity}}

### 收入构成预测

#### 订阅收入

| 用户群 | 用户数 | ARPU | 月度收入 | 年度收入 |
|--------|-------|------|---------|---------|
{{#each subscription_revenue}}
| {{segment}} | {{users}} | ${{arpu}} | ${{monthly}} | ${{yearly}} |
{{/each}}

**订阅收入总计**: ${{total_subscription}}/月

#### 其他收入

{{#each other_revenue}}
- **{{source}}**: ${{amount}}/月
  - 说明: {{description}}
{{/each}}

**总收入**: ${{total_revenue}}/月

### 月度收入预测

{{#if monthly_revenue_chart}}
```chart
type: line
title: 收入预测
x-axis: 月份
y-axis: 收入 ($)
series: {{monthly_revenue_chart.series}}
```
{{/if}}

| 月份 | 订阅收入 | 其他收入 | 总收入 | 环比增长 | 同比增长 |
|------|---------|---------|--------|---------|---------|
{{#each monthly_revenue}}
| {{month}} | ${{subscription}} | ${{other}} | ${{total}} | {{mom}}% | {{yoy}}% |
{{/each}}

### 年度收入预测

| 年份 | 总收入 | 增长率 | 驱动因素 |
|------|-------|--------|---------|
{{#each yearly_revenue}}
| {{year}} | ${{revenue}} | {{growth_rate}}% | {{drivers}} |
{{/each}}

### ARPU 预测

| 用户群 | 当前期 ARPU | 预测期 ARPU | 变化 | 原因 |
|--------|------------|------------|------|------|
{{#each arpu_forecast}}
| {{segment}} | ${{current}} | ${{forecast}} | {{change}}% | {{reason}} |
{{/each}}

---

## LTV & CAC 预测

### LTV 预测

| 用户群 | ARPU | 流失率 | 用户生命周期 | LTV |
|--------|------|--------|-------------|-----|
{{#each ltv_forecast}}
| {{segment}} | ${{arpu}} | {{churn_rate}}% | {{lifetime}} 个月 | ${{ltv}} |
{{/each}}

**平均 LTV**: ${{avg_ltv}}

### CAC 预测

| 渠道 | 获客成本 | 获客数量 | 总 CAC | 占比 |
|------|---------|---------|--------|------|
{{#each cac_by_channel}}
| {{channel}} | ${{cost_per_user}} | {{users}} | ${{total_cac}} | {{percentage}}% |
{{/each}}

**平均 CAC**: ${{avg_cac}}

### LTV/CAC 比率

| 渠道 | LTV | CAC | LTV/CAC | 回本周期 |
|------|-----|-----|---------|---------|
{{#each ltv_cac_ratio}}
| {{channel}} | ${{ltv}} | ${{cac}} | {{ratio}} | {{payback}} 个月 |
{{/each}}

**整体 LTV/CAC**: {{overall_ratio}}

---

## 情景分析

### 情景定义

{{#each scenarios}}

#### {{name}}

**概率**: {{probability}}%

**关键假设**:
{{#each assumptions}}
- {{factor}}: {{value}}
{{/each}}

**风险因素**:
{{#each risks}}
- {{risk}}: {{impact}}
{{/each}}

{{/each}}

### 情景对比结果

{{#if scenario_comparison_chart}}
```chart
type: grouped_bar
title: 情景对比
x-axis: 指标
y-axis: 值
series: {{scenario_comparison_chart.series}}
```
{{/if}}

| 指标 | 乐观 | 基准 | 悲观 |
|------|------|------|------|
{{#each scenario_metrics}}
| {{metric}} | {{optimistic}} | {{baseline}} | {{pessimistic}} |
{{/each}}

---

## 敏感性分析

### 单因素敏感性

{{#if sensitivity_chart}}
```chart
type: tornado
title: 敏感性分析 (龙卷风图)
y-axis: 参数
x-axis: 影响 (%)
series: {{sensitivity_chart.series}}
```
{{/if}}

| 参数 | 基准值 | -20% | -10% | +10% | +20% | 敏感性系数 |
|------|--------|------|------|------|------|-----------|
{{#each sensitivity_analysis}}
| {{parameter}} | {{baseline}} | {{minus_20}} | {{minus_10}} | {{plus_10}} | {{plus_20}} | {{coefficient}} |
{{/each}}

### 最敏感因素

{{#each most_sensitive}}
{{@index}}. **{{factor}}**
   - 影响: {{impact}}
   - 当前假设: {{current_assumption}}
   - 建议监控频率: {{monitoring_frequency}}
{{/each}}

### 场景矩阵

| 增长率 \ 流失率 | 低 ({{low_churn}}%) | 基准 ({{base_churn}}%) | 高 ({{high_churn}}%) |
|-----------------|-------------------|---------------------|-------------------|
| 高 ({{high_growth}}%) | {{scenario_1}} | {{scenario_2}} | {{scenario_3}} |
| 基准 ({{base_growth}}%) | {{scenario_4}} | {{scenario_5}} | {{scenario_6}} |
| 低 ({{low_growth}}%) | {{scenario_7}} | {{scenario_8}} | {{scenario_9}} |

---

## 蒙特卡洛模拟

### 模拟设置

**模拟次数**: {{simulation_runs}}
**置信水平**: {{confidence_level}}%

**参数分布**:
{{#each parameter_distributions}}
- {{name}}: {{distribution}} (μ={{mean}}, σ={{std}})
{{/each}}

### 模拟结果

#### 概率分布

{{#if monte_carlo_chart}}
```chart
type: distribution
title: 结果概率分布
x-axis: 值
y-axis: 概率密度
series: {{monte_carlo_chart.series}}
```
{{/if}}

#### 统计摘要

| 指标 | 用户数预测 | 收入预测 |
|------|-----------|---------|
| 均值 | {{users_mean}} | {{revenue_mean}} |
| 中位数 | {{users_median}} | {{revenue_median}} |
| 标准差 | {{users_std}} | {{revenue_std}} |
| 最小值 | {{users_min}} | {{revenue_min}} |
| 最大值 | {{users_max}} | {{revenue_max}} |

#### 概率区间

| 用户数 | P50 | P70 | P80 | P90 | P95 |
|--------|-----|-----|-----|-----|-----|
| {{forecast_year}} | {{p50}} | {{p70}} | {{p80}} | {{p90}} | {{p95}} |

**达成目标概率**:
{{#each goal_probability}}
- {{goal}}: {{probability}}% 概率达成
{{/each}}

---

## 风险与不确定性

### 预测风险

{{#each forecast_risks}}
- **{{type}}**: {{description}}
  - 影响: {{impact}}
  - 概率: {{probability}}%
  - 缓解措施: {{mitigation}}
{{/each}}

### 关键不确定性

{{#each key_uncertainties}}
- **{{factor}}**
  - 当前假设: {{assumption}}
  - 可能范围: {{range}}
  - 监控指标: {{monitoring}}
{{/each}}

### 外部风险

| 风险类型 | 描述 | 影响 | 应对策略 |
|---------|------|------|---------|
{{#each external_risks}}
| {{type}} | {{description}} | {{impact}} | {{response}} |
{{/each}}

---

## 预测准确度追踪

### 历史预测准确度

| 预测期 | 预测值 | 实际值 | 误差 | MAPE |
|--------|-------|--------|------|------|
{{#each forecast_accuracy}}
| {{period}} | {{forecast}} | {{actual}} | {{error}}% | {{mape}}% |
{{/each}}

**平均 MAPE**: {{avg_mape}}%

### 模型评估

| 模型 | MAE | RMSE | MAPE | 适用性 |
|------|-----|------|------|--------|
{{#each model_evaluation}}
| {{name}} | {{mae}} | {{rmse}} | {{mape}}% | {{suitability}} |
{{/each}}

---

## 行动建议

### 基于预测的决策

{{#each forecast_based_decisions}}
- **{{title}}**
  - 依据: {{rationale}}
  - 预期收益: {{expected_benefit}}
  - 风险: {{risk}}
  - 时间线: {{timeline}}
{{/each}}

### 监控计划

{{#each monitoring_plan}}
- **{{metric}}**
  - 监控频率: {{frequency}}
  - 预警阈值: {{threshold}}
  - 责任人: {{owner}}
{{/each}}

### 滚动预测

**更新周期**: {{update_frequency}}

**下次更新**: {{next_update_date}}

**更新触发条件**:
{{#each update_triggers}}
- {{trigger}}
{{/each}}

---

## 附录

### 方法说明

{{#each methodology_notes}}
- **{{method}}**: {{description}}
{{/each}}

### 数据来源

{{#each data_sources}}
- {{source}}: {{description}} (可靠度: {{reliability}})
{{/each}}

### 假设清单

{{#each all_assumptions}}
- [ ] {{assumption}}
{{/each}}

### 术语表

| 术语 | 定义 |
|------|------|
{{#each glossary}}
| {{term}} | {{definition}} |
{{/each}}

---

*本报告由 Forecast Engine 自动生成*
*预测框架: 多模型 + 情景分析 + 敏感性分析*
