---
name: forecast-engine
description: 预测引擎 - TAM/SAM/SOM市场规模、用户增长(Logistic/Bass模型)、收入预测、蒙特卡洛模拟
version: 1.0.0
author: oh-my-pm-skills
tags: [engine, forecast, prediction, trends, modeling, tam-sam-som, monte-carlo]
allowed-tools: Read, Write, Edit, WebSearch, mcp__tavily-search__search, mcp__tavily-search__searchContext, mcp__tavily-search__searchQNA, mcp__fetch__fetch
model: inherit
---

# Forecast Engine

预测引擎负责使用各种预测模型进行市场预测、用户增长预测、收入预测等，帮助 PM 做前瞻性规划。

## When to Use This Engine

其他技能需要以下功能时调用此引擎：
- 市场规模预测 (TAM/SAM/SOM)
- 用户增长预测
- 收入预测
- 趋势外推
- 情景分析
- 敏感性分析

## Execution Instructions

**IMPORTANT**: 必须使用多搜索引擎进行实际搜索和交叉验证，每个预测数据点必须包含可访问链接。

### 多搜索引擎策略

1. **WebSearch**（主搜索）- 必须使用
2. **mcp__tavily-search__search**（增强搜索）- 如果可用则使用
3. **mcp__tavily-search__searchQNA**（事实验证）- 如果可用则使用
4. **mcp__fetch__fetch**（验证链接可访问性）- 如果可用则使用

### 智能降级策略

```yaml
WebSearch 不可用:
  行为: 报错并停止
  原因: WebSearch 是必需工具

Tavily Search 不可用:
  行为: 仅使用 WebSearch，继续执行
  记录: "[警告] Tavily 不可用，使用基础搜索"

Tavily QNA 不可用:
  行为: 跳过验证步骤，继续执行
  记录: "[信息] 未使用事实验证"

mcp__fetch__fetch 不可用:
  行为: 仅记录 URL，不验证可访问性
  记录: "[信息] 未验证链接可访问性"
```

### 分层搜索策略

```yaml
关键数据（预测模型输入）:
  类型: 市场规模、增长率、类比产品数据
  搜索深度: 3 轮（WebSearch → Tavily → QNA验证）
  URL验证: 必须验证
  链接要求: 至少 1 个公开可访问链接

重要数据（预测参考）:
  类型: 行业基准、历史趋势
  搜索深度: 2 轮（WebSearch → Tavily）
  URL验证: 推荐验证
  链接要求: 提供链接即可
```

### 执行流程

**步骤 1**：搜索市场规模数据（关键数据，3 轮搜索 + 链接验证）

```yaml
第一轮 - 主搜索:
  工具: WebSearch
  查询: "[关键词] market size [当前年份]"
  记录: 记录所有找到的链接

第二轮 - 增强搜索:
  工具: mcp__tavily-search__search
  查询: "[关键词] TAM SAM SOM [当前年份]"
  补充: 补充更多数据源

第三轮 - 链接验证:
  工具: mcp__fetch__fetch
  验证: 验证关键链接的可访问性
  标注: 标注访问状态（公开/需要注册/付费/失效）
```

**步骤 2**：搜索行业增长率（关键数据，3 轮搜索）
- 第一轮：`WebSearch` → `"[关键词] market growth rate CAGR [当前年份]"`
- 第二轮：`mcp__tavily-search__search` → `"[关键词] industry forecast trends"`
- 第三轮：`mcp__tavily-search__searchQNA` → 验证增长率数据

**步骤 3**：搜索类比产品数据（重要数据，2 轮搜索）
- 第一轮：`WebSearch` → `"[类比产品] growth trajectory case study"`
- 第二轮：`mcp__tavily-search__search` → `"[类比产品] user adoption rate"`

### 信息引用要求

