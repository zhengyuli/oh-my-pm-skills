# {{project_name}} - 安全测试计划

**版本**: {{version}}
**日期**: {{date}}
**作者**: {{author}}
**测试周期**: {{test_period}}
**安全级别**: {{security_level}}

---

## 执行摘要

### 测试目标

{{test_objectives}}

### 测试范围

| 测试类型 | 覆盖范围 | 优先级 | 状态 |
|---------|---------|--------|------|
{{#each test_types}}
| {{type}} | {{scope}} | {{priority}} | {{status}} |
{{/each}}

### 关键风险

{{#each key_risks}}
- **{{risk}}**: {{severity}} (影响: {{impact}})
{{/each}}

---

## 1. 测试策略

### 1.1 测试原则

{{#each testing_principles}}
- **{{principle}}**: {{description}}
{{/each}}

### 1.2 测试方法论

**主要方法**: {{primary_methodology}}

**辅助方法**:
{{#each secondary_methodologies}}
- {{method}}
{{/each}}

### 1.3 测试级别

| 级别 | 描述 | 目标 | 范围 |
|------|------|------|------|
{{#each test_levels}}
| {{level}} | {{description}} | {{target}} | {{scope}} |
{{/each}}

---

## 2. 测试类型详情

### 2.1 渗透测试

#### 测试范围

**外部测试**:
{{#each external_penetration_tests}}
- **{{target}}**: {{description}}
  - 测试方法: {{method}}
  - 工具: {{tools}}
  - 预期发现: {{expected_findings}}
{{/each}}

**内部测试**:
{{#each internal_penetration_tests}}
- **{{target}}**: {{description}}
  - 测试方法: {{method}}
  - 工具: {{tools}}
  - 权限级别: {{privilege_level}}
{{/each}}

#### 测试场景

{{#each penetration_scenarios}}

##### {{scenario_name}}

**攻击向量**: {{attack_vector}}

**步骤**:
{{#each steps}}
{{step}}. {{action}}
   - 前置条件: {{precondition}}
   - 执行方式: {{execution}}
   - 预期结果: {{expected_result}}
{{/each}}

**成功标准**:
{{#each success_criteria}}
- {{criterion}}
{{/each}}

{{/each}}

### 2.2 漏洞扫描

#### 静态应用安全测试 (SAST)

**扫描目标**:
{{#each sast_targets}}
- {{target}} (语言: {{language}}, 框架: {{framework}})
{{/each}}

**扫描配置**:
- 工具: {{sast_tool}}
- 扫描规则: {{scan_rules}}
- 误报处理: {{false_positive_handling}}

**检查类别**:
{{#each sast_categories}}
- {{category}} (严重性: {{severity}})
{{/each}}

#### 动态应用安全测试 (DAST)

**扫描目标**:
{{#each dast_targets}}
- {{url}} (环境: {{environment}})
{{/each}}

**扫描配置**:
- 工具: {{dast_tool}}
- 爬虫深度: {{crawl_depth}}
- 认证方式: {{authentication}}

**攻击载荷**:
{{#each attack_payloads}}
- {{payload_type}}: {{examples}}
{{/each}}

#### 依赖扫描

**扫描范围**:
{{#each dependency_scopes}}
- **{{scope}}**: {{manager}}
  - 配置文件: {{config_files}}
  - 许可证策略: {{license_policy}}
{{/each}}

**漏洞数据库**:
{{#each vuln_databases}}
- {{database}} (更新频率: {{update_frequency}})
{{/each}}

### 2.3 安全功能测试

#### 身份认证

**测试场景**:
{{#each auth_test_scenarios}}

##### {{scenario}}

**测试步骤**:
{{#each test_steps}}
1. {{step}}
{{/each}}

**预期结果**:
{{#each expected_results}}
- {{result}}
{{/each}}

**实际结果**: {{actual_result}}
**状态**: {{status}}

{{/each}}

#### 访问控制

**权限矩阵验证**:
| 角色 | 资源 | 预期权限 | 测试方法 | 状态 |
|------|------|---------|---------|------|
{{#each permission_tests}}
| {{role}} | {{resource}} | {{expected_permission}} | {{test_method}} | {{status}} |
{{/each}}

**越权测试**:
{{#each privilege_escalation_tests}}
- **{{test_name}}**
  - 攻击者角色: {{attacker_role}}
  - 目标资源: {{target_resource}}
  - 攻击方法: {{attack_method}}
  - 预期结果: {{expected_result}} (状态: {{status}})
{{/each}}

#### 会话管理

**会话测试**:
{{#each session_tests}}
- **{{test}}**
  - 测试方法: {{method}}
  - 预期行为: {{expected_behavior}}
  - 实际结果: {{actual_result}}
{{/each}}

#### 输入验证

**输入验证测试**:
{{#each input_validation_tests}}

##### {{field_name}}

| 测试用例 | 输入 | 预期结果 | 实际结果 | 状态 |
|---------|------|---------|---------|------|
{{#each test_cases}}
| {{case}} | {{input}} | {{expected}} | {{actual}} | {{status}} |
{{/each}}

{{/each}}

### 2.4 网络安全测试

#### 网络扫描

**端口扫描**:
| 目标 | 端口 | 服务 | 版本 | 状态 |
|------|------|------|------|------|
{{#each port_scan_results}}
| {{target}} | {{port}} | {{service}} | {{version}} | {{status}} |
{{/each}}

**服务枚举**:
{{#each service_enumeration}}
- **{{service}}**
  - 版本: {{version}}
  - 配置: {{configuration}}
  - 漏洞: {{vulnerabilities}}
{{/each}}

#### 加密验证

**传输加密**:
{{#each tls_tests}}
- **{{endpoint}}**
  - TLS 版本: {{tls_version}}
  - 密码套件: {{cipher_suites}}
  - 证书有效性: {{certificate_valid}}
  - 弱点: {{weaknesses}}
{{/each}}

**数据加密**:
{{#each encryption_tests}}
- **{{data_type}}**
  - 存储位置: {{location}}
  - 加密算法: {{algorithm}}
  - 密钥长度: {{key_length}}
  - 验证方法: {{verification_method}}
  - 结果: {{result}}
{{/each}}

### 2.5 API 安全测试

#### 端点测试

{{#each api_endpoint_tests}}

##### {{endpoint}}

**方法**: `{{method}}`
**认证要求**: {{auth_required}}

**测试场景**:
| 场景 | 请求 | 预期响应 | 实际响应 | 状态 |
|------|------|---------|---------|------|
{{#each scenarios}}
| {{scenario}} | {{request}} | {{expected_response}} | {{actual_response}} | {{status}} |
{{/each}}

{{/each}}

#### 注入测试

**SQL 注入**:
{{#each sql_injection_tests}}
- **{{endpoint}}** (参数: {{parameter}})
  - Payload: {{payload}}
  - 预期结果: {{expected_result}}
  - 实际结果: {{actual_result}}
  - 状态: {{status}}
{{/each}}

**XSS 测试**:
{{#each xss_tests}}
- **{{endpoint}}** (参数: {{parameter}})
  - Payload: {{payload}}
  - 预期结果: {{expected_result}}
  - 实际结果: {{actual_result}}
  - 状态: {{status}}
{{/each}}

**其他注入**:
{{#each other_injection_tests}}
- **{{injection_type}}**
  - 目标: {{target}}
  - Payload: {{payload}}
  - 状态: {{status}}
{{/each}}

---

## 3. 测试环境

### 3.1 环境配置

| 环境 | 用途 | URL | 数据 | 状态 |
|------|------|-----|------|------|
{{#each environments}}
| {{name}} | {{purpose}} | {{url}} | {{data}} | {{status}} |
{{/each}}

### 3.2 测试数据

**数据类型**:
{{#each test_data_types}}
- **{{type}}**: {{description}}
  - 来源: {{source}}
  - 脱敏方法: {{anonymization}}
  - 数量: {{quantity}}
{{/each}}

**敏感数据处理**:
- 处理方法: {{sensitive_data_method}}
- 合规性: {{compliance}}

### 3.3 测试工具

**自动化工具**:
{{#each automated_tools}}
- **{{name}}**
  - 版本: {{version}}
  - 用途: {{purpose}}
  - 配置: {{configuration}}
{{/each}}

**手动工具**:
{{#each manual_tools}}
- **{{name}}**: {{purpose}}
{{/each}}

---

## 4. 测试执行计划

### 4.1 时间表

| 阶段 | 任务 | 开始日期 | 结束日期 | 负责人 | 状态 |
|------|------|---------|---------|--------|------|
{{#each schedule}}
| {{phase}} | {{task}} | {{start_date}} | {{end_date}} | {{owner}} | {{status}} |
{{/each}}

### 4.2 资源分配

**团队成员**:
{{#each team_members}}
- **{{name}}** ({{role}})
  - 负责测试: {{responsible_for}}
  - 时间分配: {{time_allocation}}
{{/each}}

**预算**:
{{#each budget_items}}
- **{{item}}**: ${{cost}}
{{/each}}

**总预算**: ${{total_budget}}

---

## 5. 缺陷管理

### 5.1 严重性级别

| 级别 | 定义 | 响应时间 | 修复时限 |
|------|------|---------|---------|
{{#each severity_levels}}
| {{level}} | {{definition}} | {{response_time}} | {{fix_deadline}} |
{{/each}}

### 5.2 缺陷跟踪

**缺陷报告**:
{{#each defects}}

##### {{defect_id}}: {{title}}

**严重性**: {{severity}}
**优先级**: {{priority}}
**状态**: {{status}}
**发现者**: {{discoverer}}
**日期**: {{discovery_date}}

**描述**:
{{description}}

**重现步骤**:
{{#each reproduction_steps}}
{{step}}. {{action}}
{{/each}}

**环境影响**:
{{#each affected_environments}}
- {{environment}}
{{/each}}

**修复建议**:
{{fix_suggestion}}

**责任人**: {{owner}}
**预计修复**: {{estimated_fix}}

{{/each}}

### 5.3 修复验证

**验证流程**:
{{#each verification_process}}
{{step}}. {{description}}
{{/each}}

---

## 6. 报告和沟通

### 6.1 报告类型

**每日报告**:
- 格式: {{daily_report_format}}
- 接收人: {{daily_report_recipients}}
- 内容: {{daily_report_content}}

**每周报告**:
- 格式: {{weekly_report_format}}
- 接收人: {{weekly_report_recipients}}
- 会议: {{weekly_meeting}}

**最终报告**:
- 模板: {{final_report_template}}
- 包含内容:
{{#each final_report_sections}}
- {{section}}
{{/each}}

### 6.2 指标和 KPI

| 指标 | 目标 | 当前 | 状态 |
|------|------|------|------|
{{#each metrics}}
| {{metric}} | {{target}} | {{current}} | {{status}} |
{{/each}}

### 6.3 利益相关者

**管理层**:
{{#each management_stakeholders}}
- **{{name}}** ({{role}})
  - 关注点: {{concerns}}
  - 汇报频率: {{report_frequency}}
{{/each}}

**技术团队**:
{{#each technical_stakeholders}}
- **{{name}}** ({{role}})
  - 关注点: {{concerns}}
  - 协作方式: {{collaboration}}
{{/each}}

---

## 7. 准入和准出标准

### 7.1 准入标准

测试开始前必须满足:
{{#each entry_criteria}}
- [ ] {{criterion}}
{{/each}}

### 7.2 准出标准

测试完成必须满足:
{{#each exit_criteria}}
- [ ] {{criterion}}
{{/each}}

### 7.3 暂停标准

以下情况测试暂停:
{{#each suspension_criteria}}
- {{criterion}} (行动: {{action}})
{{/each}}

---

## 8. 风险和缓解措施

### 8.1 测试风险

| 风险 | 可能性 | 影响 | 缓解措施 | 应急计划 |
|------|--------|------|---------|---------|
{{#each test_risks}}
| {{risk}} | {{probability}} | {{impact}} | {{mitigation}} | {{contingency}} |
{{/each}}

### 8.2 生产风险

**生产测试注意事项**:
{{#each production_test_precautions}}
- **{{precaution}}**: {{description}}
{{/each}}

---

## 9. 合规和审计

### 9.1 合规要求

**适用标准**:
{{#each compliance_standards}}
- **{{standard}}**: {{version}}
  - 要求: {{requirements}}
  - 验证方法: {{verification_method}}
{{/each}}

### 9.2 审计追踪

**测试日志**:
- 存储位置: {{log_location}}
- 保留期: {{retention_period}}
- 访问控制: {{access_control}}

**证据收集**:
{{#each evidence_collection}}
- **{{evidence_type}}**: {{location}} (保留: {{retention}})
{{/each}}

---

## 10. 持续改进

### 10.1 经验教训

**本次测试亮点**:
{{#each lessons_learned_positive}}
- {{highlight}}
{{/each}}

**需要改进**:
{{#each lessons_learned_improvement}}
- {{improvement}}
{{/each}}

### 10.2 行动项

**后续行动**:
{{#each follow_up_actions}}
- [ ] **{{action}}** (优先级: {{priority}}, 负责人: {{owner}}, 截止: {{due_date}})
{{/each}}

---

## 附录

### A. 测试用例清单

{{#each all_test_cases}}
- [{{test_id}}] {{test_name}} (状态: {{status}}, 严重性: {{severity}})
{{/each}}

### B. 工具配置文件

**SAST 配置**:
```
{{sast_configuration}}
```

**DAST 配置**:
```
{{dast_configuration}}
```

### C. 术语表

| 术语 | 定义 |
|------|------|
{{#each glossary}}
| {{term}} | {{definition}} |
{{/each}}

### D. 参考资料

{{#each references}}
- {{title}}: {{url}}
{{/each}}

---

*本测试计划由 Security Test Plan Generator 自动生成*
*安全级别: {{security_level}}*
*测试框架: {{testing_framework}}*
