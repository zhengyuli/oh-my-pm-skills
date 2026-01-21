---
name: impact-analyzer
description: 影响分析专家 - CVSS漏洞评分、业务影响分析、风险评估、优先级排序
version: 1.0.0
author: oh-my-pm-skills
tags: [security, impact-analysis, cvss, risk-assessment, business-impact]
allowed-tools: Read, Write, Edit
model: inherit
---

# Impact Analyzer

影响分析器负责评估安全漏洞和事件的影响，使用 CVSS 评分和业务影响分析提供决策支持。

## When to Use This Skill

用户请求以下功能时激活此技能：
- "评估漏洞影响"
- "CVSS 评分"
- "业务影响分析"
- "风险评估"
- "impact analysis"

## Core Process

### 步骤 1: 收集漏洞信息

```yaml
漏洞基本信息:
  标识符:
    - CVE ID
    - CWE ID
    - 内部跟踪 ID

  描述:
    - 漏洞类型
    - 影响组件
    - 发现日期
    - 公开状态

  技术细节:
    - 攻击向量
    - 复杂度
    - 所需权限
    - 用户交互
    - 影响范围
```

### 步骤 2: CVSS v3.1 评分

#### CVSS 基础指标

```yaml
Attack Vector (AV) - 攻击向量:
  N (Network) - 网络攻击: 0.85
    - 攻击者可远程利用
    - 不需要物理访问或本地访问

  A (Adjacent) - 相邻网络攻击: 0.62
    - 需要同一广播域
    - 如 WiFi、蓝牙

  L (Local) - 本地攻击: 0.55
    - 需要本地访问
    - 如键盘、终端

  P (Physical) - 物理攻击: 0.2
    - 需要物理接触
    - 如 USB 设备

Attack Complexity (AC) - 攻击复杂度:
  L (Low) - 低复杂度: 0.77
    - 可以自动化利用
    - 不需要特殊条件

  H (High) - 高复杂度: 0.44
    - 需要特定条件
    - 难以自动化

Privileges Required (PR) - 所需权限:
  N (None) - 无需权限: 0.85
    - 未认证用户即可利用

  L (Low) - 低权限: 0.62
    - 需要基本用户权限
    - 非管理员

  H (High) - 高权限: 0.27
    - 需要管理员权限

User Interaction (UI) - 用户交互:
  N (None) - 无需交互: 0.85
    - 不需要用户参与

  R (Required) - 需要交互: 0.62
    - 需要用户执行操作
    - 如点击链接

Scope (S) - 影响范围:
  U (Unchanged) - 范围不变: 1.0
    - 只影响 vulnerable component

  C (Changed) - 范围改变: 1.0 (ISS 计算)
    - 影响跨越 trust boundary
    - 影响其他组件

Impact (C/I/A) - 影响:

  Confidentiality (C) - 机密性:
    H (High) - 高影响: 0.56
      完全 loss of confidentiality
      所有数据泄露

    L (Low) - 低影响: 0.22
      部分数据泄露
      有限访问

    N (None) - 无影响: 0
      不影响机密性

  Integrity (I) - 完整性:
    H (High) - 高影响: 0.56
      完全 loss of integrity
      所有数据可被修改

    L (Low) - 低影响: 0.22
      部分数据可被修改

    N (None) - 无影响: 0
      不影响完整性

  Availability (A) - 可用性:
    H (High) - 高影响: 0.56
      完全 loss of availability
      系统完全不可用

    L (Low) - 低影响: 0.22
      性能下降
      部分功能不可用

    N (None) - 无影响: 0
      不影响可用性
```

#### CVSS 评分计算

```yaml
基础评分计算:

Impact Subscore (ISS):
  ISS = 1 - [(1 - ImpactC) × (1 - ImpactI) × (1 - ImpactA)]

  范围: 0 - 1

Impact:
  如果 Scope = Unchanged:
    Impact = ISS
  如果 Scope = Changed:
    Impact = 7.52 × (ISS - 0.029) - 3.25 × (ISS - 0.02)^15

Exploitability:
  Exploitability = 8.22 × AV × AC × PR × UI

Base Score:
  如果 Scope = Unchanged:
    Base = min(10, Impact + Exploitability)
  如果 Scope = Changed:
    Base = min(10, 1.08 × (Impact + Exploitability))

评分范围: 0.0 - 10.0
```