每个预测数据必须包含：
```yaml
预测数据: [数值]
来源: [机构/分析师]
发布日期: [YYYY-MM-DD]
URL: [可访问的链接]
访问状态: [公开/需要注册/付费]
备用链接: [如果主要链接不可访问]
搜索日期: [YYYY-MM-DD]
```

### 进度输出要求

**Level 1：主要阶段进度（默认显示）**
```markdown
[阶段 1/2] 正在搜索市场数据和增长率...
[阶段 1/2] ✓ 已完成市场规模和增长率数据收集
[阶段 2/2] 正在分析类比产品数据...
[阶段 2/2] ✓ 预测模型构建完成
```

**Level 2：详细进度（日志记录）**
```markdown
[搜索] 正在搜索市场规模数据...
[完成] ✓ 已搜索市场数据 (WebSearch)
[搜索] 正在使用 Tavily 深度搜索...
[完成] ✓ Tavily 搜索完成
[验证] 正在验证市场规模数据...
[完成] ✓ 市场规模已验证: $XX 亿
[链接] 正在验证链接可访问性...
[完成] ✓ 链接已验证: https://... (公开)
```

### 最终输出

- **文件**: `outputs/forecasts/YYYY-MMDD-[topic]-forecast.md`
- **日志**: `outputs/logs/YYYY-MMDD-forecast-engine-execution.log`
- **URL清单**: `outputs/references/YYYY-MMDD-[topic]-urls.md`

**⚠️ 禁止行为**：
- ❌ 仅依赖训练数据生成预测数字
- ❌ 跳过工具调用步骤
- ❌ 不标注数据来源

## Core Process

### 步骤 1: 选择预测模型

```yaml
模型选择决策树:

预测类型:
  市场规模预测:
    ├─ 有历史市场数据？
    │  ├─ 是 → 自回归模型 (ARIMA)
    │  └─ 否 ↓
    │  └─ 有类比产品？
    │     ├─ 是 → 类比增长模型
    │     └─ 否 → S 形曲线模型 (Bass/Gompertz)

  用户增长预测:
    ├─ 产品阶段？
    │  ├─ 早期 → 指数增长模型
    │  ├─ 成长期 → Logistic/S 形曲线
    │  └─ 成熟期 → 线性/平稳模型

  收入预测:
    ├─ 有历史收入数据？
    │  ├─ 是 → 时间序列模型
    │  └─ 否 → 自下而上建模
```

### 步骤 2: 数据准备

```yaml
数据收集:
  历史数据:
    - 时间跨度: 至少 12 个月
    - 数据频率: 月度/季度
    - 数据质量: 清洗异常值

  外部变量:
    - 市场增长率
    - 竞品数据
    - 宏观经济指标
    - 行业报告

数据验证:
  平稳性检验:
    - Augmented Dickey-Fuller 检验
    - 趋势和季节性分解

  相关性检验:
    - 变量间相关性
    - 领先/滞后关系
```

### 步骤 3: 执行预测

#### 市场规模预测

```yaml
TAM (Total Addressable Market):
  自上而下法:
    公式: TAM = 目标客户数 × 人均年消费
    示例:
      - 企业数量: 100,000 家
      - 人均年消费: $1,000
      - TAM = $100M

  自下而上法:
    公式: TAM = Σ(细分市场规模)
    步骤:
      1. 识别市场细分
      2. 估算各细分规模
      3. 汇总

SAM (Serviceable Addressable Market):
  定义: 产品可触达的市场
  公式: SAM = TAM × 可触达比例
  因素:
    - 地理限制
    - 行业限制
    - 规模限制

SOM (Serviceable Obtainable Market):
  定义: 短期可获得的市场
  公式: SOM = SAM × 市场份额目标
  因素:
    - 竞争强度
    - 产品差异化
    - 营销能力

增长预测:
  CAGR (复合年增长率):
    公式: CAGR = (终值/初值)^(1/n) - 1

  市场增长率:
    历史增长率: 基于过去 3-5 年
    行业预测: 基于分析师报告
    驱动因素: 技术趋势、政策变化
```

