---
name: compliance-checker
description: 合规检查专家 - SOC2/ISO27001/GDPR框架验证、检查清单生成、差距分析
version: 1.0.0
author: oh-my-pm-skills
tags: [security, compliance, soc2, iso27001, gdpr, audit]
allowed-tools: Read, Write, Edit
model: inherit
---

# Compliance Checker

合规检查器负责验证产品是否符合各种合规框架要求，生成检查清单和差距分析报告。

## When to Use This Skill

用户请求以下功能时激活此技能：
- "合规检查"
- "SOC 2 审计"
- "ISO 27001 认证"
- "GDPR 合规"
- "安全合规"
- "compliance check"

## Core Process

### 步骤 1: 识别合规要求

```yaml
合规框架选择:

SOC 2 Type II:
  适用: SaaS 公司、处理客户数据
  范围: 安全、可用性、完整性、保密性、隐私
  审计: 年度第三方审计

ISO 27001:
  适用: 全球性企业、需要国际认可
  范围: 信息安全管理体系 (ISMS)
  认证: 第三方认证审核

GDPR:
  适用: 处理欧盟公民数据
  范围: 个人数据保护
  要求: 合规声明、数据保护官

PCI-DSS:
  适用: 处理支付卡数据
  范围: 卡数据保护
  审计: 季度扫描、年度评估

HIPAA:
  适用: 处理健康信息
  范围: PHI 保护
  要求: 风险评估、审计日志

多框架合规:
  组合多个框架要求
  识别共同控制点
  减少重复工作
```

### 步骤 2: 系统合规评估

```yaml
评估维度:

数据管理:
  - 数据分类和标记
  - 数据保留策略
  - 数据销毁流程
  - 数据传输加密
  - 数据存储加密

访问控制:
  - 身份认证策略
  - 多因素认证 (MFA)
  - 权限最小化
  - 访问定期审查
  - 权限撤销流程

安全监控:
  - 日志记录
  - 异常检测
  - 入侵检测
  - 事件响应
  - 定期审计

变更管理:
  - 变更审批流程
  - 变更记录
  - 回滚计划
  - 影响评估
  - 测试要求

供应商管理:
  - 供应商风险评估
  - 合同要求
  - 定期审查
  - 绩效监控
  - 应急响应

业务连续性:
  - 风险评估
  - 备份策略
  - 灾难恢复
  - 业务连续性计划
  - 定期测试
```

### 步骤 3: 生成检查清单

### SOC 2 检查清单

```yaml
CC (Common Criteria) 映射:

CC1.1: 控制环境
  检查项:
    - [ ] 董事会批准信息安全政策
    - [ ] 指定安全负责人
    - [ ] 定期安全培训
    - [ ] 岗位职责定义
    - [ ] 背景调查流程

CC2.1: 通信规范
  检查项:
    - [ ] 书面安全政策
    - [ ] 政策定期审查
    - [ ] 员工确认政策
    - [ ] 政策变更沟通
    - [ ] 违规后果说明

CC3.1: 风险评估
  检查项:
    - [ ] 年度风险评估
    - [ ] 风险识别和分类
    - [ ] 风险缓解计划
    - [ ] 残留风险接受
    - [ ] 监控和审查

CC6.1: 逻辑和物理访问控制
  检查项:
    - [ ] 用户身份验证
    - [ ] MFA 实施
    - [ ] 权限最小化
    - [ ] 访问定期审查
    - [ ] 特权访问管理

CC6.6: 加密
  检查项:
    - [ ] 传输加密 (TLS 1.2+)
    - [ ] 存储加密 (AES-256)
    - [ ] 密钥管理
    - [ ] 加密算法审查
    - [ ] 证书管理

CC7.2: 系统监控
  检查项:
    - [ ] 日志记录策略
    - [ ] 审计跟踪
    - [ ] 异常检测
    - [ ] 日志保留 (90 天+)
    - [ ] 日志保护

CC8.1: 变更管理
  检查项:
    - [ ] 变更审批流程
    - [ ] 变更测试要求
    - [ ] 变更记录
    - [ ] 回滚计划
    - [ ] 紧急变更流程
```

