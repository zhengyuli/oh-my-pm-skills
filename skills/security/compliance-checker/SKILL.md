---
name: compliance-checker
description: 合规检查专家 - SOC2/ISO27001/GDPR框架验证、检查清单生成、差距分析
version: 1.0.0
author: oh-my-pm-skills
tags: [security, compliance, soc2, iso27001, gdpr, audit]
allowed-tools: Read, Write, Edit, WebSearch, mcp__tavily-search__search, mcp__tavily-search__searchContext, mcp__tavily-search__searchQNA, mcp__fetch__fetch
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

## Execution Instructions

**CRITICAL**: 合规框架和法规要求会频繁更新，必须通过实际网络搜索获取最新信息，禁止依赖训练数据生成合规要求。

### 多搜索引擎策略

使用多搜索引擎策略（详见 `shared/search-strategies.yaml#multi_search_engine_strategy`）进行交叉验证，确保法规信息的准确性和时效性。

**快速参考**：
- **WebSearch**（主搜索）- 必须使用
- **Tavily Search**（增强搜索）- 获取法规更新和官方解读
- **Tavily QNA**（事实验证）- 验证关键合规要求
- **mcp__fetch**（内容抓取）- 抓取官方法规文档

### 智能降级策略

智能降级策略（详见 `shared/search-strategies.yaml#intelligent_fallback_strategy`）：

**快速参考**：
- WebSearch 不可用 → 报错停止
- Tavily Search 不可用 → 继续执行，可能缺少深度数据
- Tavily QNA 不可用 → 跳过验证，数据未独立验证
- mcp__fetch 不可用 → 不验证链接，URL 可能失效

### 分层搜索策略

根据数据重要性调整搜索深度（详见 `shared/search-strategies.yaml#tiered_search_strategy`）：

**快速参考**：
- **关键合规数据**（法规更新、官方标准）：2-3 轮搜索
- **重要合规数据**（审计标准、检查清单）：2 轮搜索
- **辅助数据**（合规工具、培训资源）：1 轮搜索

### 执行流程（必须按顺序执行）

#### 阶段一：法规更新搜索

**步骤 1.1**：搜索最新法规更新（关键数据，3 轮搜索）

```yaml
第一轮 - 主搜索:
  工具: WebSearch
  查询: "[框架名称] requirements update [当前年份]"
  进度: [阶段 1/4] 正在搜索 [框架] 最新法规更新...
  输出: [完成] ✓ 已搜索到 X 条更新

第二轮 - 增强搜索（如果 Tavily 可用）:
  工具: mcp__tavily-search__search
  查询: "[框架名称] compliance changes [当前年份] official"
  进度: [进度] 正在深度搜索法规变更细节...
  输出: [完成] ✓ 补充了 X 项变更详情

第三轮 - 官方验证（如果 Fetch 可用）:
  工具: mcp__fetch__fetch
  查询: 官方网站 URL（如 SOC 2: aicpa.org, GDPR: europa.eu, ISO: iso.org）
  进度: [进度] 正在验证官方文档...
  输出: [验证] ✓ 已验证官方要求版本
```

**步骤 1.2**：搜索审计标准更新（关键数据，3 轮搜索）
- 第一轮：`WebSearch` → `"[框架] audit criteria [当前年份]"`
- 第二轮：`mcp__tavily-search__search` → `"[框架] audit requirements checklist [当前年份]"`
- 第三轮：`mcp__fetch__fetch` → 验证官方审计标准文档

**步骤 1.3**：框架特定搜索

对于 **SOC 2**:
```yaml
搜索重点:
  - AICPA Trust Services Criteria 更新
  - SOC 2 Guide 新版本
  - 审计员解释公告
官方来源: aicpa.org
```

对于 **GDPR**:
```yaml
搜索重点:
  - EDPB 指南更新
  - GDPR 第 29 条工作组文件
  - 欧盟法院判例
官方来源: europa.eu, edpb.europa.eu
```

对于 **ISO 27001**:
```yaml
搜索重点:
  - ISO/IEC 27001:2022 更新
  - ISO/IEC 27002 控制措施
  - 认证机构要求
官方来源: iso.org
```

#### 阶段二：行业最佳实践搜索

**步骤 2.1**：搜索合规案例（重要数据，2 轮搜索）
- 第一轮：`WebSearch` → `"[框架] compliance case studies [当前年份]"`
- 第二轮：`mcp__tavily-search__search` → `"[框架] audit best practices lessons learned"`