#### 用户增长预测

```yaml
模型类型:

1. 指数增长模型 (早期阶段)
   公式: U(t) = U0 × e^(r×t)
   参数:
     - U0: 初始用户数
     - r: 增长率
     - t: 时间
   适用: 产品发布早期，增长加速

2. Logistic 增长模型 (S 形曲线)
   公式: U(t) = K / (1 + ((K - U0) / U0) × e^(-r×t))
   参数:
     - K: 承载能力 (市场饱和点)
     - U0: 初始用户数
     - r: 增长率
   适用: 成长期到成熟期过渡

3. Bass 扩散模型 (产品采用)
   公式: dN/dt = (p + q×N/K) × (K - N)
   参数:
     - p: 创新系数 (外部影响)
     - q: 模仿系数 (口碑传播)
     - K: 市场潜力
   适用: 新产品扩散预测

4. 自回归模型 (ARIMA)
   公式: ARIMA(p,d,q)
   参数:
     - p: 自回归阶数
     - d: 差分阶数
     - q: 移动平均阶数
   适用: 有历史时间序列数据

预测流程:
  1. 参数校准:
     - 使用历史数据拟合模型
     - 最小化预测误差

  2. 情景分析:
     - 乐观情景: 高增长假设
     - 基准情景: 现有趋势延续
     - 悲观情景: 低增长假设

  3. 敏感性分析:
     - 关键参数变化的影响
     - 识别最关键的假设
```

#### 收入预测

```yaml
自下而上建模:
  基本公式:
    收入 = 用户数 × ARPU

  分层建模:
    免费用户:
      - 用户数预测
      - 转化率

    付费用户:
      - 新增付费用户
      - 续约率
      - 流失率

    收入构成:
      - 订阅收入
      - 增购/交叉销售
      - 广告收入
      - 其他收入

ARPU 预测:
  驱动因素:
    - 定价策略
    - 套餐选择
    - 使用频率

  预测方法:
    - 历史趋势外推
    - 定价变化影响
    - 套餐迁移影响

LTV (Lifetime Value) 预测:
  公式: LTV = ARPU × 用户生命周期

  用户生命周期:
    公式: 生命周期 = 1 / 流失率

  简化 LTV:
    公式: LTV = ARPU / 流失率

  LTV 预测:
    - 基于历史留存曲线
    - 按用户群分层
    - 考虑季节性

收入预测模型:
  短期 (1-3 个月):
    - 时间序列模型
    - 季节性调整

  中期 (3-12 个月):
    - 分层用户增长 + ARPU
    - 考虑产品路线图

  长期 (1-3 年):
    - 市场份额预测
    - 定价策略演进
    - 新产品线
```

#### 趋势外推

```yaml
移动平均法:
  简单移动平均 (SMA):
    公式: SMA = Σ(x_i) / n
    适用: 稳定趋势

  加权移动平均 (WMA):
    公式: WMA = Σ(w_i × x_i) / Σ(w_i)
    适用: 近期数据更重要

  指数移动平均 (EMA):
    公式: EMA_t = α × x_t + (1-α) × EMA_{t-1}
    适用: 平滑短期波动

趋势分解:
  加性模型:
    Y = T + S + R
    - T: 趋势项
    - S: 季节项
    - R: 随机项

  乘性模型:
    Y = T × S × R
    适用: 季节性幅度随趋势变化

回归预测:
  线性回归:
    公式: y = a + bx
    适用: 线性趋势

  多项式回归:
    公式: y = a + bx + cx² + ...
    适用: 非线性趋势

  指数回归:
    公式: y = a × e^(bx)
    适用: 指数增长/衰减
```

### 步骤 4: 情景分析

