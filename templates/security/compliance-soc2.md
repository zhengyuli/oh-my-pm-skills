# {{project_name}} - SOC 2 合规检查清单

**版本**: {{version}}
**日期**: {{date}}
**报告类型**: SOC 2 Type {{soc2_type}}
**准备状态**: {{status}}

---

## 执行摘要

### 合规状态总览

| 准则 | 控制点 | 通过 | 进行中 | 不适用 | 完成率 |
|------|--------|------|--------|--------|--------|
{{#each criteria_summary}}
| {{criterion}} | {{total}} | {{passed}} | {{in_progress}} | {{na}} | {{completion}}% |
{{/each}}

**总体完成率**: {{overall_completion}}%

### 关键发现

{{#each key_findings}}
- **{{finding}}**: {{severity}} (优先级: {{priority}})
{{/each}}

### 行动建议

{{#each recommendations}}
- [ ] {{recommendation}} (优先级: {{priority}}, 负责人: {{owner}})
{{/each}}

---

## 信任服务准则 (TSC)

### CC1.1 安全策略

#### 控制要求

组织应记录、发布并维护涵盖所有信任服务准则的安全策略。

**实施状态**: {{cc1_1_status}}

**证据**:
{{#each cc1_1_evidence}}
- [ ] {{evidence_item}} (位置: {{location}})
{{/each}}

**控制措施**:
{{#each cc1_1_controls}}
- **{{control}}**: {{description}} (状态: {{status}})
{{/each}}

**负责人**: {{owner}}
**审查周期**: {{review_cycle}}

---

### CC2.1 通信安全

#### 控制要求

在公共网络和受信任网络之间传输数据时，应实施加密机制。

**实施状态**: {{cc2_1_status}}

**加密配置**:
{{#each cc2_1_encryption}}
- **{{use_case}}**: {{algorithm}} ({{key_size}} 位密钥)
{{/each}}

**证据**:
{{#each cc2_1_evidence}}
- [ ] {{evidence_item}}
{{/each}}

---

### CC3.1 数据加密

#### 控制要求

存储的敏感数据应使用加密机制保护。

**实施状态**: {{cc3_1_status}}

**数据分类与加密**:
| 数据类型 | 加密要求 | 算法 | 状态 |
|---------|---------|------|------|
{{#each cc3_1_data_classification}}
| {{type}} | {{requirement}} | {{algorithm}} | {{status}} |
{{/each}}

**密钥管理**:
- 密钥轮换: {{key_rotation}}
- 密钥存储: {{key_storage}}
- 访问控制: {{key_access_control}}

---

### CC4.1 访问控制

#### 控制要求

系统应基于唯一用户身份实施访问控制。

**实施状态**: {{cc4_1_status}}

**访问控制模型**: {{access_control_model}}

**权限矩阵**:
| 资源 | 角色 | 权限 | 审批要求 |
|------|------|------|---------|
{{#each cc4_1_permissions}}
| {{resource}} | {{role}} | {{permission}} | {{approval}} |
{{/each}}

**证据**:
{{#each cc4_1_evidence}}
- [ ] {{evidence_item}}
{{/each}}

---

### CC5.1 监控

#### 控制要求

系统应监控安全相关事件并记录监控日志。

**实施状态**: {{cc5_1_status}}

**监控事件**:
{{#each cc5_1_events}}
- **{{event}}**: {{description}} (告警: {{alert}})
{{/each}}

**日志配置**:
- 保留期: {{log_retention}}
- 日志级别: {{log_level}}
- 日志存储: {{log_storage}}

---

### CC6.1 事件响应

#### 控制要求

组织应建立和记录事件响应程序。

**实施状态**: {{cc6_1_status}}

**响应流程**:
{{#each cc6_1_response_steps}}
{{step}}. {{step_name}}
   - 触发: {{trigger}}
   - 行动: {{action}}
   - 负责人: {{owner}}
   - 时限: {{timeline}}
{{/each}}

**演练记录**:
{{#each cc6_1_drills}}
- **{{drill_type}}**: {{date}} (参与人: {{participants}})
{{/each}}

---

### CC7.1 变更管理

#### 控制要求

系统变更应经过授权、测试和追踪。

**实施状态**: {{cc7_1_status}}

**变更流程**:
```
变更请求 → 风险评估 → 变更审批 → 变更测试 → 变更部署 → 变更验证
```

**变更记录**:
{{#each cc7_1_changes}}
- **{{change}}**: {{date}} (审批人: {{approver}})
{{/each}}

---

### CC8.1 风险评估

#### 控制要求

组织应识别和评估安全风险。

**实施状态**: {{cc8_1_status}}

**风险登记**:
| 风险 | 可能性 | 影响 | 风险等级 | 缓解措施 | 状态 |
|------|--------|------|---------|---------|------|
{{#each cc8_1_risks}}
| {{risk}} | {{probability}} | {{impact}} | {{level}} | {{mitigation}} | {{status}} |
{{/each}}

---

## 控制活动详细检查

### 安全策略

**文档**: {{security_policy_doc}}

**检查项**:
{{#each security_policy_checks}}
- [ ] {{check}} (状态: {{status}}, 负责人: {{owner}})
{{/each}}

**更新周期**: {{update_cycle}}

---

### 访问控制

**检查项**:
{{#each access_control_checks}}
- [ ] {{check}}
{{/each}}

**访问审查**:
- 审查频率: {{access_review_frequency}}
- 上次审查: {{last_review_date}}
- 下次审查: {{next_review_date}}

---

### 数据加密

**加密清单**:
{{#each encryption_checklist}}
- [ ] **{{data_type}}**: {{location}} ({{algorithm}})
{{/each}}

**密钥管理**:
- 密钥生成: {{key_generation}}
- 密钥分发: {{key_distribution}}
- 密钥销毁: {{key_destruction}}

---

### 监控和日志

**日志范围**:
{{#each logging_scope}}
- **{{system}}**: {{events}}
{{/each}}

**SIEM 集成**:
- SIEM: {{siem_tool}}
- 集成状态: {{integration_status}}

---

### 漏洞管理

**漏洞扫描**:
- 工具: {{vulnerability_scanner}}
- 频率: {{scan_frequency}}
- 上次扫描: {{last_scan_date}}

**修复 SLA**:
| 严重性 | 响应时间 | 目标 |
|--------|---------|------|
{{#each vulnerability_sla}}
| {{severity}} | {{response}} | {{target}} |
{{/each}}

---

### 事件响应

**响应团队**:
{{#each incident_response_team}}
- **{{role}}**: {{name}} (联系方式: {{contact}})
{{/each}}

**响应时间**:
| 事件级别 | 响应时间 | 升级时间 |
|---------|---------|---------|
{{#each response_times}}
| {{severity}} | {{response}} | {{escalation}} |
{{/each}}

---

### 第三方风险管理

**供应商**:
{{#each third_party_risks}}
| 供应商 | 服务 | 风险评估 | 缓解措施 | 审查状态 |
|--------|------|---------|---------|---------|
| {{vendor}} | {{service}} | {{risk}} | {{mitigation}} | {{review}} |
{{/each}}

---

## 证据收集

### 证据清单

{{#each evidence_checklist}}

#### {{criterion}} 证据

| 证据类型 | 要求 | 位置 | 状态 | 收集人 |
|---------|------|------|------|--------|
{{#each evidences}}
| {{type}} | {{requirement}} | {{location}} | {{status}} | {{collector}} |
{{/each}}

{{/each}}

---

## 差距分析

### 当前差距

{{#each gaps}}
- **{{gap}}**: {{description}}
  - 影响准则: {{affected_criteria}}
  - 优先级: {{priority}}
  - 建议解决方案: {{solution}}
  - 预计工时: {{effort}}
  - 负责人: {{owner}}
{{/each}}

### 整改计划

| 差距 | 优先级 | 行动项 | 负责人 | 截止 | 状态 |
|------|--------|--------|--------|------|------|
{{#each remediation_plan}}
| {{gap}} | {{priority}} | {{action}} | {{owner}} | {{due}} | {{status}} |
{{/each}}

---

## 合规就绪度

### 评估标准

| 评估项 | 标准 | 当前 | 目标 | 差距 |
|--------|------|------|------|------|
{{#each readiness_metrics}}
| {{metric}} | {{standard}} | {{current}} | {{target}} | {{gap}} |
{{/each}}

### 整体评分

**合规评分**: {{compliance_score}} / 100

**评级**:
{{#if score_gt_90}}
- **A**: 优秀 (可以接受审计)
{{/if}}
{{#if score_75_to_90}}
- **B**: 良好 (需要少量改进)
{{/if}}
{{#if score_60_to_75}}
- **C**: 合格 (需要中等改进)
{{/if}}
{{#if score_lt_60}}
- **D**: 不合格 (需要大量改进)
{{/if}}

---

## 下一步行动

### 立即行动

{{#each immediate_actions}}
- [ ] **{{action}}**
  - 优先级: P0
  - 负责人: {{owner}}
  - 截止: {{due_date}}
{{/each}}

### 短期规划

{{#each short_term_actions}}
- [ ] **{{action}}**
  - 优先级: P1
  - 负责人: {{owner}}
  - 截止: {{due_date}}
{{/each}}

---

## 附录

### 术语表

{{#each glossary}}
| 术语 | 定义 |
|------|------|
| {{term}} | {{definition}} |
{{/each}}

### 参考资料

{{#each references}}
- {{title}}: {{url}}
{{/each}}

---

*本检查清单由 Compliance Checker 自动生成*
*合规框架: SOC 2*
