---
name: analytics-engine
description: 数据分析引擎 - 指标计算(DAU/MAU/留存/LTV/CAC)、A/B测试、漏斗分析、异常检测
version: 1.0.0
author: oh-my-pm-skills
tags: [engine, analytics, metrics, insights, ab-testing, funnel, retention, cohort]
allowed-tools: Read, Write, Edit
model: inherit
---

# Analytics Engine

分析引擎负责处理产品数据相关的分析任务，为 PM 提供数据驱动的洞察和决策支持。

## When to Use This Engine

其他技能需要以下功能时调用此引擎：
- 计算产品指标和 KPI
- 分析用户行为数据
- A/B 测试结果分析
- 漏斗分析和转化率计算
- 留存分析和用户分层
- 趋势检测和异常识别

## Core Process

### 步骤 1: 识别分析类型

```yaml
分析类型:
  描述性分析 (Descriptive):
    - 发生了什么？
    - 历史数据总结
    - 基础指标计算

  诊断性分析 (Diagnostic):
    - 为什么发生？
    - 根因分析
    - 相关性分析

  预测性分析 (Predictive):
    - 将会发生什么？
    - 趋势外推
    - 概率预测

  规范性分析 (Prescriptive):
    - 应该做什么？
    - 优化建议
    - 决策支持
```

### 步骤 2: 收集和验证数据

```yaml
数据验证:
  完整性检查:
    - 必需字段是否存在
    - 数据覆盖率是否充足
    - 时间范围是否连续

  质量检查:
    - 异常值检测
    - 重复数据处理
    - 数据类型验证

  统计有效性:
    - 样本量是否足够
    - 置信区间计算
    - 统计显著性检验
```

### 步骤 3: 执行分析

#### 产品指标计算

```yaml
用户增长指标:
  DAU/MAU 比率:
    公式: DAU / MAU
    含义: 用户粘性指标
    基准: 0.2+ (优秀), 0.1-0.2 (良好), <0.1 (需改进)

  用户增长率:
    公式: (新用户 - 流失用户) / 期初用户 × 100%
    分类: 日/周/月增长率

  累计用户数:
    公式: SUM(期间新增用户)
    维度: 总用户 / 活跃用户 / 付费用户

参与度指标:
  会话时长:
    公式: AVG(会话结束时间 - 会话开始时间)
    分类: 平均 / 中位数 / P90

  会话频率:
    公式: 总会话数 / 总用户数
    周期: 日/周/月

  功能使用率:
    公式: 使用功能的用户 / 总用户 × 100%
    维度: 按功能 / 按用户群

  页面/屏幕深度:
    公式: AVG(每会话访问页面数)

留存指标:
  次日留存 (Day 1 Retention):
    公式: 第 2 天活跃用户 / 第 1 天新用户 × 100%

  7 日留存 (Day 7 Retention):
    公式: 第 7 天活跃用户 / 第 1 天新用户 × 100%

  30 日留存 (Day 30 Retention):
    公式: 第 30 天活跃用户 / 第 1 天新用户 × 100%

  留存曲线:
    分析: N 日留存率趋势
    应用: 识别流失模式

转化指标:
  漏斗转化率:
    公式: 进入下一步用户 / 当前步骤用户 × 100%
    分析: 每步转化率、总转化率、流失点

  注册转化率:
    公式: 完成注册用户 / 访问注册页用户 × 100%

  付费转化率:
    公式: 付费用户数 / 活跃用户 × 100%

  购买转化率:
    公式: 完成购买用户 / 进入购买流程用户 × 100%

营收指标:
  ARPU (Average Revenue Per User):
    公式: 总收入 / 总用户数
    周期: 月度 ARPU

  ARPPU (Average Revenue Per Paying User):
    公式: 总收入 / 付费用户数

  LTV (Lifetime Value):
    公式: ARPU × 用户生命周期
    估算: 基于留存和 ARPU 预测

  CAC (Customer Acquisition Cost):
    公式: 获客总成本 / 新增用户数

  LTV/CAC 比率:
    含义: 获客投资回报
    基准: 3+ (健康), 1-3 (需关注), <1 (不可持续)
```

#### A/B 测试分析