```yaml
情景构建:
  乐观情景:
    假设:
      - 市场接受度高于预期
      - 竞争压力较小
      - 营销效率高
    输入参数调整: +20-50%

  基准情景:
    假设:
      - 按历史趋势延续
      - 市场条件不变
      - 执行按计划
    输入参数: 基准值

  悲观情景:
    假设:
      - 市场接受度低于预期
      - 竞争加剧
      - 宏观经济下行
    输入参数调整: -20-50%

蒙特卡洛模拟:
  步骤:
    1. 定义关键参数的概率分布
    2. 随机抽样 (1000+ 次)
    3. 计算每次模拟的结果
    4. 统计结果分布

  输出:
    - 预期值 (均值)
    - 置信区间 (50%, 80%, 95%)
    - 风险评估
```

### 步骤 5: 敏感性分析

```yaml
单因素敏感性:
  方法: 每次改变一个参数

  输入:
    - 参数: 用户增长率
    - 范围: ±20%
    - 步长: 5%

  输出:
    - 龙卷风图
    - 敏感性系数
    - 关键驱动因素识别

多因素敏感性:
  方法: 同时改变多个参数

  场景矩阵:
    | 增长率 \ 流失率 | 低 | 基准 | 高 |
    |-----------------|-----|------|-----|
    | 高              |     |      |     |
    | 基准            |     |      |     |
    | 低              |     |      |     |

  最优/最差情景识别
```

### 步骤 6: 预测评估

```yaml
模型评估指标:
  MAE (平均绝对误差):
    公式: MAE = Σ|y - ŷ| / n

  RMSE (均方根误差):
    公式: RMSE = √(Σ(y - ŷ)² / n)

  MAPE (平均绝对百分比误差):
    公式: MAPE = Σ|(y - ŷ) / y| × 100% / n

  判断标准:
    - MAPE < 10%: 高精度
    - 10% ≤ MAPE < 20%: 良好
    - 20% ≤ MAPE < 50%: 合理
    - MAPE ≥ 50%: 低精度

预测区间:
  置信区间:
    - 50% 置信区间: 可能性中等
    - 80% 置信区间: 高可能性
    - 95% 置信区间: 极高可能性

  预测不确定性:
    来源:
      - 参数不确定性
      - 模型不确定性
      - 外部环境变化
```

## Forecast API

### 调用格式 - 市场规模预测

```yaml
forecast_engine:
  action: "market_size"
  methodology: "bottom_up"

  inputs:
    market_segments:
      - name: "中小企业"
        company_count: 100000
        penetration_rate: 0.05
        avg_contract_value: 1000

      - name: "大型企业"
        company_count: 1000
        penetration_rate: 0.10
        avg_contract_value: 50000

    assumptions:
      market_growth_rate: 0.15  # 15% CAGR
      forecast_years: 5

  options:
    scenarios: ["optimistic", "baseline", "pessimistic"]
    confidence_level: 0.80
```

### 调用格式 - 用户增长预测

```yaml
forecast_engine:
  action: "user_growth"
  model: "logistic"

  inputs:
    current_users: 10000
    growth_rate: 0.10  # 月度 10%
    market_potential: 1000000  # 承载能力 K
    forecast_months: 24

  options:
    include_seasonality: true
    scenarios:
      optimistic:
        growth_rate: 0.15
      baseline:
        growth_rate: 0.10
      pessimistic:
        growth_rate: 0.05
```

### 调用格式 - 收入预测

```yaml
forecast_engine:
  action: "revenue"
  methodology: "bottom_up"

  inputs:
    user_growth:
      current_users: 10000
      monthly_growth_rate: 0.08
      churn_rate: 0.02

    monetization:
      free_to_paid_conversion: 0.05
      arpu_free: 0
      arpu_paid: 50

    forecast_period:
      start: "2024-01-01"
      end: "2024-12-31"
      granularity: "monthly"

  options:
    include_seasonality: true
    confidence_intervals: [0.50, 0.80, 0.95]
```

