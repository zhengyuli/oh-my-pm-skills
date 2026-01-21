# {{project_name}} - 竞品分析报告

**版本**: {{version}}
**日期**: {{date}}
**作者**: {{author}}
**分析周期**: {{analysis_period}}
**市场**: {{market}}

---

## 执行摘要

### 分析结论

{{#each key_conclusions}}
{{@index}}. {{conclusion}}
   - 影响: {{impact}}
   - 置信度: {{confidence}}
{{/each}}

### 市场定位

**目标细分**: {{target_segment}}

**差异化机会**: {{differentiation_opportunity}}

### 战略建议

{{#each strategic_recommendations}}
- **{{recommendation}}** (优先级: {{priority}})
{{/each}}

---

## 1. 研究方法

### 1.1 分析框架

**主要框架**: {{primary_framework}}

**辅助框架**:
{{#each secondary_frameworks}}
- {{framework}}
{{/each}}

### 1.2 竞品选择标准

{{#each selection_criteria}}
- **{{criterion}}**: {{description}}
  - 权重: {{weight}}%
{{/each}}

### 1.3 数据来源

**公开数据**:
{{#each public_data}}
- {{source}} (更新频率: {{update_frequency}})
{{/each}}

**一手数据**:
{{#each primary_data}}
- {{method}} (样本: {{sample}})
{{/each}}

### 1.4 分析局限

{{#each limitations}}
- **{{limitation}}**: {{mitigation}}
{{/each}}

---

## 2. 竞品概览

### 2.1 竞品列表

| 竞品 | 类型 | 成立时间 | 总部 | 员工数 | 融资阶段 |
|------|------|---------|------|--------|---------|
{{#each competitors_overview}}
| {{name}} | {{type}} | {{founded}} | {{location}} | {{employees}} | {{funding_stage}} |
{{/each}}

### 2.2 市场格局

**市场集中度**:
- CR3: {{cr3}}%
- CR5: {{cr5}}%
- HHI: {{hhi}}

**竞争强度**: {{competition_intensity}}/10

**市场阶段**: {{market_stage}}

---

## 3. 竞品详细分析

{{#each competitor_details}}

## {{competitor_name}}

### 3.{{@index}}.1 基本信息

**公司信息**:
- 成立时间: {{founded_year}}
- 创始人: {{founders}}
- 总部: {{headquarters}}
- 员工数: {{employees}}
- 营收: ${{revenue}}
- 增长率: {{growth_rate}}%

**融资信息**:
- 最新轮次: {{latest_round}}
- 估值: ${{valuation}}
- 投资者: {{investors}}

**领导团队**:
{{#each leadership}}
- **{{name}}** ({{title}}): {{background}}
{{/each}}

### 3.{{@index}}.2 产品分析

**产品定位**: {{product_positioning}}

**核心功能**:
{{#each core_features}}
- **{{feature}}**
  - 描述: {{description}}
  - 用户价值: {{user_value}}
  - 实现质量: {{quality}}/10
{{/each}}

**产品架构**:
```
{{product_architecture}}
```

**技术栈**:
{{#each tech_stack}}
- **{{layer}}}}: {{technologies}}
{{/each}}

**独特功能**:
{{#each unique_features}}
- **{{feature}}}
  - 独特性: {{uniqueness}}
  - 竞争优势: {{competitive_advantage}}
{{/each}}

**产品路线图**:
{{#each product_roadmap}}
- **{{phase}}** ({{timeline}}): {{features}}
{{/each}}

### 3.{{@index}}.3 用户体验分析

**用户界面**:
- 设计风格: {{design_style}}
- 易用性: {{usability}}/10
- 学习曲线: {{learning_curve}}
- 视觉质量: {{visual_quality}}/10

**核心流程**:
{{#each core_flows}}
- **{{flow_name}}**
  - 步骤数: {{steps}}
  - 摩擦点: {{friction_points}}
  - 完成率: {{completion_rate}}%
  - 满意度: {{satisfaction}}/10
{{/each}}

**移动体验**:
- 原生应用: {{native_app}}
- 响应式: {{responsive}}
- 性能: {{mobile_performance}}/10

**可访问性**: {{accessibility_score}}/10

### 3.{{@index}}.4 定价分析

**定价模式**: {{pricing_model}}

**定价方案**:
{{#each pricing_plans}}
- **{{plan_name}}**
  - 价格: ${{price}}/{{period}}
  - 目标客户: {{target_customer}}
  - 包含功能: {{included_features}}
  - 限制: {{limitations}}
{{/each}}

**免费增值策略**:
- 免费版限制: {{free_tier_limits}}
- 转化率: {{conversion_rate}}%
- 平均客单价: ${{arpu}}

**企业定价**:
- 定制报价: {{enterprise_pricing}}
- 合同期限: {{contract_term}}
- 折扣策略: {{discount_strategy}}

**价格竞争力**: {{price_competitiveness}}/10

### 3.{{@index}}.5 商业模式

**收入来源**:
{{#each revenue_streams}}
- **{{stream}}}
  - 占比: {{percentage}}%
  - 增长趋势: {{growth_trend}}
{{/each}}

**成本结构**:
{{#each cost_structure}}
- **{{category}}}}: 占比 {{percentage}}%
{{/each}}

**客户获取**:
- CAC: ${{cac}}
- LTV: ${{ltv}}
- LTV/CAC: {{ltv_cac_ratio}}:1
- 回收周期: {{payback_period}}个月

**关键指标**:
{{#each key_metrics}}
- {{metric}}: {{value}}
{{/each}}

### 3.{{@index}}.6 目标客户

**客户画像**:
{{#each customer_personas}}
- **{{persona}}**
  - 占比: {{percentage}}%
  - 行业: {{industries}}
  - 公司规模: {{company_size}}
  - 使用场景: {{use_cases}}
{{/each}}

**客户细分**:
| 细分 | 占比 | ARPU | 留存率 |
|------|------|------|--------|
{{#each customer_segments}}
| {{segment}} | {{percentage}}% | ${{arpu}} | {{retention}}% |
{{/each}}

**客户满意度**:
- NPS: {{nps}}
- CSAT: {{csat}}/10
- 流失率: {{churn_rate}}%/月

### 3.{{@index}}.7 营销策略

**品牌定位**: {{brand_positioning}}

**价值主张**: {{value_proposition}}

**营销渠道**:
{{#each marketing_channels}}
- **{{channel}}**
  - 投入: {{investment}}
  - 效果: {{effectiveness}}
  - ROI: {{roi}}
{{/each}}

**内容策略**:
{{#each content_strategy}}
- **{{type}}}
  - 频率: {{frequency}}
  - 表现: {{performance}}
{{/each}}

**合作伙伴**:
{{#each partners}}
- **{{partner}}}: {{partnership_type}}
{{/each}}

**营销预算**: ${{marketing_budget}}/年

### 3.{{@index}}.8 销售策略

**销售模式**: {{sales_model}}

**销售团队**:
- SDR: {{sdr_count}}
- AE: {{ae_count}}
- CSM: {{csm_count}}

**销售周期**: {{sales_cycle}}天

**成交率**: {{win_rate}}%

**定价权**: {{pricing_power}}

**客户支持**:
- 支持渠道: {{support_channels}}
- 响应时间: {{response_time}}
- 满意度: {{support_satisfaction}}/10

### 3.{{@index}}.9 优势与劣势

**优势**:
{{#each strengths}}
- **{{strength}}**
  - 重要性: {{importance}}
  - 可持续性: {{sustainability}}
{{/each}}

**劣势**:
{{#each weaknesses}}
- **{{weakness}}}
  - 影响: {{impact}}
  - 改善难度: {{difficulty}}
{{/each}}

**机会**:
{{#each opportunities_comp}}
- **{{opportunity}}}
  - 潜力: {{potential}}
{{/each}}

**威胁**:
{{#each threats_comp}}
- **{{threat}}}
  - 可能性: {{probability}}
{{/each}}

### 3.{{@index}}.10 最新动态

**产品更新**:
{{#each product_updates}}
- **{{update}}}} ({{date}})
{{/each}}

**商业举措**:
{{#each business_moves}}
- **{{move}}}} ({{date}})
{{/each}}

**市场扩张**:
{{#each market_expansion}}
- **{{market}}}} ({{date}})
{{/each}}

**战略合作**:
{{#each partnerships_comp}}
- **{{partnership}}}} ({{date}})
{{/each}}

---

{{/each}}

## 4. 对比分析

### 4.1 功能对比矩阵

| 功能 | {{#each competitor_names}}{{this}} | {{/each}} |
|------|{{#each competitor_names}}---------|{{/each}}|
{{#each feature_comparison}}
| {{feature}} | {{#each competitors}}{{status}} | {{/each}} |
{{/each}}

图例: ✅ 已实现 | ⚠️ 部分实现 | ❌ 未实现 | 🚧 计划中

### 4.2 定位对比

**定位图谱**:
```
高价格
  |
  |  [{{high_price_premium Competitors}}]
  |
中 |
  |  [{{mid_price_mass Competitors}}]
  |
低 |________________________
     低功能        高功能

[{{low_price_basic Competitors}}]    [{{high_price_advanced Competitors}}]
```

**市场分割**:
{{#each market_segments}}
- **{{segment}}**
  - 主要竞品: {{key_competitors}}
  - 市场规模: ${{market_size}}
{{/each}}

### 4.3 获客渠道对比

| 渠道 | {{#each competitor_names_short}}{{this}} | {{/each}} |
|------|{{#each competitor_names_short}}------|{{/each}}|
{{#each channel_comparison}}
| {{channel}} | {{#each competitors}}{{presence}} | {{/each}} |
{{/each}}

### 4.4 客户评价对比

| 维度 | {{#each competitor_names_short}}{{this}} | {{/each}} |
|------|{{#each competitor_names_short}}------|{{/each}}|
{{#each review_comparison}}
| {{dimension}} | {{#each competitors}}{{score}} | {{/each}} |
{{/each}}

---

## 5. 用户反馈分析

### 5.1 用户评价汇总

{{#each user_feedback_summary}}

#### {{competitor_name}}

**总体评分**: {{overall_rating}}/5

**评价来源**:
{{#each review_sources}}
- {{source}} ({{review_count}}条评价)
{{/each}}

**好评要点**:
{{#each positive_points}}
- {{point}} (提及率: {{mention_rate}}%)
{{/each}}

**差评要点**:
{{#each negative_points}}
- {{point}} (提及率: {{mention_rate}}%)
{{/each}}

**用户画像**:
{{#each reviewer_demographics}}
- {{segment}}: {{percentage}}%
{{/each}}

{{/each}}

### 5.2 用户痛点总结

**共同痛点**:
{{#each common_pain_points}}
- **{{pain_point}}**
  - 影响竞品: {{affected_competitors}}
  - 严重性: {{severity}}/10
  - 解决难度: {{difficulty}}/10
{{/each}}

**未满足需求**:
{{#each unmet_needs}}
- **{{need}}**
  - 重要性: {{importance}}/10
{{/each}}

---

## 6. 竞争态势分析

### 6.1 竞争强度评估

| 维度 | 评分 | 说明 |
|------|------|------|
{{#each competition_intensity_metrics}}
| {{dimension}} | {{score}}/10 | {{description}} |
{{/each}}

**总体竞争强度**: {{overall_intensity}}/10

### 6.2 进入壁垒

**技术壁垒**: {{technical_barrier}}/10
**资金壁垒**: {{financial_barrier}}/10
**网络效应**: {{network_effects}}/10
**转换成本**: {{switching_costs}}/10
**监管壁垒**: {{regulatory_barrier}}/10

**总体壁垒**: {{overall_barrier}}/10

### 6.3 替代品威胁

**直接替代**:
{{#each direct_substitutes}}
- **{{substitute}}}: {{threat_level}}/10
{{/each}}

**间接替代**:
{{#each indirect_substitutes}}
- **{{substitute}}}: {{threat_level}}/10
{{/each}}

### 6.4 供应商议价力

**供应商集中度**: {{supplier_concentration}}/10
**转换成本**: {{supplier_switching_cost}}/10
**前向整合**: {{forward_integration}}/10

**总体议价力**: {{supplier_power}}/10

### 6.5 客户议价力

**价格敏感度**: {{price_sensitivity}}/10
**产品差异度**: {{product_differentiation}}/10
**转换成本**: {{customer_switching_cost}}/10
**信息透明度**: {{information_transparency}}/10

**总体议价力**: {{buyer_power}}/10

---

## 7. 机会识别

### 7.1 市场空白

**功能空白**:
{{#each functional_gaps}}
- **{{gap}}**
  - 重要性: {{importance}}/10
  - 实现难度: {{difficulty}}/10
  - 竞争压力: {{competitive_pressure}}/10
{{/each}}

**细分市场空白**:
{{#each segment_gaps}}
- **{{segment}}**
  - 规模: ${{size}}
  - 增长率: {{growth_rate}}%
  - 服务不足原因: {{underserved_reason}}
{{/each}}

### 7.2 差异化机会

**产品差异化**:
{{#each product_differentiation}}
- **{{opportunity}}}
  - 差异化程度: {{differentiation_level}}/10
  - 可持续性: {{sustainability}}/10
{{/each}}

**服务差异化**:
{{#each service_differentiation}}
- **{{opportunity}}}
  - 实现成本: {{cost}}
  - 客户价值: {{customer_value}}
{{/each}}

**商业模式差异化**:
{{#each business_model_differentiation}}
- **{{opportunity}}}
  - 风险: {{risk}}
  - 回报: {{return}}
{{/each}}

### 7.3 颠覆机会

**技术颠覆**:
{{#each technology_disruption}}
- **{{opportunity}}}
  - 成熟度: {{maturity}}
  - 时间窗口: {{time_window}}
{{/each}}

**商业模式颠覆**:
{{#each business_model_disruption}}
- **{{opportunity}}}
  - 可行性: {{feasibility}}
{{/each}}

---

## 8. 战略建议

### 8.1 定位策略

**推荐定位**: {{recommended_positioning}}

**理由**:
{{#each positioning_rationale}}
- {{reason}}
{{/each}}

**定位陈述**: {{positioning_statement}}

### 8.2 产品策略

**核心功能优先级**:
{{#each product_priorities}}
- **{{feature}}}} (P{{priority}})
  - 差距分析: {{gap_analysis}}
  - 竞争优势: {{competitive_advantage}}
  - 实现成本: {{implementation_cost}}
{{/each}}

**差异化功能**:
{{#each differentiating_features}}
- **{{feature}}}
  - 独特性: {{uniqueness}}
  - 价值: {{value}}
  - 护城河: {{moat}}
{{/each}}

**应避免的功能**:
{{#each features_to_avoid}}
- **{{feature}}}} - {{reason}}
{{/each}}

### 8.3 定价策略

**推荐定价模式**: {{recommended_pricing_model}}

**定价方案**:
{{#each recommended_pricing}}
- **{{plan}}}: ${{price}}/{{period}}
  - 目标客户: {{target_customer}}
  - 竞争对比: {{competitive_comparison}}
{{/each}}

**定价依据**:
{{#each pricing_rationale}}
- {{factor}}: {{analysis}}
{{/each}}

### 8.4 GTM 策略

**目标市场**: {{target_market}}

**渠道策略**:
{{#each channel_strategy}}
- **{{channel}}}
  - 优先级: {{priority}}
  - 预算分配: {{budget_allocation}}%
  - 竞品对比: {{competitive_comparison}}
{{/each}}

**营销信息**:
{{#each marketing_messages}}
- **{{audience}}}: {{message}}
  - 差异化: {{differentiation}}
{{/each}}

**上市时机**: {{launch_timing}}

**时机选择理由**:
{{#each timing_rationale}}
- {{factor}}: {{consideration}}
{{/each}}

---

## 9. 风险评估

### 9.1 竞争风险

{{#each competitive_risks}}
- **{{risk}}**
  - 可能性: {{probability}}
  - 影响: {{impact}}
  - 缓解措施: {{mitigation}}
{{/each}}

### 9.2 响应策略

**如果竞品降价**:
{{#each price_response}}
- {{scenario}} → {{response}}
{{/each}}

**如果竞品推出新功能**:
{{#each feature_response}}
- {{scenario}} → {{response}}
{{/each}}

**如果新竞品进入市场**:
{{#each new_competitor_response}}
- {{scenario}} → {{response}}
{{/each}}

---

## 10. 行动计划

### 10.1 短期行动 (1-3个月)

{{#each short_term_actions}}
- [ ] **{{action}}**
  - 优先级: {{priority}}
  - 负责人: {{owner}}
  - 截止: {{deadline}}
  - 成功指标: {{success_metric}}
{{/each}}

### 10.2 中期计划 (3-12个月)

{{#each medium_term_plans}}
- [ ] **{{initiative}}**
  - 优先级: {{priority}}
  - 里程碑: {{milestones}}
  - 资源需求: {{resource_requirements}}
{{/each}}

### 10.3 长期战略 (1-3年)

{{#each long_term_strategy}}
- [ ] **{{strategic_initiative}}}
  - 战略目标: {{strategic_objective}}
  - 关键里程碑: {{key_milestones}}
{{/each}}

---

## 附录

### A. 竞品评分卡

{{#each scorecards}}

#### {{competitor_name}}

| 维度 | 评分 | 权重 | 加权分 |
|------|------|------|--------|
{{#each dimensions}}
| {{name}} | {{score}} | {{weight}}% | {{weighted_score}} |
{{/each}}
| **总分** | | | **{{total_score}}** |

{{/each}}

### B. 数据收集日志

{{#each data_collection_log}}
- **{{date}}}: {{source}}
  - 收集内容: {{content}}
  - 可靠性: {{reliability}}
{{/each}}

### C. 竞品监控清单

**日常监控**:
{{#each daily_monitoring}}
- [ ] {{item}} (频率: {{frequency}})
{{/each}}

**定期分析**:
{{#each periodic_analysis}}
- [ ] {{analysis}} (频率: {{frequency}}, 下次: {{next_date}})
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

*本报告由 Competitor Analyzer 自动生成*
*分析框架: {{primary_framework}}*
*分析周期: {{analysis_period}}*