```yaml
测试设计验证:
  样本量计算:
    公式: n = (Zα + Zβ)² × (p1(1-p1) + p2(1-p2)) / Δ²
    参数:
      - Zα: 显著性水平 (95% = 1.96)
      - Zβ: 统计功效 (80% = 0.84)
      - p1, p2: 对照组和实验组预期转化率
      - Δ: 最小可检测差异

  随机化检查:
    - 用户分组是否随机
    - 组间分布是否一致
    - 时间分布是否均匀

结果分析:
  基础指标:
    - 对照组转化率: CR_control
    - 实验组转化率: CR_experiment
    - 绝对差异: Δ = CR_exp - CR_ctrl
    - 相对提升: Δ% = (CR_exp - CR_ctrl) / CR_ctrl × 100%

  统计显著性:
    Z 检验:
      公式: Z = (p1 - p2) / √(p(1-p)(1/n1 + 1/n2))
      判断: |Z| > 1.96 → 显著 (p < 0.05)

    置信区间:
      公式: CI = Δ ± 1.96 × SE
      含义: 真实差异有 95% 概率在此区间

  P 值计算:
    - p < 0.01: 极显著 (**)
    - p < 0.05: 显著 (*)
    - p < 0.10: 边缘显著 (†)
    - p ≥ 0.10: 不显著 (ns)

  效应量 (Cohen's d):
    公式: d = (μ1 - μ2) / σ_pooled
    解释:
      - d < 0.2: 小效应
      - 0.2 ≤ d < 0.5: 中等效应
      - d ≥ 0.8: 大效应

结果解读:
  显著 + 正向:
    - 建议: 推全实验组
    - 预期影响: 预估年化收益

  显著 + 负向:
    - 建议: 放弃实验组
    - 分析: 失败原因

  不显著:
    - 建议: 收集更多数据或优化假设
    - 检查: 样本量、测试时长、指标选择
```

#### 漏斗分析

```yaml
漏斗类型:
  转化漏斗:
    - 访问 → 注册 → 激活 → 留存 → 付费

  功能漏斗:
    - 页面访问 → 交互 → 完成操作

  获客漏斗:
    - 曝光 → 点击 → 访问 → 注册

分析指标:
  整体转化率:
    公式: 完成用户 / 入口用户 × 100%

  分步转化率:
    公式: 第 N 步用户 / 第 N-1 步用户 × 100%

  流失率:
    公式: 1 - 转化率

  跳出率:
    公式: 首页退出用户 / 入口用户 × 100%

  平均完成时间:
    公式: AVG(完成时间 - 开始时间)

洞察输出:
  最大流失点:
    - 识别转化率最低的步骤
    - 分析流失原因

  优化机会:
    - 高流失 + 大流量 = 高优先级
    - 计算提升潜力

  用户路径分析:
    - 用户是否按预期路径
    - 是否有意外捷径或绕道
```

#### 留存分析

```yaml
同期群分析 (Cohort Analysis):
  按获客时间分组:
    - 计算每组在不同时间点的留存率
    - 对比不同同期群的表现

  留存热力图:
    - 行: 获客周/月
    - 列: 留存周/月
    - 值: 留存率 (%)

  留存曲线拟合:
    - 指数衰减: R(t) = R0 × e^(-λt)
    - 幂律衰减: R(t) = R0 × t^(-α)
    - 识别最佳拟合模型

留存分层:
  按用户属性:
    - 获客渠道
    - 用户画像
    - 地区/设备

  按行为特征:
    - 首日行为
    - 功能使用
    - 付费状态

  高价值用户识别:
    - 留存 > 阈值
    - 付费意愿
    - 推荐可能性
```

#### 异常检测

```yaml
异常类型:
  突增/突降:
    - 检测: 3-sigma 规则
    - 规则: |x - μ| > 3σ
    - 应用: DAU、营收、错误率

  趋势改变:
    - 检测: CUSUM 控制图
    - 应用: 增长率变化

  周期性异常:
    - 检测: 与历史同期对比
    - 应用: 季节性调整

根因分析:
  维度下钻:
    - 按地区/设备/渠道细分
    - 识别异常贡献者

  相关性分析:
    - 与其他指标的相关性
    - 外部事件关联

  影响评估:
    - 营收影响
    - 用户影响
    - 优先级评估
```

### 步骤 4: 生成洞察

```yaml
洞察框架:
  WHAT (发生了什么):
    - 关键指标变化
    - 数据模式识别

  WHY (为什么发生):
    - 相关性分析
    - 根因假设

  SO WHAT (意味着什么):
    - 业务影响
    - 优先级评估

  NOW WHAT (接下来做什么):
    - 行动建议
    - 实验设计

洞察类型:
  增长机会:
    - 高潜用户群
    - 未充分利用的功能
    - 低竞争市场

  风险预警:
    - 流失征兆
    - 指标下降
    - 用户不满信号

  优化方向:
    - 转化瓶颈
    - 留存驱动因素
    - 功能改进点
```

## Analytics API

### 调用格式 - 基础指标