### 返回格式

```yaml
result:
  success: true
  forecast_type: "user_growth"
  model: "logistic"

  summary:
    forecast_period: "2024-01-01 to 2025-12-31"
    current_users: 10000
    projected_users: 45000
    growth_rate: 123%

  scenarios:
    optimistic:
      final_users: 60000
      cagr: 82%

    baseline:
      final_users: 45000
      cagr: 68%

    pessimistic:
      final_users: 25000
      cagr: 42%

  confidence_intervals:
    p50: [38000, 52000]
    p80: [32000, 58000]
    p95: [25000, 65000]

  monthly_breakdown:
    - month: "2024-01"
      users_baseline: 10800
      users_optimistic: 11500
      users_pessimistic: 10200

    # ... 更多月份

  sensitivity_analysis:
    most_sensitive_parameter: "growth_rate"
    sensitivity_ranking:
      - parameter: "growth_rate"
        impact: "high"
        range: "+/- 40%"

      - parameter: "churn_rate"
        impact: "medium"
        range: "+/- 15%"

  key_assumptions:
    - "市场接受度符合基准情景"
    - "竞争格局保持稳定"
    - "无重大监管变化"

  risks:
    - type: "execution"
      description: "获客效率低于预期"
      mitigation: "多渠道测试，优化转化"

    - type: "market"
      description: "竞争对手推出类似产品"
      mitigation: "加速产品差异化"

  recommendations:
    short_term:
      - "验证增长假设"
      - "监控关键指标"

    medium_term:
      - "调整营销投入"
      - "优化产品路线图"
```

## 预测模板

### 市场规模预测模板

```markdown
# 市场规模预测

## 方法论

**方法**: 自下而上
**数据来源**: {{data_sources}}
**预测期**: {{forecast_period}}

## TAM (总可寻址市场)

| 细分市场 | 客户数量 | 人均消费 | 市场规模 |
|---------|---------|---------|---------|
{{#each tam_segments}}
| {{name}} | {{count}} | {{arpu}} | {{size}} |
{{/each}}

**TAM 总计**: {{tam_total}}

## SAM (可服务市场)

**可触达比例**: {{reachable_percentage}}%

| 限制因素 | 影响 |
|---------|------|
{{#each sam_constraints}}
| {{factor}} | {{impact}} |
{{/each}}

**SAM 总计**: {{sam_total}}

## SOM (可获得市场)

**目标市场份额**: {{market_share_goal}}%

| 年份 | 市场规模 | 目标份额 | SOM |
|------|---------|---------|-----|
{{#each som_forecast}}
| {{year}} | {{market_size}} | {{share}} | {{som}} |
{{/each}}

## 增长假设

| 假设 | 基准 | 乐观 | 悲观 |
|------|------|------|------|
{{#each growth_assumptions}}
| {{name}} | {{baseline}} | {{optimistic}} | {{pessimistic}} |
{{/each}}

## 风险与不确定性

{{#each risks}}
- **{{type}}**: {{description}}
  - 缓解措施: {{mitigation}}
{{/each}}
```

### 用户增长预测模板

```markdown
# 用户增长预测

## 模型选择

**模型**: {{model_type}}
**适用理由**: {{model_rationale}}

## 当前状况

| 指标 | 值 |
|------|---|
| 当前用户数 | {{current_users}} |
| 月增长率 | {{growth_rate}}% |
| 流失率 | {{churn_rate}}% |
| 产品阶段 | {{stage}} |

## 增长预测

### 基准情景

{{#each baseline_forecast}}
- **{{month}}**: {{users}} 用户 (增长 {{growth}}%)
{{/each}}

### 情景对比

| 月份 | 悲观 | 基准 | 乐观 |
|------|------|------|------|
{{#each scenario_comparison}}
| {{month}} | {{pessimistic}} | {{baseline}} | {{optimistic}} |
{{/each}}

## 关键驱动因素

| 因素 | 影响 | 敏感性 |
|------|------|--------|
{{#each drivers}}
| {{name}} | {{impact}} | {{sensitivity}} |
{{/each}}

## 置信区间

{{#each confidence_intervals}}
- **{{level}}% 置信**: {{range}} 用户
{{/each}}
```

