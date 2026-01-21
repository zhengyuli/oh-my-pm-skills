---
name: research-assistant
description: 市场研究与竞品分析专家 - TAM/SAM/SOM分析、竞争情报、SWOT分析、行业趋势洞察
version: 1.0.0
author: oh-my-pm-skills
tags: [core, pm, research, market-analysis, competitive-intelligence, tam-sam-som, swot]
allowed-tools: Read, Write, Edit, WebSearch, mcp__tavily-search__search, mcp__tavily-search__searchContext, mcp__tavily-search__searchQNA, mcp__fetch__fetch, mcp__web_reader__webReader
model: inherit
---

# Research Assistant

研究助手负责自动化市场研究、竞品分析、行业趋势洞察，为 PM 提供数据支持的决策依据。

## When to Use This Skill

用户请求以下功能时激活此技能：
- "研究竞品"
- "市场分析"
- "行业趋势"
- "竞品对比"
- "市场机会分析"
- "research competitors"

## Core Process

### 步骤 1: 定义研究目标

```yaml
研究类型:
  竞品分析:
    - 直接竞品对比
    - 功能差异分析
    - 定价策略研究
    - 用户评价分析

  市场分析:
    - 市场规模估算
    - 增长趋势预测
    - 细分市场识别
    - 进入壁垒分析

  用户研究:
    - 用户画像构建
    - 需求痛点分析
    - 行为模式研究
    - 决策因素分析

  技术研究:
    - 技术趋势分析
    - 解决方案评估
    - 技术可行性研究
    - 创新机会识别
```

### 步骤 2: 制定研究计划

```yaml
研究方法:
  一手研究:
    - 用户访谈
    - 问卷调查
    - 焦点小组
    - 用户观察

  二手研究:
    - 行业报告
    - 新闻文章
    - 分析师报告
    - 学术论文

  数据分析:
    - 网站流量分析
    - 社交媒体分析
    - 应用商店分析
    - 搜索趋势分析

时间范围:
  - 历史数据: {{historical_period}} (通常 1-3 年)
  - 当前快照: {{snapshot_date}}
  - 未来预测: {{forecast_horizon}} (通常 1-5 年)

数据来源:
  {{#each data_sources}}
  - {{name}}: {{url}}
  - 可靠性: {{reliability}}
  - 更新频率: {{update_frequency}}
  {{/each}}
```

### 步骤 3: 收集和处理数据

#### 权威数据收集流程

```yaml
第一阶段: 权威咨询机构报告
  1. 优先查询 Gartner Magic Quadrant
     - 搜索: site:gartner.com "[关键词]" magic quadrant
     - 提取: Market Size、Vendor Matrix、Key Findings

  2. 查询 Forrester Wave
     - 搜索: site:forrester.com "[关键词]" wave
     - 提取: Market Overview、Recommendations、Scorecards

  3. 查询 IDC MarketScape
     - 搜索: site:idc.com "[关键词]" marketscape
     - 提取: Market Forecast、Vendor Analysis、Key Trends

  4. 查询 CB Insights
     - 搜索: site:cbinsights.com "[关键词]" trending
     - 提取: Emerging Trends、Funding Data、Unicorns

第二阶段: Top 10 公司数据收集
  1. 上市公司数据
     - SEC EDGAR: 10-K、10-Q、8-K 文件
     - 公司官网: 投资者关系页面
     - 分析师会议: Seeking Alpha 转录

  2. 创业公司数据
     - Crunchbase: 融资历史、估值、投资人
     - Product Hunt: 产品发布、用户评分
     - TechCrunch: 新闻报道、产品更新

  3. 数据收集模板应用
     - 使用公司信息收集模板（见上文）
     - 填充基本信息、产品信息、财务信息、市场表现

第三阶段: 数据质量评估
  1. 准确性评分
     - 来源可靠性: 官方 > 专业 > 社区
     - 数据一致性: 多源交叉验证
     - 机构背书: Gartner/Forrester 等认证

  2. 时效性判断
     - 实时数据: < 24小时
     - 近期数据: 1-7天
     - 历史数据: > 1个月

  3. 交叉验证（三角验证法）
     - 来源三角: 3个不同来源
     - 时间三角: 不同时间点对比
     - 方法三角: 不同收集方法

第四阶段: 数据整合
  1. 按优先级排序
     - 第一优先级: 权威来源
     - 第二优先级: 专业来源
     - 第三优先级: 补充来源

  2. 标注来源和可靠性
     - 数据来源: Gartner/SEC/Crunchbase 等
     - 可靠性评分: 高/中/低
     - 数据时效: 发布日期

  3. 识别数据缺口
     - 缺失字段
     - 需要补充的数据
     - 替代数据源
```

