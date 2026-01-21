---
name: threat-modeling
description: STRIDE/DREAD威胁建模专家 - 6类威胁识别、风险量化评估、缓解措施、攻击场景分析
version: 1.0.0
author: oh-my-pm-skills
tags: [security, threat-modeling, stride, dread, risk-assessment, attack-vectors, mitigation]
allowed-tools: Read, Write, Edit
model: inherit
---

# Threat Modeling

威胁建模技能负责使用 STRIDE 和 DREAD 方法论对系统进行威胁分析、风险评估和缓解措施建议。

## When to Use This Skill

用户请求以下功能时激活此技能：
- "威胁建模"
- "安全威胁分析"
- "STRIDE 分析"
- "DREAD 评估"
- "风险评估"
- "threat model"
- "security threats"

## Core Process

### 步骤 1: 理解系统上下文

```yaml
系统信息收集:
  系统边界:
    - 系统名称和目的
    - 主要组件和模块
    - 数据流和交互
    - 信任边界

  资产识别:
    - 关键资产 (数据、功能、资源)
    - 资产价值 (高/中/低)
    - 资产敏感度 (公开/内部/机密/绝密)

  用户角色:
    - 管理员
    - 普通用户
    - 第三方集成
    - 匿名访问

  技术栈:
    - 编程语言和框架
    - 数据库和存储
    - API 和协议
    - 第三方依赖
```

### 步骤 2: STRIDE 威胁分析

#### STRIDE 分类

```yaml
Spoofing (伪装) - S:
  定义: 攻击者冒充合法用户或系统

  攻击向量:
    - 用户身份冒充
    - API 密钥窃取
    - 证书伪造
    - IP 地址欺骗

  示例场景:
    - 攻击者使用被盗凭证登录
    - 中间人攻击拦截通信
    - 伪造 API 请求

Tampering (篡改) - T:
  定义: 攻击者未经授权修改数据或代码

  攻击向量:
    - 数据包修改
    - 数据库注入
    - 代码篡改
    - 配置修改

  示例场景:
    - SQL 注入修改数据
    - XSS 修改页面内容
    - 中间人修改 API 响应

Repudiation (抵赖) - R:
  定义: 用户否认执行过某操作

  攻击向量:
    - 缺少审计日志
    - 日志被篡改
    - 无法追溯操作

  示例场景:
    - 用户删除数据后无法证明
    - 管理员操作无记录
    - 关键操作无签名

Information Disclosure (信息泄露) - I:
  定义: 敏感信息被未授权方获取

  攻击向量:
    - 数据库泄露
    - 日志暴露
    - 错误信息泄露
    - 侧信道攻击

  示例场景:
    - SQL 注入获取用户数据
    - 错误页面暴露堆栈信息
    - 日志文件包含密码

Denial of Service (拒绝服务) - D:
  定义: 系统无法为合法用户提供服务

  攻击向量:
    - 资源耗尽
    - 洪水攻击
    - 逻辑炸弹
    - 缓冲区溢出

  示例场景:
    - DDoS 攻击
    - 资源泄漏导致崩溃
    - 恶意请求耗尽 CPU

Elevation of Privilege (权限提升) - E:
  定义: 攻击者获得更高权限

  攻击向量:
    - 提权漏洞
    - 权限绕过
    - 会话劫持
    - 越权访问

  示例场景:
    - 普通用户访问管理员功能
    - 会话固定攻击
    - IDOR 漏洞
```

#### STRIDE 分析步骤

```yaml
1. 绘制数据流图 (DFD):
   - 识别外部实体
   - 识别处理过程
   - 识别数据存储
   - 识别数据流

2. 对每个元素应用 STRIDE:
   - 进程: STRIDE 全部
   - 数据存储: TIR
   - 数据流: TID
   - 外部实体: S

3. 记录威胁:
   - 威胁描述
   - 影响范围
   - 攻击难度
   - 现有控制
```

### 步骤 3: DREAD 风险评估