#### 严重性评级

```yaml
CVSS 评分 → 严重性:

  9.0 - 10.0: 严重 (Critical)
    - 必须立即修复
    - 阻塞发布
    - 需要紧急响应

  7.0 - 8.9: 高危 (High)
    - 尽快修复
    - 优先处理
    - 需要计划

  4.0 - 6.9: 中危 (Medium)
    - 应该修复
    - 正常排期
    - 监控状态

  0.1 - 3.9: 低危 (Low)
    - 可以修复
    - 低优先级
    - 记录备案

  0.0: 信息级 (None)
    - 仅信息性
    - 不影响安全
```

### 步骤 3: 业务影响分析

```yaml
业务影响维度:

财务影响:
  直接损失:
    - 收入损失
    - 数据恢复成本
    - 系统修复成本
    - 罚款和赔偿

  间接损失:
    - 客户流失
    - 声誉损失
    - 保险费用增加
    - 机会成本

运营影响:
  服务中断:
    - 系统不可用时间
    - 业务功能受限
    - 生产力下降

  恢复成本:
    - 人力资源
    - 第三方服务
    - 设备更换

合规影响:
  法规违规:
    - GDPR 罚款
    - HIPAA 罚款
    - PCI-DSS 罚款

  合规成本:
    - 审计要求
    - 报告义务
    - 通知成本

声誉影响:
  客户信任:
    - 品牌损害
    - 客户流失率
    - 获取新客户难度

  合作伙伴关系:
    - 合作伙伴损失
    - 合同终止
    - 未来机会损失

人员影响:
  员工影响:
    - 工作中断
    - 压力和士气
    - 培训需求

  客户影响:
    - 服务体验下降
    - 数据泄露风险
    - 信任度下降
```

### 步骤 4: 风险评估

```yaml
风险评估公式:

风险 = 可能性 × 影响

可能性评估:
  5 - 几乎确定: 公开的漏洞利用工具
  4 - 很可能: 已有概念验证代码
  3 - 可能: 理论上可行
  2 - 不太可能: 需要特殊条件
  1 - 极不可能: 需要多个因素

影响评估:
  5 - 灾难性: 业务中断、大量数据泄露
  4 - 重大: 显著财务损失、声誉受损
  3 - 中等: 可衡量的损失
  2 - 较小: 轻微损失
  1 - 可忽略: 几乎无影响

风险矩阵:
  高风险 (15-25): 立即处理
  中风险 (8-14): 计划处理
  低风险 (1-7): 记录监控
```

### 步骤 5: 生成影响报告

```yaml
工作流:
  1. qa_engine:
      action: "validate_vulnerability_info"
      验证漏洞信息

  2. scoring_engine:
      action: "cvss_scoring"
      计算 CVSS 评分

  3. scoring_engine:
      action: "business_impact_scoring"
      评估业务影响

  4. template_engine:
      action: "render"
      template: "impact-analysis"
      生成报告

  5. document_engine:
      action: "create"
      type: "impact_analysis"
      输出报告
```

## 影响分析报告模板

```markdown
# {{vulnerability_title}} - 影响分析报告

**CVE ID**: {{cve_id}}
**分析日期**: {{date}}
**分析师**: {{author}}

---

## 执行摘要

### CVSS 评分

**基础评分**: {{base_score}} / 10
**严重性**: {{severity}} (Critical/High/Medium/Low)

**向量字符串**: {{vector_string}}

### 业务影响

**总体风险**: {{overall_risk}} (高/中/低)

**关键发现**:
{{#each key_findings}}
- {{.}}
{{/each}}

**建议**: {{recommendation}}

---

## CVSS v3.1 评分详情

### 基础指标

| 指标 | 值 | 评分 | 描述 |
|------|-----|------|------|
| Attack Vector (AV) | {{av}} | {{av_score}} | {{av_description}} |
| Attack Complexity (AC) | {{ac}} | {{ac_score}} | {{ac_description}} |
| Privileges Required (PR) | {{pr}} | {{pr_score}} | {{pr_description}} |
| User Interaction (UI) | {{ui}} | {{ui_score}} | {{ui_description}} |
| Scope (S) | {{scope}} | {{scope_score}} | {{scope_description}} |
| Confidentiality (C) | {{c}} | {{c_score}} | {{c_description}} |
| Integrity (I) | {{i}} | {{i_score}} | {{i_description}} |
| Availability (A) | {{a}} | {{a_score}} | {{a_description}} |

### 评分计算

**Impact Subscore (ISS)**: {{iss}}
**Exploitability**: {{exploitability}}
**Base Score**: {{base_score}}

### 严重性等级

```
{{severity_description}}