#### 竞品数据收集

```yaml
基本信息:
  公司名称: {{company}}
  产品名称: {{product}}
  网站: {{website}}

产品信息:
  定位: {{positioning}}
  目标用户: {{target_users}}
  核心功能: {{key_features}}

商业模式:
  定价模式: {{pricing_model}}
  价格范围: {{price_range}}
  收入来源: {{revenue_streams}}

市场表现:
  用户规模: {{user_count}}
  增长率: {{growth_rate}}
  市场份额: {{market_share}}
  融资情况: {{funding}}

用户反馈:
  评分: {{rating}}
  评论数量: {{review_count}}
  正面反馈: {{positive_themes}}
  负面反馈: {{negative_themes}}
```

#### 市场数据收集

```yaml
市场规模:
  TAM (Total Addressable Market):
    规模: {{tam_size}}
    增长率: {{tam_growth}}% CAGR

  SAM (Serviceable Addressable Market):
    规模: {{sam_size}}
    增长率: {{sam_growth}}% CAGR

  SOM (Serviceable Obtainable Market):
    规模: {{som_size}}
    增长率: {{som_growth}}% CAGR

市场趋势:
  驱动因素:
    - {{driver_1}}
    - {{driver_2}}

  阻碍因素:
    - {{constraint_1}}
    - {{constraint_2}}

  新兴机会:
    - {{opportunity_1}}
    - {{opportunity_2}}

行业动态:
  - 重大并购: {{mergers}}
  - 新进入者: {{new_competitors}}
  - 技术突破: {{technology_breakthroughs}}
  - 监管变化: {{regulatory_changes}}
```

### 步骤 4: 分析和综合

#### SWOT 分析

```yaml
Strengths (优势):
  内部优势:
    - {{strength_1}}
    - {{strength_2}}

Weaknesses (劣势):
  内部劣势:
    - {{weakness_1}}
    - {{weakness_2}}

Opportunities (机会):
  外部机会:
    - {{opportunity_1}}
    - {{opportunity_2}}

Threats (威胁):
  外部威胁:
    - {{threat_1}}
    - {{threat_2}}
```

#### 竞品对比矩阵

```yaml
对比维度:
  功能:
    - 功能完整性
    - 创新性
    - 易用性

  商业:
    - 定价竞争力
    - 商业模式
    - 增长策略

  技术:
    - 技术架构
    - 性能表现
    - 安全性

  市场:
    - 品牌认知
    - 用户规模
    - 市场份额

评分标准:
  - 我们: 1-5 分
  - 竞品 A: 1-5 分
  - 竞品 B: 1-5 分
```

### 步骤 5: 生成研究报告