### 收入预测模板

```markdown
# 收入预测

## 方法论

**方法**: {{methodology}}
**预测期**: {{forecast_period}}

## 收入构成

### 订阅收入

| 用户群 | 用户数 | ARPU | 月度收入 |
|--------|-------|------|---------|
{{#each subscription_revenue}}
| {{segment}} | {{users}} | ${{arpu}} | ${{revenue}} |
{{/each}}

**订阅收入总计**: ${{total_subscription}}

### 其他收入

{{#each other_revenue}}
- **{{source}}**: ${{amount}}
{{/each}}

**总收入**: ${{total_revenue}}

## 月度预测

| 月份 | 收入 | 环比增长 | 同比增长 |
|------|------|---------|---------|
{{#each monthly_forecast}}
| {{month}} | ${{revenue}} | {{mom}}% | {{yoy}}% |
{{/each}}

## 关键假设

{{#each assumptions}}
- **{{name}}**: {{description}} (基准: {{baseline}})
{{/each}}

## 敏感性分析

{{#each sensitivity}}
- **{{parameter}}** 变化 ±{{change}}%: 收入影响 ±{{impact}}%
{{/each}}
```

## 常见预测场景

### 场景 1: 新产品市场规模预测

```
问题: 新产品 TAM/SAM/SOM 是多少？

流程:
  1. 定义目标客户
  2. 估算客户数量
  3. 计算人均消费
  4. 应用可触达比例
  5. 设定市场份额目标

输出: TAM/SAM/SOM + 增长预测
```

### 场景 2: 用户增长规划

```
问题: 明年能获得多少用户？

流程:
  1. 分析历史增长
  2. 选择增长模型
  3. 校准模型参数
  4. 运行情景分析
  5. 评估风险

输出: 用户增长曲线 + 置信区间
```

### 场景 3: 收入预测

```
问题: 明年收入会是多少？

流程:
  1. 预测用户增长
  2. 估算 ARPU
  3. 考虑定价变化
  4. 分收入类型建模
  5. 汇总收入预测

输出: 月度/季度收入预测
```

## 最佳实践

✅ **DO**:
- 使用多种方法交叉验证
- 明确所有假设和前提
- 提供情景和置信区间
- 定期回顾和更新预测
- 记录预测准确率

❌ **DON'T**:
- 只提供单一数字
- 忽视不确定性
- 过度拟合历史数据
- 忽视外部环境变化
- 假设趋势永远延续

## 预测准确率评估

```yaml
评估周期:
  - 月度: 短期预测
  - 季度: 中期预测
  - 年度: 长期预测

准确率目标:
  - 短期 (1-3 月): MAPE < 10%
  - 中期 (3-12 月): MAPE < 20%
  - 长期 (1-3 年): MAPE < 30%

改进循环:
  1. 预测 → 2. 实际 → 3. 对比 → 4. 分析 → 5. 改进
```

## 集成点

此引擎被以下技能使用：
- **research-assistant**: 市场规模预测
- **prd-generator**: 成功指标和目标设定
- **priority-evaluator**: 资源分配预测
- **orchestrator**: 规划工作流

## 测试示例

```bash
# 市场规模预测
forecast-engine market \
  --method bottom_up \
  --segments data/segments.json

# 用户增长预测
forecast-engine users \
  --model logistic \
  --current 10000 \
  --rate 0.10 \
  --months 24

# 收入预测
forecast-engine revenue \
  --users 10000 \
  --arpu 50 \
  --growth 0.08 \
  --period 12m
```