{{base_score}} / 10
{{severity_lower}}
```

---

## 技术影响

### 受影响组件

{{#each affected_components}}
#### {{name}}

- **版本**: {{version}}
- **位置**: {{location}}
- **配置**: {{configuration}}
- **暴露**: {{exposure}}

{{/each}}

### 攻击场景

{{#each attack_scenarios}}
#### {{scenario_name}}

**前提条件**:
{{#each prerequisites}}
- {{.}}
{{/each}}

**攻击步骤**:
{{#each steps}}
{{index}}. {{step}}
{{/each}}

**影响**: {{impact}}

**可能性**: {{likelihood}}

{{/each}}

### 缓解措施

#### 技术缓解

{{#each technical_mitigations}}
- **{{measure}}**
  - 描述: {{description}}
  - 有效性: {{effectiveness}}
  - 实施复杂度: {{complexity}}
  - 预估时间: {{estimate}}
{{/each}}

#### 配置缓解

{{#each configuration_mitigations}}
- **{{measure}}**
  - 描述: {{description}}
  - 配置变更: {{change}}
{{/each}}

---

## 业务影响分析

### 财务影响

| 影响类别 | 估算损失 | 可能性 | 风险值 |
|---------|---------|--------|--------|
{{#each financial_impact}}
| {{category}} | {{amount}} | {{likelihood}}% | {{risk_value}} |
{{/each}}
| **总计** | **{{total_amount}}** | - | **{{total_risk}}** |

**说明**:
{{#each financial_notes}}
- {{.}}
{{/each}}

### 运营影响

{{#each operational_impact}}
#### {{category}}

**影响描述**: {{description}}

**持续时间**: {{duration}}

**受影响功能**:
{{#each affected_functions}}
- {{function}} (影响: {{impact_level}})
{{/each}}

**恢复成本**: {{recovery_cost}}

**恢复时间**: {{recovery_time}}

{{/each}}

### 合规影响

{{#each compliance_impact}}
#### {{framework}}

**违规类型**: {{violation_type}}

**潜在罚款**: {{potential_fine}}

**其他要求**:
{{#each requirements}}
- [ ] {{requirement}}
  - 截止: {{deadline}}
  - 负责人: {{owner}}
{{/each}}

**通知义务**:
- 通知对象: {{notify_parties}}
- 时间限制: {{notification_deadline}}
- 通知内容: {{notification_content}}

{{/each}}

### 声誉影响

**客户信任**:
- 当前信任度: {{current_trust}}%
- 预期下降: {{expected_decline}}%
- 恢复时间: {{recovery_period}}

**品牌影响**: {{brand_impact}}

**媒体关注**: {{media_attention}}

**客户流失预估**:
- 流失率: {{churn_rate}}%
- 影响客户数: {{affected_customers}}
- 收入影响: {{revenue_impact}}

---

## 风险评估

### 风险矩阵

```
             影响
            高 | 中 | 低
         ----+---+---+---
   很高 |   |   |   |
   可能 | 高 | 中 | 低 |
   可能 |   | 中 | 低 | 低
   不太| 中 | 低 | 低 | 低
   可能|   |   | 低 | 低
         可能性