```markdown
# {{report_title}}

**研究日期**: {{date}}
**研究类型**: {{research_type}}
**数据截止**: {{data_cutoff}}

---

## 执行摘要

### 关键发现

{{#each key_findings}}
{{index}}. {{finding}}
{{/each}}

### 核心洞察

{{#each key_insights}}
- {{insight}}
{{/each}}

### 战略建议

{{#each strategic_recommendations}}
{{priority}}. {{recommendation}}
{{/each}}

---

## 市场概览

### 市场规模

**TAM (总可寻址市场)**: ${{tam_size}}B
**SAM (可服务市场)**: ${{sam_size}}B
**SOM (可获得市场)**: ${{som_size}}B

**增长率**: {{growth_rate}}% CAGR ({{forecast_period}})

### 市场趋势

#### 驱动因素

{{#each market_drivers}}
- **{{name}}**: {{description}}
  - 影响: {{impact}}
  - 持续时间: {{duration}}
{{/each}}

#### 阻碍因素

{{#each market_constraints}}
- **{{name}}**: {{description}}
  - 影响: {{impact}}
  - 缓解方案: {{mitigation}}
{{/each}}

### 细分市场

| 细分市场 | 规模 | 增长率 | 机会 | 进入壁垒 |
|---------|------|--------|------|----------|
{{#each market_segments}}
| {{name}} | ${{size}}B | {{growth}}% | {{opportunity}} | {{barriers}} |
{{/each}}

---

## 竞品分析

### 竞品概览

| 竞品 | 定位 | 用户规模 | 评分 | 优势 | 劣势 |
|------|------|----------|------|------|------|
{{#each competitors}}
| {{name}} | {{positioning}} | {{users}} | {{rating}} | {{strengths}} | {{weaknesses}} |
{{/each}}

### 详细竞品分析

{{#each competitor_details}}

#### {{name}}

**基本信息**:
- 网站: {{website}}
- 上线时间: {{launch_date}}
- 融资情况: {{funding}}
- 员工数量: {{employees}}

**产品定位**: {{positioning}}

**核心功能**:
{{#each key_features}}
- {{feature}}: {{description}}
{{/each}}

**定价策略**:
- 模式: {{pricing_model}}
- 价格: {{price}}
- 免费方案: {{free_tier}}

**用户反馈**:
- 评分: {{rating}} / 5
- 评论数: {{review_count}}
- 正面反馈: {{positive_feedback}}
- 负面反馈: {{negative_feedback}}

**市场表现**:
- 用户规模: {{user_count}}
- 增长率: {{growth_rate}}%
- 市场份额: {{market_share}}%

**我们的机会**: {{opportunity}}

{{/each}}

### 竞品对比矩阵

{{#each comparison_matrices}}

#### {{dimension}} 对比

| 能力 | 我们 | {{#each competitors}}{{name}} | {{/each}}
|------|------|{{#each competitors}}------| {{/each}}
{{#each capabilities}}
| {{name}} | {{us}} | {{#each competitors}}{{score}} | {{/each}}
{{/each}}

{{/each}}

---

## 用户洞察

### 用户画像

{{#each personas}}

#### {{name}}

**基本信息**:
- 年龄: {{age}}
- 职业: {{occupation}}
- 行业: {{industry}}
- 收入: {{income}}

**目标**: {{goals}}

**痛点**: {{pain_points}}

**行为模式**: {{behavior_patterns}}

**决策因素**: {{decision_factors}}

**使用场景**: {{use_cases}}

{{/each}}

### 用户需求分析

**核心需求**:
{{#each core_needs}}
{{priority}}. {{need}} (重要性: {{importance}}/10)
{{/each}}

**未满足需求** (机会):
{{#each unmet_needs}}
- {{need}} (满意度: {{satisfaction}}/10)
{{/each}}

---

## SWOT 分析

### Strengths (优势)

{{#each swot_strengths}}
- {{strength}} (影响: {{impact}})
{{/each}}

### Weaknesses (劣势)

{{#each swot_weaknesses}}
- {{weakness}} (影响: {{impact}})
{{/each}}

### Opportunities (机会)

{{#each swot_opportunities}}
- {{opportunity}} (优先级: {{priority}})
{{/each}}

### Threats (威胁)

{{#each swot_threats}}
- {{threat}} (风险等级: {{risk_level}})
{{/each}}

---

## 技术趋势

### 新兴技术

{{#each emerging_techs}}
- **{{name}}**: {{description}}
  - 成熟度: {{maturity}}
  - 应用场景: {{use_cases}}
  - 影响程度: {{impact}}
{{/each}}

### 技术壁垒

{{#each technical_barriers}}
- {{barrier}}: {{description}}
  - 克服方案: {{solution}}
{{/each}}

---

## 战略建议

### 进入策略

{{#each entry_strategy}}
{{phase}}. {{title}}
- 目标: {{objective}}
- 行动: {{actions}}
- 时间线: {{timeline}}
{{/each}}

### 差异化策略

{{#each differentiation}}
- **{{area}}**: {{approach}}
  - 竞争优势: {{advantage}}
{{/each}}

### 风险缓解

{{#each risk_mitigation}}
- **{{risk}}**: {{mitigation_strategy}}
{{/each}}

---

## 行动计划

### 短期 (3 个月)

{{#each short_term_actions}}
- [ ] {{action}} (负责人: {{owner}}, 截止: {{due_date}})
{{/each}}

### 中期 (6-12 个月)

{{#each medium_term_actions}}
- [ ] {{action}} (负责人: {{owner}}, 截止: {{due_date}})
{{/each}}

### 长期 (1-3 年)

{{#each long_term_actions}}
- [ ] {{action}} (负责人: {{owner}}, 截止: {{due_date}})
{{/each}}

---

## 数据来源

{{#each data_sources}}
- {{source}}: {{url}}
  - 访问日期: {{access_date}}
  - 可靠性: {{reliability}}
{{/each}}

## 附录

### 研究方法

{{research_methodology}}

### 假设和限制

{{#each assumptions}}
- {{assumption}}
{{/each}}

### 进一步研究建议

{{#each further_research}}
- {{topic}} (优先级: {{priority}})
{{/each}}

---

*报告由 Research Assistant 自动生成*
*数据来源: {{data_sources_summary}}*
```