```yaml
analytics_engine:
  action: "calculate_metrics"
  data:
    source: "user_events"
    time_range: "2024-01-01 to 2024-01-31"
    metrics:
      - "dau"
      - "mau"
      - "retention_d1"
      - "retention_d7"
      - "arpu"

  options:
    compare_with:
      - "previous_period"
      - "same_period_last_year"
    segment_by:
      - "acquisition_channel"
      - "user_type"
```

### 调用格式 - A/B 测试

```yaml
analytics_engine:
  action: "analyze_ab_test"
  test:
    name: "checkout_button_color"
    variants:
      - name: "control"
        users: 10000
        conversions: 500
      - name: "treatment_blue"
        users: 10000
        conversions: 550

  metrics:
    - "conversion_rate"
    - "revenue_per_user"

  options:
    confidence_level: 0.95
    statistical_power: 0.80
    effect_size: "medium"
```

### 调用格式 - 漏斗分析

```yaml
analytics_engine:
  action: "funnel_analysis"
  funnel:
    name: "user_onboarding"
    steps:
      - name: "signup_page_view"
        event: "page_view"
        filter: "page = '/signup'"

      - name: "signup_submit"
        event: "signup_submit"

      - name: "email_verify"
        event: "email_verified"

      - name: "profile_complete"
        event: "profile_completed"

  options:
    time_window: "7 days"
    segment_by: "acquisition_channel"
    include_path_analysis: true
```

### 返回格式

```yaml
result:
  success: true
  analysis_type: "ab_test"

  summary:
    test_name: "checkout_button_color"
    winner: "treatment_blue"
    significance: "significant"
    confidence: 95%
    p_value: 0.003

  metrics:
    control:
      conversion_rate: 5.0%
      users: 10000
      conversions: 500

    treatment_blue:
      conversion_rate: 5.5%
      users: 10000
      conversions: 550

  impact:
    absolute_lift: "+0.5%"
    relative_lift: "+10%"
    estimated_annual_revenue_impact: "+$50,000"

  recommendation: "推荐全量上线 treatment_blue 变体"

  next_actions:
    - "监控上线后指标"
    - "分析不同用户群的表现差异"
    - "规划下一轮优化测试"
```

## 常见分析场景

### 场景 1: 产品健康度检查

```
问题: 产品整体表现如何？

分析:
  1. 计算核心指标 (DAU, MAU, 留存, 营收)
  2. 与历史对比 (趋势)
  3. 识别异常和风险
  4. 生成健康度评分

输出: 产品仪表盘摘要
```

### 场景 2: 功能价值分析

```
问题: 哪些功能最有价值？

分析:
  1. 计算各功能使用率
  2. 分析功能与留存的相关性
  3. 功能满意度评分
  4. 开发成本 vs 用户价值

输出: 功能优先级矩阵
```

### 场景 3: 用户流失预警

```
问题: 如何预测用户流失？

分析:
  1. 历史流失用户行为分析
  2. 识别流失信号特征
  3. 建立流失预测模型
  4. 生成风险用户清单

输出: 流失风险评分 + 挽留策略
```

### 场景 4: 营收增长分析

```
问题: 营收增长来自哪里？

分析:
  1. 营收分解 (新用户 vs 留存用户)
  2. ARPU 趋势
  3. 付费转化率变化
  4. LTV/CAC 比率

输出: 营收驱动力归因
```

## 最佳实践

✅ **DO**:
- 从业务问题开始，而非数据
- 验证数据质量和统计有效性
- 提供可行动的建议
- 可视化关键洞察
- 定期回顾和更新分析

❌ **DON'T**:
- 混淆相关性和因果性
- 忽视统计显著性
- 过度拟合数据
- 只报告数字不讲故事
- 忽视样本偏差

## 统计检验参考

```yaml
Z 检验:
  用途: 大样本比例比较
  条件: n ≥ 30

t 检验:
  用途: 小样本均值比较
  条件: n < 30

卡方检验:
  用途: 分类变量关联性
  示例: 用户群与功能使用

ANOVA:
  用途: 多组均值比较
  示例: 多个 A/B 变体对比

Mann-Whitney U:
  用途: 非参数组间比较
  条件: 数据非正态分布
```

## 集成点

此引擎被以下技能使用：
- **research-assistant**: 市场数据分析
- **priority-evaluator**: 数据驱动优先级
- **prd-generator**: 成功指标定义
- **jtbd-analyzer**: 用户行为分析

## 测试示例

```bash
# 计算产品指标
analytics-engine metrics \
  --type retention \
  --period 30d

# 分析 A/B 测试
analytics_engine ab_test \
  --control data/control.csv \
  --treatment data/variant.csv \
  --metric conversion_rate

# 漏斗分析
analytics_engine funnel \
  --steps "view,click,purchase" \
  --segment_by channel
```