```yaml
DREAD 评分维度:

Damage (潜在损害) - 1-10 分:
  10: 完全系统控制、数据全部泄露
  9: 关键业务功能瘫痪
  8: 敏感数据大规模泄露
  7: 部分敏感数据泄露
  6: 非敏感数据泄露
  5: 业务功能部分受限
  4: 服务轻微中断
  3: 非关键数据泄露
  2: 极小影响
  1: 几乎无影响

Reproducibility (可复现性) - 1-10 分:
  10: 任何人都可以轻松复现
  8: 需要一些技术能力
  6: 需要特定条件
  4: 需要专业工具
  2: 难以复现
  1: 几乎不可能复现

Exploitability (可利用性) - 1-10 分:
  10: 远程、无需认证、自动化工具
  8: 远程、需要认证
  6: 本地、需要用户交互
  4: 本地、需要特定权限
  2: 需要物理访问
  1: 理论上可能

Affected Users (受影响用户) - 1-10 分:
  10: 所有用户 (100%)
  8: 大多数用户 (50-90%)
  6: 部分用户 (10-49%)
  4: 少数用户 (1-9%)
  2: 极少数用户 (<1%)
  1: 个别用户

Discoverability (可发现性) - 1-10 分:
  10: 公开已知、有漏洞利用工具
  8: 公开已知、需要定制
  6: 可能在公开渠道发现
  4: 需要深入分析
  2: 非常难以发现
  1: 几乎不可能发现
```

#### DREAD 计算和风险等级

```yaml
DREAD 分数 = (Damage + Reproducibility + Exploitability + Affected + Discoverability) / 5

风险等级:
  高风险 (8-10 分):
    - 必须修复
    - 阻塞发布
    - 需要紧急处理

  中风险 (5-7 分):
    - 应该修复
    - 计划修复
    - 需要监控

  低风险 (1-4 分):
    - 可以接受
    - 记录备案
    - 可选修复
```

### 步骤 4: 生成缓解措施

```yaml
针对 STRIDE 的缓解措施:

Spoofing (S):
  - 强身份验证 (MFA)
  - 证书验证
  - API 密钥管理
  - 设备指纹

Tampering (T):
  - 数据加密 (传输和存储)
  - 数字签名
  - 完整性校验
  - 代码签名
  - 输入验证

Repudiation (R):
  - 审计日志
  - 不可变日志
  - 操作签名
  - 追踪和监控

Information Disclosure (I):
  - 数据加密
  - 访问控制
  - 数据脱敏
  - 安全日志
  - 错误处理

Denial of Service (D):
  - 速率限制
  - 资源配额
  - 负载均衡
  - DDoS 防护
  - 资源监控

Elevation of Privilege (E):
  - 最小权限原则
  - 权限隔离
  - 会话管理
  - 访问控制
  - 定期审计
```

### 步骤 5: 调用引擎生成报告

```yaml
工作流:
  1. qa_engine:
      action: "validate_system_info"
      检查系统信息完整性

  2. scoring_engine:
      action: "dread_scoring"
      计算每个威胁的 DREAD 分数

  3. template_engine:
      action: "render"
      template: "threat-stride"
      生成威胁模型报告

  4. document_engine:
      action: "create"
      type: "threat_model"
      输出最终报告
```

## 威胁建模模板