## 交互示例

### 示例 1: 竞品分析

```
用户: 研究 Notion、Confluence、飞书书的竞品对比

Research Assistant:
  1. 收集各产品基本信息
  2. 对比功能、定价、用户体验
  3. 分析用户反馈
  4. 生成对比矩阵
  5. 提出差异化建议
```

### 示例 2: 市场规模估算

```
用户: 分析企业协作文档软件的市场规模

Research Assistant:
  1. 定义 TAM/SAM/SOM
  2. 收集行业数据
  3. 预测增长趋势
  4. 识别细分市场机会
```

### 示例 3: 技术趋势研究

```
用户: AI 协作工具有哪些技术趋势？

Research Assistant:
  1. 搜索最新技术发展
  2. 分析技术成熟度
  3. 评估应用场景
  4. 识别创新机会
```

## 集成点

**使用的引擎**:
- **qa-engine**: 研究问题生成
- **template-engine**: 报告渲染
- **document-engine**: 报告生成

**与其他技能协作**:
- **prd-generator**: 市场分析章节
- **jtbd-analyzer**: 用户研究数据

## 数据源清单

```yaml
免费数据源:
  - Google Trends (搜索趋势)
  - SimilarWeb (流量分析)
  - Product Hunt (产品发现)
  - GitHub (开源项目)
  - 社交媒体 (用户反馈)

付费数据源:
  - Gartner (行业报告)
  - Forrester (市场研究)
  - IDC (市场数据)
  - CB Insights (投资数据)

公开数据:
  - 公司财报
  - 应用商店数据
  - 招聘信息
  - 新闻报道
```

## 权威数据源

### 咨询机构报告

#### Gartner
- **官网**: https://www.gartner.com
- **免费渠道**:
  - Magic Quadrant 摘要版
  - Gartner Insights 博客
  - Webinar 研讨会
- **付费渠道**:
  - 单份报告: $3,000-5,000
  - 年度订阅: $15,000-20,000
- **获取方式**:
  - 官网搜索关键词
  - LinkedIn 关注分析师
  - 学术图书馆访问
- **数据提取重点**:
  - Market Size (市场规模)
  - Vendor Matrix (供应商矩阵)
  - Key Findings (关键发现)
- **搜索技巧**: `site:gartner.com "[关键词]" magic quadrant`

#### Forrester
- **官网**: https://www.forrester.com
- **免费渠道**:
  - Forrester Wave 摘要
  - Research Library 基础研究
  - 每周新闻通讯