```

**当前风险等级**: {{current_risk_level}}

### 风险评分

**技术风险**: {{technical_risk}} / 25
**业务风险**: {{business_risk}} / 25
**合规风险**: {{compliance_risk}} / 25
**声誉风险**: {{reputation_risk}} / 25

**总风险评分**: {{total_risk}} / 100

---

## 修复优先级

### 立即修复 (P0)

{{#each p0_fixes}}
#### {{title}} ({{vulnerability_id}})

**理由**:
- CVSS: {{cvss_score}} ({{severity}})
- 业务影响: {{business_impact}}
- 利用可能性: {{exploitability}}

**修复方案**:
- 描述: {{description}}
- 复杂度: {{complexity}}
- 预估时间: {{estimate}}
- 负责人: {{owner}}
- 截止: {{due_date}}

**缓解措施** (临时):
{{#each temporary_mitigations}}
- {{measure}}
{{/each}}

{{/each}}

### 高优先级 (P1)

[格式同 P0]

### 中优先级 (P2)

[格式同 P0]

### 低优先级 (P3)

[格式同 P0]

---

## 监控和检测

### 检测方法

{{#each detection_methods}}
- **{{method}}**
  - 描述: {{description}}
  - 工具: {{tools}}
  - 指标: {{metrics}}
{{/each}}

### 监控指标

{{#each monitoring_metrics}}
- **{{metric}}**
  - 当前值: {{current}}
  - 阈值: {{threshold}}
  - 响应: {{response}}
{{/each}}

---

## 附录

### 术语表

{{#each glossary}}
- **{{term}}**: {{definition}}
{{/each}}

### 参考链接

{{#each references}}
- {{title}}: {{url}}
{{/each}}

### 变更历史

| 版本 | 日期 | 变更 | 作者 |
|------|------|------|------|
{{#each version_history}}
| {{version}} | {{date}} | {{changes}} | {{author}} |
{{/each}}

---

*本报告由 Impact Analyzer 技能自动生成*
*CVSS 版本: 3.1*
```

## 交互示例

### 示例 1: CVE 分析

```
用户: 分析 CVE-2023-1234 的影响

Impact Analyzer:
  1. 获取 CVE 详情
  2. 计算 CVSS v3.1 评分
  3. 评估受影响组件
  4. 分析业务影响
  5. 提供修复建议
```

### 示例 2: 内部漏洞评估

```
用户: 评估发现的 SQL 注入漏洞影响

Impact Analyzer:
  1. 收集漏洞技术细节
  2. 计算 CVSS 评分
  3. 评估数据泄露风险
  4. 分析财务和合规影响
  5. 制定修复优先级
```

### 示例 3: 批量风险评估

```
用户: 评估本周发现的 10 个漏洞

Impact Analyzer:
  1. 收集所有漏洞信息
  2. 计算 CVSS 评分
  3. 评估业务影响
  4. 按风险排序
  5. 生成修复路线图
```

## 集成点

**使用的引擎**:
- **qa-engine**: 漏洞信息验证
- **scoring-engine**: CVSS 和业务影响评分
- **template-engine**: 报告渲染
- **document-engine**: 报告生成

**与其他技能协作**:
- **threat-modeling**: 漏洞到威胁的映射
- **compliance-checker**: 合规违规评估
- **security-use-case-generator**: 验证测试用例

## 最佳实践

✅ **DO**:
- 使用最新 CVSS 版本
- 考虑实际环境因素
- 评估业务影响
- 提供可操作建议
- 定期重新评估

❌ **DON'T**:
- 只看 CVSS 分数
- 忽视业务影响
- 过度或低估风险
- 缺少上下文
- 一次评估后从不更新

## CVSS 评分工具

```bash
# CVSS 计算器
impact-analyzer calculate \
  --cvss-vector "AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H"

# 批量 CVE 分析
impact-analyzer analyze-cve \
  --cve-list "CVE-2023-1234,CVE-2023-5678"

# 内部漏洞评估
impact-analyzer assess \
  --vulnerability "SQL Injection" \
  --context "Production API"
```

## 输出格式

```yaml
result:
  success: true
  analysis:
    cve_id: "{{cve_id}}"
    cvss:
      base_score: {{score}}
      severity: "{{severity}}"
      vector: "{{vector_string}}"

    business_impact:
      financial: {{amount}}
      operational: {{description}}
      compliance: {{frameworks}}
      reputation: {{level}}

    overall_risk: "{{risk_level}}"
    priority: "{{priority}}"

    recommendation: "{{action}}"

  report_path: "reports/impact/{{cve_id}}-analysis.md"
```