### ISO 27001 检查清单

```yaml
A.5 安全政策:
  检查项:
    - [ ] 信息安全政策
    - [ ] 政策审查
    - [ ] 政策分配
    - [ ] 政策合规

A.9 访问控制:
  检查项:
    - [ ] 访问控制政策
    - [ ] 用户注册
    - [ ] 特权访问
    - [ ] 密码管理
    - [ ] 访问审查

A.10 密码学:
  检查项:
    - [ ] 加密政策
    - [ ] 密钥管理
    - [ ] 信息加密
    - [ ] 数字签名
    - [ ] 加密算法

A.12 运行安全:
  检查项:
    - [ ] 操作程序
    - [ ] 恶意软件防护
    - [ ] 备份
    - [ ] 日志
    - [ ] 漏洞管理

A.13 通信安全:
  检查项:
    - [ ] 网络控制
    - [ ] 服务安全
    - [ ] 传输隔离
    - [ ] 电子邮件安全
    - [ ] 保密协议

A.14 系统获取:
  检查项:
    - [ ] 安全要求
    - [ ] 供应商关系
    - [ ] 采购审计
    - [ ] 外包协议
    - [ ] 监控和审查
```

### GDPR 检查清单

```yaml
第 1 章: 一般规定
  检查项:
    - [ ] 指定数据保护官 (DPO)
    - [ ] 记录处理活动
    - [ ] 数据保护影响评估 (DPIA)
    - [ ] 合规证明
    - [ ] 跨境数据传输

第 2 章: 数据主体权利
  检查项:
    - [ ] 访问权机制
    - [ ] 更正权机制
    - [ ] 删除权机制 ("被遗忘权")
    - [ ] 限制处理权
    - [ ] 数据可携权
    - [ ] 反对权

第 3 章: 控制者和处理者
  检查项:
    - [ ] 合法处理依据
    - [ ] 同意管理
    - [ ] 儿童数据保护
    - [ ] 处理者合同
    - [ ] 处理活动记录

第 4 章: 数据传输
  检查项:
    - [ ] 充分性决定
    - [ ] 适当保障措施
    - [ ] 约束性企业规则
    - [ ] 标准合同条款
    - [ ] 认证机制

第 5 章: 数据安全
  检查项:
    - [ ] 安全措施实施
    - [ ] 数据加密
    - [ ] 访问控制
    - [ ] 数据匿名化
    - [ ] 假名化

第 6 章: 监管和合规
  检查项:
    - [ ] 数据泄露通知 (72 小时)
    - [ ] 数据保护影响评估
    - [ ] 事先咨询
    - [ ] 行为准则
    - [ ] 认证机制
```

### 步骤 4: 差距分析

```yaml
差距评估:

完全合规 (100%):
  - 所有检查项通过
  - 有文档和证据
  - 定期审查

部分合规 (50-99%):
  - 部分检查项通过
  - 有文档但证据不足
  - 需要改进

不合规 (0-49%):
  - 大部分检查项未通过
  - 缺少文档和证据
  - 需要重大改进

差距报告格式:
  控制点:
    - 要求: {{requirement}}
    - 当前状态: {{current_status}}
    - 证据: {{evidence}}
    - 差距: {{gap}}
    - 改进计划: {{improvement_plan}}
    - 负责人: {{owner}}
    - 截止日期: {{due_date}}
```

### 步骤 5: 调用引擎生成报告

```yaml
工作流:
  1. qa_engine:
      action: "validate_compliance_scope"
      检查合规范围定义

  2. scoring_engine:
      action: "compliance_scoring"
      计算合规分数

  3. template_engine:
      action: "render"
      template: "compliance-{{framework}}"
      生成合规报告

  4. document_engine:
      action: "create"
      type: "compliance_report"
      输出最终报告
```

## 合规报告模板