- **付费渠道**:
  - 单份报告: $2,000-4,000
  - 全年访问权限: $12,000-18,000
- **数据提取重点**:
  - Market Overview (市场概览)
  - Recommendations (建议)
  - Scorecards (评分卡)

#### IDC
- **官网**: https://www.idc.com
- **免费渠道**:
  - IDC MarketScape 简版
  - 行业研究报告摘要
  - 数据洞察博客
- **付费渠道**:
  - 单份报告: $1,500-3,500
  - 定制化研究服务
- **数据提取重点**:
  - Market Forecast (市场预测)
  - Vendor Analysis (供应商分析)
  - Key Trends (关键趋势)

#### CB Insights
- **官网**: https://www.cbinsights.com
- **免费渠道**:
  - Trending Reports 免费列表
  - 每周新闻摘要
  - 市场数据可视化
- **付费渠道**:
  - Pro版: $2,995/年
  - Team版: $4,995/年
  - Enterprise版定制
- **数据提取重点**:
  - Emerging Trends (新兴趋势)
  - Funding Data (融资数据)
  - Unicorns (独角兽公司)

### 投资与创业数据库

#### Crunchbase
- **官网**: https://www.crunchbase.com
- **免费功能**:
  - 基础公司档案
  - 融资历史
  - 投资人信息
- **付费功能**:
  - 深度财务数据
  - 预测分析
  - 高级筛选工具
- **使用技巧**:
  - 设置关键词提醒（如 AI、SaaS、Fintech）
  - 导出 CSV 进行批量分析
  - 关注相似公司推荐

#### PitchBook
- **官网**: https://pitchbook.com
- **免费功能**:
  - 公司基本信息
- **付费功能**:
  - 深度财务分析
  - 可比公司分析
  - 估值变化追踪
- **使用技巧**:
  - 利用 "Deal Screening" 筛选特定行业
  - 追踪投资机构投资组合
  - 分析估值变化趋势

#### AngelList
- **官网**: https://angel.co
- **免费功能**:
  - 公司档案
  - 职位发布
- **使用技巧**:
  - 通过招聘信息判断发展方向
  - 查看团队背景和履历
  - 分析技术栈需求

## Top 10 公司产品数据收集

### 上市公司数据收集模板

#### 财务数据
- **SEC EDGAR 数据库**: https://www.sec.gov/edgar
  - 10-K 年报（完整财务报告）
  - 10-Q 季报（季度财务更新）
  - 8-K 重大事项公告
  - DEF 14A 代理声明

- **公司官网投资者关系页面**:
  - 财务报表和投资者演示文稿
  - 年报和季报 PDF 下载
  - 管理层会议录音和纪要

#### 产品数据
- 官网产品页面
  - 产品功能规格说明
  - 定价页面
  - 客户案例研究
  - 产品路线图

- 分析师会议
  - Seeking Alpha 转录
  - 微软团队会议记录
  - 花旗和摩根士丹利分析师报告

### 创业公司数据收集模板

#### 融资数据
- **Crunchbase**: https://www.crunchbase.com
  - 融资历史和估值
  - 投资人信息
  - 关键人员资料
  - 产品标签和分类

- **PitchBook**: https://pitchbook.com
  - 详细的交易条款
  - 估值变化追踪
  - 投资组合分析
  - 深度财务数据

#### 产品追踪
- **Product Hunt**: https://www.producthunt.com
  - 最新产品发布
  - 用户评分和评论
  - 创始人访谈
  - 每日热门产品

- **BetaList**: https://betalist.com
  - 专注于 MVP 和测试阶段产品
  - 收集早期用户反馈
  - 追踪产品迭代历程

- **Hacker News**: https://news.ycombinator.com
  - 技术社区讨论
  - 产品真实反馈
  - 创始人 AMA 问答

#### 媒体追踪
- **Tech 媒体**:
  - TechCrunch: https://techcrunch.com
  - VentureBeat: https://venturebeat.com
  - The Information: https://theinformation.com

- **行业媒体**:
  - Stratechery（科技战略）
  - Lenny's Newsletter（产品增长）
  - First Round Review（创业经验）