**步骤 2.2**：搜索常见问题和解决方案（重要数据，2 轮搜索）
- 第一轮：`WebSearch` → `"[框架] common compliance challenges [当前年份]"`
- 第二轮：`mcp__tavily-search__search` → `"[框架] audit failures remediation"`

#### 阶段三：数据整合与标注

**步骤 3.1**：交叉验证合规要求
- 对比多个来源的合规要求
- 如果要求一致：标注 "多源验证"
- 如果要求存在差异：标注 "存在差异，以官方来源为准"

**步骤 3.2**：标注数据质量
```yaml
每个合规要求必须标注:
  来源: [官方文档 / 咨询机构 / 行业协会]
  发布日期: [YYYY-MM]
  更新状态: [最新 / 需要验证 / 已过期]
  搜索方法: [WebSearch / Tavily / Fetch / QNA]
  验证状态: [已验证 / 未验证]
  URL: [官方文档链接（如果可用）]
```

### 进度输出要求

**Level 1：主要阶段进度（默认显示）**
```markdown
[阶段 1/3] 正在搜索 [框架] 最新法规更新...
[阶段 1/3] ✓ 已完成法规更新搜索，发现 X 项变更
[阶段 2/3] 正在搜索行业最佳实践...
[阶段 2/3] ✓ 已收集 X 个合规案例
[阶段 3/3] 正在生成合规检查清单...
[阶段 3/3] ✓ 合规报告已生成
```

**Level 2：详细进度（日志记录）**
```markdown
[搜索] 正在搜索 SOC 2 更新 (WebSearch)...
[完成] ✓ 找到 X 条更新
[搜索] 正在使用 Tavily 深度搜索...
[完成] ✓ 补充了 X 项变更详情
[验证] 正在验证 AICPA 官方文档...
[完成] ✓ 已验证 Trust Services Criteria 版本: 2017 (最新更新: 2024-06)
[链接] 已记录官方文档: https://www.aicpa.org/trust-services-criteria
[搜索] 正在搜索审计标准...
[完成] ✓ 已获取审计标准
[搜索] 正在搜索行业案例...
[完成] ✓ 已收集 X 个案例
[生成] 正在生成合规检查清单...
[完成] ✓ 检查清单已生成
```

### 信息引用要求

**采用分层引用格式，平衡简洁性和可追溯性：**

#### 报告主体中的引用（简洁）
```markdown
SOC 2 Type II 要求日志保留至少 90 天 [AICPA TSC 2017]¹。
GDPR 要求数据泄露通知在 72 小时内完成 [GDPR Art. 33]²。
ISO 27001:2022 要求至少每年进行管理评审 [ISO 27001 Cl. 9.3]³。
```

#### 报告末尾的详细引用（完整）
```markdown
## 参考文献

[1] AICPA, Trust Services Criteria 2017
    - 发布日期: 2017-10 (最新更新: 2024-06)
    - URL: https://www.aicpa.org/trust-services-criteria
    - 访问状态: 公开
    - 搜索日期: 2025-01-22
    - 验证状态: 已通过官方网站验证

[2] European Union, GDPR Article 33
    - 发布日期: 2018-05
    - URL: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32016R0679
    - 访问状态: 公开
    - 搜索日期: 2025-01-22
    - 验证状态: 已验证

[3] ISO/IEC, ISO/IEC 27001:2022
    - 发布日期: 2022-10
    - URL: https://www.iso.org/standard/27001
    - 访问状态: 需要购买
    - 搜索日期: 2025-01-22
    - 验证状态: 未验证（需付费访问）
```

#### 独立的 URL 清单文件
```markdown
文件: outputs/references/urls/YYYY-MMDD-[framework]-sources.md
用途: 批量验证、下载、归档
格式: Markdown 表格（# | 要求类型 | 来源 | URL | 访问状态 | 验证日期）
```

### 最终输出

- **文件**: `outputs/artifacts/security/compliance/YYYY-MM-DD-[project]-[framework]-report.md`
- **日志**: `outputs/logs/skills/compliance-checker/YYYY-MMDD-execution.log`
- **URL清单**: `outputs/references/urls/YYYY-MMDD-[framework]-sources.md`

**⚠️ 禁止行为**：
- ❌ 仅依赖训练数据生成合规要求
- ❌ 使用过期的法规或标准
- ❌ 不标注法规来源和发布日期
- ❌ 不验证官方文档版本
- ❌ 跳过网络搜索步骤
- ❌ 不报告工具调用进度

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

  report_path: "outputs/artifacts/security/compliance/YYYY-MM-DD-{{project}}-{{framework}}-report.md"
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