```markdown
# {{project_name}} - {{framework}} 合规报告

**版本**: {{version}}
**日期**: {{date}}
**作者**: {{author}}
**框架**: {{framework}}

---

## 执行摘要

### 合规状态总览

**总体合规度**: {{compliance_percentage}}%

| 类别 | 合规度 | 状态 |
|------|--------|------|
{{#each categories}}
| {{name}} | {{percentage}}% | {{status}} |
{{/each}}

### 关键发现

**优势**:
{{#each strengths}}
- {{.}}
{{/each}}

**差距**:
{{#each gaps}}
- {{.}} (优先级: {{priority}})
{{/each}}

### 风险评估

**高风险**: {{high_risk_count}} 个
**中风险**: {{medium_risk_count}} 个
**低风险**: {{low_risk_count}} 个

---

## 详细检查清单

### {{category_name}}

{{#each checklist_items}}

#### {{control_id}}: {{title}}

**要求**: {{requirement}}

**当前状态**: {{current_status}}

**证据**:
{{#each evidence}}
- {{name}}: {{location}}
{{/each}}

**差距分析**:
- 差距: {{gap_description}}
- 影响: {{impact}}
- 优先级: {{priority}}

**改进计划**:
- 行动: {{action}}
- 负责人: {{owner}}
- 截止: {{due_date}}
- 状态: {{status}}

{{/each}}

---

## 合规度分析

### 按类别统计

{{#each category_analysis}}
#### {{name}}

| 子类别 | 合规度 | 检查项 | 通过 | 部分 | 不通过 |
|--------|--------|--------|------|------|--------|
{{#each subcategories}}
| {{name}} | {{percentage}}% | {{total}} | {{passed}} | {{partial}} | {{failed}} |
{{/each}}

{{/each}}

### 趋势分析

```
合规度趋势:
{{#each trend_data}}
{{date}}: {{percentage}}%
{{/each}}
```

**改进率**: {{improvement_rate}}%
**目标**: {{target_percentage}}%

---

## 风险和问题

### 高风险问题

{{#each high_risk_issues}}
#### {{title}}

**类别**: {{category}}
**控制点**: {{control_id}}

**描述**: {{description}}

**影响**: {{impact}}
**可能性**: {{likelihood}}

**缓解措施**:
{{#each mitigations}}
- {{action}} (负责人: {{owner}}, 截止: {{due_date}})
{{/each}}

{{/each}}

### 中风险问题

[格式同上]

### 低风险问题

[格式同上]

---

## 改进路线图

### 第一阶段 (紧急 - 1 个月)

{{#each phase1}}
- [ ] {{title}} ({{control_id}})
  - 负责人: {{owner}}
  - 截止: {{due_date}}
  - 预期改进: {{improvement}}%
{{/each}}

### 第二阶段 (重要 - 3 个月)

{{#each phase2}}
- [ ] {{title}} ({{control_id}})
  - 负责人: {{owner}}
  - 截止: {{due_date}}
  - 预期改进: {{improvement}}%
{{/each}}

### 第三阶段 (优化 - 6 个月)

{{#each phase3}}
- [ ] {{title}} ({{control_id}})
  - 负责人: {{owner}}
  - 截止: {{due_date}}
  - 预期改进: {{improvement}}%
{{/each}}

---

## 审计准备

### 文档清单

{{#each document_checklist}}
- [ ] {{document}}
  - 位置: {{location}}
  - 负责人: {{owner}}
  - 状态: {{status}}
{{/each}}

### 证据收集

{{#each evidence_items}}
- [ ] {{title}}
  - 类型: {{type}} (政策/流程/记录/日志)
  - 位置: {{location}}
  - 期限: {{retention}}
  - 状态: {{status}}
{{/each}}

### 审计演练

{{#each mock_audits}}
#### {{audit_name}}
- 日期: {{date}}
- 范围: {{scope}}
- 审计师: {{auditor}}
- 发现: {{findings}}
- 改进: {{improvements}}
{{/each}}

---

## 培训和意识

### 培训计划

{{#each training_plan}}
#### {{training_name}}
- 目标: {{audience}}
- 频率: {{frequency}}
- 内容: {{content}}
- 完成率: {{completion_rate}}%
{{/each}}

### 意识活动

{{#each awareness_activities}}
- {{title}}: {{description}}
  - 日期: {{date}}
  - 参与率: {{participation}}%
{{/each}}

---

## 监控和度量

### KPI 指标

{{#each kpis}}
- **{{name}}**: {{current}} / {{target}} ({{percentage}}%)
  - 趋势: {{trend}}
  - 行动: {{action}}
{{/each}}

### 定期审查

{{#each reviews}}
#### {{review_type}}
- 频率: {{frequency}}
- 参与者: {{participants}}
- 输出: {{output}}
- 状态: {{status}}
{{/each}}

---

## 附录

### 术语表

{{#each glossary}}
- **{{term}}**: {{definition}}
{{/each}}

### 参考文档

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

*本报告由 Compliance Checker 技能自动生成*
*合规框架: {{framework}}*
```

## 交互示例

### 示例 1: SOC 2 准备

```
用户: 准备 SOC 2 Type II 审计

Compliance Checker:
  1. 识别适用信任标准 (TSC)
  2. 生成检查清单
  3. 进行差距分析
  4. 创建改进计划
  5. 准备审计证据
```

### 示例 2: GDPR 合规

```
用户: 检查产品是否符合 GDPR

Compliance Checker:
  1. 分析数据处理活动
  2. 检查数据主体权利机制
  3. 验证数据处理合法性
  4. 评估跨境传输
  5. 生成合规报告
```

### 示例 3: 多框架合规

```
用户: 同时符合 SOC 2 和 ISO 27001

Compliance Checker:
  1. 映射两个框架的控制点
  2. 识别共同要求
  3. 生成统一检查清单
  4. 减少重复工作
  5. 协调审计计划
```

## 集成点

**使用的引擎**:
- **qa-engine**: 合规范围验证
- **scoring-engine**: 合规度评分
- **template-engine**: 报告渲染
- **document-engine**: 报告生成

**与其他技能协作**:
- **prd-generator**: PRD 中的合规章节
- **threat-modeling**: 威胁到合规要求的映射
- **impact-analyzer**: 合规违规影响评估

## 最佳实践

✅ **DO**:
- 早期开始合规准备
- 定期进行差距评估
- 保持详细文档和证据
- 培训所有员工
- 定期审查和更新

❌ **DON'T**:
- 临时抱佛脚
- 忽视文档证据
- 只关注技术控制
- 忽视管理控制
- 一次审查后就停止

## 合规路线图

### 准备阶段 (3-6 个月)

```yaml
月度任务:
  第 1 个月:
    - 选择审计机构
    - 定义合规范围
    - 进行初步差距分析

  第 2 个月:
    - 实施高优先级控制
    - 创建和更新文档
    - 开始证据收集

  第 3 个月:
    - 完成控制实施
    - 进行内部审计
    - 修复发现的问题

  第 4-6 个月:
    - 模拟审计
    - 完善证据
    - 准备正式审计
```

## 输出格式

```yaml
result:
  success: true
  compliance:
    framework: "{{framework}}"
    overall_compliance: {{percentage}}%
    grade: "{{grade}}"

  summary:
    passed: {{count}}
    partial: {{count}}
    failed: {{count}}

  gaps:
    high_priority: {{count}}
    medium_priority: {{count}}
    low_priority: {{count}}

  roadmap:
    immediate: {{items}}
    short_term: {{items}}
    long_term: {{items}}

  report_path: "reports/compliance/{{framework}}-report.md"
```

## 测试场景

```bash
# SOC 2 检查
compliance-checker assess \
  --framework soc2 \
  --scope "security,availability"

# GDPR 合规
compliance-checker assess \
  --framework gdpr \
  --data-types "personal,sensitive"

# 多框架对比
compliance-checker compare \
  --frameworks "soc2,iso27001" \
  --output "comparison.md"
```