```markdown
# {{project_name}} - STRIDE 威胁建模报告

**版本**: {{version}}
**日期**: {{date}}
**作者**: {{author}}
**框架**: STRIDE + DREAD

---

## 执行摘要

{{summary}}

**关键发现**:
{{#each key_findings}}
- {{.}}
{{/each}}

**风险统计**:
- 高风险威胁: {{high_risk_count}}
- 中风险威胁: {{medium_risk_count}}
- 低风险威胁: {{low_risk_count}}

---

## 系统概览

### 系统架构

{{architecture_diagram}}

### 系统边界

{{#each system_boundaries}}
#### {{name}}

**类型**: {{type}}
**描述**: {{description}}

**信任级别**: {{trust_level}}

**数据流**:
{{#each data_flows}}
- {{from}} → {{to}}: {{data}} ({{protocol}})
{{/each}}

**关键资产**:
{{#each assets}}
- {{name}} ({{sensitivity}}, {{value}})
{{/each}}

{{/each}}

---

## STRIDE 威胁分析

### 1. Spoofing (伪装)

{{#each spoofing_threats}}
#### {{title}}

**描述**: {{description}}

**目标组件**: {{target_component}}

**攻击场景**: {{attack_scenario}}

**现有控制**: {{existing_controls}}

**DREAD 评分**: {{dread_score}} / 10

**风险等级**: {{risk_level}}

**缓解措施**:
{{#each mitigations}}
- {{measure}} (优先级: {{priority}})
{{/each}}

**残留风险**: {{residual_risk}}

{{/each}}

### 2. Tampering (篡改)

[格式同上]

### 3. Repudiation (抵赖)

[格式同上]

### 4. Information Disclosure (信息泄露)

[格式同上]

### 5. Denial of Service (拒绝服务)

[格式同上]

### 6. Elevation of Privilege (权限提升)

[格式同上]

---

## DREAD 风险评估

### 风险矩阵

| 威胁 | Damage | Reproducibility | Exploitability | Affected | Discoverability | DREAD | 风险等级 |
|------|--------|----------------|----------------|----------|----------------|-------|----------|
{{#each threat_matrix}}
| {{name}} | {{damage}} | {{reproducibility}} | {{exploitability}} | {{affected}} | {{discoverability}} | {{dread}} | {{level}} |
{{/each}}

### 风险分布

**高风险 (8-10 分)**: {{high_count}} 个
{{#each high_risks}}
- {{name}} ({{dread}} 分)
{{/each}}

**中风险 (5-7 分)**: {{medium_count}} 个
{{#each medium_risks}}
- {{name}} ({{dread}} 分)
{{/each}}

**低风险 (1-4 分)**: {{low_count}} 个
{{#each low_risks}}
- {{name}} ({{dread}} 分)
{{/each}}

---

## 缓解措施

### 立即实施 (高风险)

{{#each immediate_mitigations}}
- [ ] {{title}} (威胁: {{threats}})
  - 描述: {{description}}
  - 优先级: P0
  - 负责人: {{owner}}
  - 截止: {{due_date}}
{{/each}}

### 近期规划 (中风险)

{{#each short_term_mitigations}}
- [ ] {{title}} (威胁: {{threats}})
  - 描述: {{description}}
  - 优先级: P1
  - 负责人: {{owner}}
  - 截止: {{due_date}}
{{/each}}

### 长期考虑 (低风险)

{{#each long_term_mitigations}}
- [ ] {{title}} (威胁: {{threats}})
  - 描述: {{description}}
  - 优先级: P2
  - 负责人: {{owner}}
{{/each}}

---

## 安全控制

### 技术控制

{{#each technical_controls}}
- {{control}}: {{description}}
  - 覆盖威胁: {{threats}}
  - 实施状态: {{status}}
{{/each}}

### 管理控制

{{#each administrative_controls}}
- {{control}}: {{description}}
  - 覆盖威胁: {{threats}}
  - 实施状态: {{status}}
{{/each}}

### 物理控制

{{#each physical_controls}}
- {{control}}: {{description}}
  - 覆盖威胁: {{threats}}
  - 实施状态: {{status}}
{{/each}}

---

## 验证和测试

### 安全测试计划

{{#each security_tests}}
#### {{test_name}}
- 类型: {{type}} (单元/集成/渗透)
- 目标: {{target}}
- 工具: {{tools}}
- 频率: {{frequency}}
{{/each}}

### 验证方法

{{#each verification_methods}}
- {{method}}: {{description}}
{{/each}}

---

## 监控和响应

### 监控指标

{{#each monitoring_metrics}}
- {{metric}}: {{description}}
  - 阈值: {{threshold}}
  - 响应: {{response_action}}
{{/each}}

### 事件响应

{{#each incident_responses}}
#### 威胁类型: {{threat_type}}
- 检测: {{detection}}
- 响应时间: {{response_time}}
- 响应步骤: {{response_steps}}
- 恢复: {{recovery}}
{{/each}}

---

## 合规映射

{{#each compliance_mappings}}
### {{framework}}
{{#each requirements}}
- [ ] {{requirement}}
  - 相关威胁: {{related_threats}}
  - 控制措施: {{controls}}
{{/each}}

{{/each}}

---

## 附录

### 假设和前提

{{#each assumptions}}
- {{assumption}}
{{/each}}

### 使用的工具

{{#each tools_used}}
- {{name}}: {{purpose}}
{{/each}}

### 参考资料

{{#each references}}
- {{title}}: {{url}}
{{/each}}

### 版本历史

| 版本 | 日期 | 变更 | 作者 |
|------|------|------|------|
{{#each version_history}}
| {{version}} | {{date}} | {{changes}} | {{author}} |
{{/each}}

---

*本报告使用 Threat Modeling 技能自动生成*
*评估标准: STRIDE + DREAD*
```