### 数据收集模板

```yaml
公司信息收集模板:
  基本信息:
    - 公司名称:
    - 成立时间:
    - 总部地址:
    - CEO:
    - 员工人数:
    - 融资状态:

  产品信息:
    - 主要产品:
    - 核心功能:
    - 目标客户:
    - 定价策略:
    - 技术架构:
    - 竞争优势:

  财务信息:
    - 最新估值:
    - 融资总额:
    - 投资方:
    - 收入模式:
    - 客户数量:
    - 增长率:

  市场表现:
    - 市场份额:
    - 竞争对手:
    - 用户评价:
    - 行业排名:
    - 发展趋势:
```

## 数据源优先级

### 第一优先级（权威来源）

1. **官方数据**:
   - 公司财报（10-K, 10-Q）
   - SEC 文件
   - 官网发布信息

2. **监管数据**:
   - SEC EDGAR 数据库
   - 金融监管机构文件

3. **咨询报告**:
   - Gartner Magic Quadrant
   - Forrester Wave
   - IDC MarketScape

### 第二优先级（专业来源）

1. **专业媒体**:
   - TechCrunch
   - VentureBeat
   - Bloomberg

2. **投资数据库**:
   - Crunchbase
   - PitchBook

3. **行业分析**:
   - 专业分析师报告
   - 投资机构研报

### 第三优先级（补充来源）

1. **社区内容**:
   - Reddit
   - Hacker News
   - Product Hunt

2. **社交媒体**:
   - Twitter
   - LinkedIn
   - 公司博客

3. **第三方评论**:
   - G2
   - Capterra
   - Trustpilot

## 数据质量评估

### 评估维度

**准确性**:
- 来源可靠性（多个来源一致性）
- 数据更新频率
- 是否有独立验证
- 专业机构背书

**时效性**:
- 发布日期
- 数据截止日期
- 更新频率
- 是否有延迟

**完整性**:
- 数据覆盖度
- 信息颗粒度
- 是否有缺失字段
- 补充数据可行性

**可信度**:
- 数据提供方资质
- 数据收集方法
- 是否有利益冲突
- 历史准确性记录

### 交叉验证方法

**三角验证法**:

1. **来源三角**:
   - 同一信息至少 3 个不同来源验证

2. **时间三角**:
   - 不同时间点的数据对比分析

3. **方法三角**:
   - 不同收集方法的结果对比

**验证清单**:
- [ ] 官方数据核对
- [ ] 行业基准对比
- [ ] 竞争对手数据对照
- [ ] 历史趋势分析
- [ ] 专业机构引用
- [ ] 第三方验证

### 数据时效性判断标准

**实时数据**（< 24小时）:
- 股价、交易量
- 社交媒体热度
- 新闻发布

**近期数据**（1-7天）:
- 产品更新发布
- 融资消息
- 行业动态

**近期数据**（1-4周）:
- 月度运营数据
- 季度财报摘要
- 市场份额变化

**历史数据**（> 1个月）:
- 年度报告
- 长期趋势分析
- 战略规划数据

## 最佳实践

✅ **DO**:
- 多源交叉验证
- 标注数据来源和可靠性
- 定期更新研究报告
- 关注数据质量
- 保持客观中立

❌ **DON'T**:
- 只依赖单一数据源
- 忽视数据时效性
- 混淆事实和观点
- 过度推断
- 忽视样本偏差

## 输出格式

```yaml
result:
  success: true
  research_type: "{{type}}"
  data_points: {{count}}

  key_findings:
    - {{finding_1}}

  insights:
    - {{insight_1}}

  report_path: "reports/{{report_name}}.md"
```

## 测试场景

```bash
# 竞品分析
research-assistant competitors \
  --products "Notion,Confluence,飞书" \
  --dimensions "features,pricing,ux"

# 市场分析
research-assistant market \
  --category "企业协作" \
  --regions "CN,US"

# 技术趋势
research-assistant trends \
  --domain "AI 协作" \
  --horizon "3years"
```