## 交互示例

### 示例 1: Web 应用威胁建模

```
用户: 对我的电商网站做威胁建模

Threat Modeling:
  1. 收集系统信息 (前端、API、数据库、支付)
  2. 绘制数据流图
  3. 应用 STRIDE 分析
  4. DREAD 评分
  5. 生成缓解建议
```

### 示例 2: API 安全分析

```
用户: 分析 REST API 的安全威胁

Threat Modeling:
  1. 识别 API 端点和数据流
  2. 重点分析 S (Spoofing) 和 E (Elevation)
  3. 评估认证和授权机制
  4. 提供安全加固建议
```

### 示例 3: 新功能安全评估

```
用户: 评估"文件上传"功能的安全风险

Threat Modeling:
  1. 分析文件上传数据流
  2. 识别相关威胁 (T, I, D, E)
  3. DREAD 评分
  4. 推荐安全控制
```

## 集成点

**使用的引擎**:
- **qa-engine**: 系统信息验证
- **scoring-engine**: DREAD 评分
- **template-engine**: 报告渲染
- **document-engine**: 报告生成

**与其他技能协作**:
- **prd-generator**: PRD 中的安全章节
- **compliance-checker**: 合规要求的威胁分析
- **impact-analyzer**: 漏洞影响评估

## 最佳实践

✅ **DO**:
- 早期进行威胁建模（设计阶段）
- 绘制清晰的数据流图
- 对所有信任边界建模
- 定期更新威胁模型
- 验证缓解措施有效性

❌ **DON'T**:
- 只关注技术威胁
- 忽视社会工程学
- 过度依赖工具
- 忽视低风险威胁
- 一次建模后从不更新

## 常见威胁模式

### Web 应用威胁

```yaml
认证相关:
  - 弱密码
  - 凭证填充
  - 会话固定
  - CSRF

授权相关:
  - 越权访问
  - 权限提升
  - IDOR
  - 路径遍历

输入验证:
  - SQL 注入
  - XSS
  - 命令注入
  - SSRF
```

### API 威胁

```yaml
认证/授权:
  - API 密钥泄露
  - Token 窃取
  - OAuth 漏洞
  - 权限绕过

数据相关:
  - 敏感数据暴露
  - 批量数据获取
  - 参数污染
  - 注入攻击
```

## 输出格式

```yaml
result:
  success: true
  threat_model:
    project: "{{project_name}}"
    framework: "STRIDE + DREAD"
    total_threats: {{count}}

  risk_summary:
    high: {{count}}
    medium: {{count}}
    low: {{count}}

  prioritized_mitigations:
    immediate: {{count}}
    short_term: {{count}}
    long_term: {{count}}

  report_path: "reports/security/{{project_name}}-threat-model.md"
```

## 测试场景

```bash
# 完整威胁建模
threat-modeling analyze \
  --project "电商网站" \
  --framework STRIDE \
  --methodology DREAD

# 快速威胁评估
threat-modeling quick-assess \
  --feature "文件上传" \
  --focus "T,I,D,E"

# 生成缓解措施
threat-modeling mitigate \
  --threats "SQL注入,XSS" \
  --priority "high"
```
