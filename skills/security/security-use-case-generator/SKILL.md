---
name: security-use-case-generator
description: 安全用例生成器 - OWASP Top 10测试用例、安全验证场景、渗透测试场景生成
version: 1.0.0
author: oh-my-pm-skills
tags: [security, testing, owasp, test-cases, security-scenarios]
allowed-tools: Read, Write, Edit
model: inherit
---

# Security Use Case Generator

安全用例生成器负责基于 OWASP Top 10 和其他安全标准生成安全测试用例和验证场景。

## When to Use This Skill

用户请求以下功能时激活此技能：
- "生成安全测试用例"
- "OWASP 测试"
- "安全验证场景"
- "渗透测试用例"
- "security test cases"

## Core Process

### 步骤 1: 分析应用架构

```yaml
应用信息收集:
  应用类型:
    - Web 应用
    - 移动应用
    - API 服务
    - 微服务
    - 桌面应用

  技术栈:
    - 前端框架
    - 后端框架
    - 数据库
    - 认证机制
    - 第三方依赖

  攻击面:
    - 用户输入点
    - API 端点
    - 文件上传
    - 数据查询
    - 第三方集成

  数据类型:
    - 用户认证信息
    - 个人数据
    - 支付信息
    - 敏感业务数据
```

### 步骤 2: 选择测试框架

```yaml
OWASP Top 10 (2021):
  A01: 访问控制失效
  A02: 加密失败
  A03: 注入
  A04: 不安全设计
  A05: 错误的安全配置
  A06: 易受攻击和过时的组件
  A07: 身份识别和身份验证失败
  A08: 软件和数据完整性失败
  A09: 安全日志和监控失败
  A10: 服务器端请求伪造 (SSRF)

OWASP API Security Top 10:
  API1: 对象级授权失效
  API2: 用户身份验证失效
  API3: 属性级授权失效
  API4: 资源消耗无限制
  API5: 分页和限制失效
  API6: 批量分配
  API7: 安全配置错误
  API8: 注入
  API9: 资产管理不当
  API10: 日志和监控不足

移动应用安全:
  - 不安全数据存储
  - 不安全通信
  - 不安全认证
  - 代码质量
  - 逆向工程
  - 加密算法
```

### 步骤 3: 生成测试用例

### OWASP A01: 访问控制失效

```yaml
测试用例:

  TC-A01-001: 垂直权限提升
    描述: 普通用户访问管理员功能
    步骤:
      1. 以普通用户身份登录
      2. 尝试访问 /admin 端点
      3. 尝试访问管理员 API
      4. 尝试执行管理员操作
    预期: 返回 403 Forbidden
    实际: {{actual_result}}
    状态: {{status}}

  TC-A01-002: 水平权限提升
    描述: 用户 A 访问用户 B 的数据
    步骤:
      1. 以用户 A 身份登录
      2. 获取用户 A 的 ID
      3. 修改请求，将 ID 替换为用户 B 的 ID
      4. 查看是否能访问用户 B 的数据
    预期: 返回 403 Forbidden
    实际: {{actual_result}}
    状态: {{status}}

  TC-A01-003: IDOR 测试
    描述: 直接对象引用测试
    步骤:
      1. 查看用户个人资料页面
      2. 记录 URL 中的 ID 参数
      3. 修改 ID 为其他用户的 ID
      4. 检查是否显示其他用户信息
    预期: 不显示其他用户信息
    实际: {{actual_result}}
    状态: {{status}}

  TC-A01-004: API 权限绕过
    描述: 通过 API 绕过 UI 权限检查
    步骤:
      1. 识别禁用的功能按钮
      2. 捕获该功能的 API 调用
      3. 直接调用 API
      4. 检查是否执行
    预期: API 返回 403
    实际: {{actual_result}}
    状态: {{status}}
```

### OWASP A02: 加密失败

```yaml
测试用例:

  TC-A02-001: TLS 版本检查
    描述: 验证是否使用强 TLS 版本
    步骤:
      1. 使用 nmap 或 openssl 检查 TLS 版本
      2. 检查是否支持 TLS 1.2+
      3. 检查是否禁用 SSL/TLS 1.0/1.1
    预期: 仅支持 TLS 1.2+
    工具: nmap, sslscan, testssl.sh

  TC-A02-002: 弱加密算法检查
    描述: 检查是否使用弱加密算法
    步骤:
      1. 检查密码套件
      2. 识别 RC4, DES, 3DES 等弱算法
      3. 检查密钥长度
    预期: 不使用弱算法
    工具: sslscan, cipherscan

  TC-A02-003: 敏感数据存储加密
    描述: 验证敏感数据是否加密存储
    步骤:
      1. 访问数据库
      2. 检查密码字段
      3. 检查是否使用哈希+盐
      4. 检查 PII 数据加密
    预期: 敏感数据加密存储
    工具: 数据库查询

  TC-A02-004: 证书验证
    描述: 验证 SSL 证书有效性
    步骤:
      1. 检查证书是否过期
      2. 检查证书链
      3. 检查主机名匹配
    预期: 证书有效
    工具: openssl, curl
```

### OWASP A03: 注入

```yaml
测试用例:

  TC-A03-001: SQL 注入测试
    描述: 测试 SQL 注入漏洞
    步骤:
      1. 识别输入点 (表单, API, URL)
      2. 输入测试载荷:
         - ' OR '1'='1
         - " OR "1"="1
         - ' UNION SELECT NULL--
         - '; DROP TABLE users--
      3. 观察响应
    预期: 输入被正确转义
    工具: sqlmap, Burp Suite

  TC-A03-002: XSS 测试 (反射型)
    描述: 测试反射型 XSS
    步骤:
      1. 识别反射输入点
      2. 输入测试载荷:
         - <script>alert('XSS')</script>
         - <img src=x onerror=alert('XSS')>
         - <svg onload=alert('XSS')>
      3. 检查响应中是否执行
    预期: 脚本不执行
    工具: Burp Suite, XSStrike

  TC-A03-003: XSS 测试 (存储型)
    描述: 测试存储型 XSS
    步骤:
      1. 提交包含 XSS 的数据
      2. 访问显示该数据的页面
      3. 检查脚本是否执行
    预期: 脚本被过滤/转义
    工具: Burp Suite

  TC-A03-004: 命令注入测试
    描述: 测试操作系统命令注入
    步骤:
      1. 识别系统命令执行点
      2. 输入测试载荷:
         - ; ls -la
         - | cat /etc/passwd
         - `whoami`
         - $(id)
      3. 检查命令是否执行
    预期: 命令不执行
    工具: 手动测试

  TC-A03-005: LDAP 注入测试
    描述: 测试 LDAP 注入
    步骤:
      1. 识别认证功能
      2. 输入测试载荷:
         - *)(uid=*))(|(uid=*
         - *)(objectClass=*)
      3. 检查是否能绕过认证
    预期: 正常认证流程
    工具: 手动测试
```

### OWASP A07: 身份识别和身份验证失败

```yaml
测试用例:

  TC-A07-001: 弱密码检查
    描述: 测试是否允许弱密码
    步骤:
      1. 尝试注册弱密码
      2. 输入: "123456", "password", "qwerty"
      3. 检查是否被接受
    预期: 拒绝弱密码

  TC-A07-002: 暴力破解保护
    描述: 测试暴力破解保护
    步骤:
      1. 多次尝试错误密码
      2. 检查是否被锁定
      3. 检查是否有延迟
    预期: 有速率限制/锁定机制

  TC-A07-003: 会话管理
    描述: 测试会话安全性
    步骤:
      1. 登录获取会话 Token
      2. 检查 Token 随机性
      3. 登出后检查 Token 是否失效
      4. 检查超时机制
    预期: Token 安全，超时合理

  TC-A07-004: 密码重置流程
    描述: 测试密码重置安全性
    步骤:
      1. 请求密码重置
      2. 检查 Token 安全性
      3. 检查是否有信息泄露
      4. 尝试重用 Token
    预期: 安全的密码重置流程
```

### OWASP API Security API1: 对象级授权失效

```yaml
测试用例:

  TC-API1-001: API 垂直权限提升
    描述: 测试 API 垂直权限
    步骤:
      1. 以普通用户身份登录
      2. 调用管理员 API 端点
      3. 检查是否成功
    预期: 返回 403

  TC-API1-002: API 水平权限提升
    描述: 测试 API 水平权限
    步骤:
      1. 以用户 A 身份调用 API
      2. 修改 ID 为用户 B 的 ID
      3. 检查是否能访问用户 B 数据
    预期: 返回 403

  TC-API1-003: 批量操作权限
    描述: 测试批量操作的权限检查
    步骤:
      1. 准备批量获取请求
      2. 混合自己和他人的 ID
      3. 调用批量 API
      4. 检查返回数据
    预期: 只返回有权限的数据
```

### 步骤 4: 生成测试场景

```yaml
场景化测试:

场景 1: 攻击者链
  攻击序列:
    1. 信息收集
    2. 利用弱认证
    3. 权限提升
    4. 数据窃取
  测试目标:
    - 验证纵深防御
    - 检测异常行为
    - 响应及时性

场景 2: 内部威胁
  攻击序列:
    1. 滥用合法权限
    2. 数据导出
    3. 覆盖日志
  测试目标:
    - 最小权限原则
    - 审计日志
    - 异常检测

场景 3: 供应链攻击
  攻击序列:
    1. 利用第三方组件漏洞
    2. 获取系统访问
    3. 横向移动
  测试目标:
    - 组件版本检查
    - 网络隔离
    - 入侵检测
```

### 步骤 5: 调用引擎生成测试计划

```yaml
工作流:
  1. qa_engine:
      action: "identify_attack_surface"
      识别攻击面

  2. scoring_engine:
      action: "risk_scoring"
      评估测试用例风险

  3. template_engine:
      action: "render"
      template: "security-usecase-owasp"
      生成测试计划

  4. document_engine:
      action: "create"
      type: "security_test_plan"
      输出测试计划
```

## 安全测试用例模板

```markdown
# {{project_name}} - 安全测试用例

**版本**: {{version}}
**日期**: {{date}}
**测试框架**: {{framework}}
**范围**: {{scope}}

---

## 测试概览

### 测试目标

{{#each objectives}}
- {{.}}
{{/each}}

### 测试范围

**应用**: {{application_name}}
**URL**: {{base_url}}
**环境**: {{environment}} (开发/测试/预发布)

### 测试类型

{{#each test_types}}
- {{name}}: {{description}}
{{/each}}

---

## OWASP Top 10 测试用例

### A01: 访问控制失效

{{#each a01_tests}}
#### {{test_id}}: {{title}}

**描述**: {{description}}

**严重性**: {{severity}} (高/中/低)

**测试步骤**:
{{#each steps}}
{{index}}. {{step}}
{{/each}}

**预期结果**: {{expected}}

**实际结果**: {{actual}}

**状态**: {{status}} (通过/失败/跳过)

**证据**: {{evidence}}

**修复建议**: {{remediation}}

---

{{/each}}

### A02: 加密失败

[格式同 A01]

### A03: 注入

[格式同 A01]

### A04: 不安全设计

[格式同 A01]

### A05: 错误的安全配置

[格式同 A01]

### A06: 易受攻击和过时的组件

[格式同 A01]

### A07: 身份识别和身份验证失败

[格式同 A01]

### A08: 软件和数据完整性失败

[格式同 A01]

### A09: 安全日志和监控失败

[格式同 A01]

### A10: 服务器端请求伪造 (SSRF)

[格式同 A01]

---

## API 安全测试用例

{{#each api_tests}}
### {{category}}

#### {{test_id}}: {{title}}

**API 端点**: {{endpoint}}
**方法**: {{method}}

**描述**: {{description}}

**测试步骤**:
{{#each steps}}
{{index}}. {{step}}
{{/each}}

**请求示例**:
```http
{{method}} {{endpoint}} HTTP/1.1
Host: {{host}}
{{#each headers}}
{{name}}: {{value}}
{{/each}}

{{#if body}}
{{body}}
{{/if}}
```

**预期响应**:
```http
HTTP/1.1 {{status_code}}
{{response_body}}
```

**实际响应**:
```http
{{actual_response}}
```

**状态**: {{status}}

---

{{/each}}

---

## 业务逻辑测试

### 测试场景

{{#each business_logic_tests}}

#### {{scenario_name}}

**描述**: {{description}}

**威胁**: {{threat}}

**测试步骤**:
{{#each steps}}
{{index}}. {{step}}
{{/each}}

**预期**: {{expected}}

**实际**: {{actual}}

**状态**: {{status}}

**业务影响**: {{business_impact}}

{{/each}}

---

## 测试工具

### 工具清单

{{#each tools}}
- **{{name}}**: {{purpose}}
  - 版本: {{version}}
  - 用途: {{usage}}
{{/each}}

### 工具配置

{{#each tool_configs}}
#### {{tool_name}}

```yaml
{{config}}
```

{{/each}}

---

## 测试执行计划

### 测试环境

- **环境**: {{environment}}
- **URL**: {{url}}
- **认证**: {{authentication}}
- **测试数据**: {{test_data}}

### 时间表

| 阶段 | 任务 | 负责人 | 截止 |
|------|------|--------|------|
{{#each schedule}}
| {{phase}} | {{task}} | {{owner}} | {{due_date}} |
{{/each}}

### 测试顺序

1. 信息收集 ({{duration}})
2. 自动化扫描 ({{duration}})
3. 手动测试 ({{duration}})
4. 业务逻辑测试 ({{duration}})
5. 报告生成 ({{duration}})

---

## 结果汇总

### 发现汇总

| 严重性 | 数量 | 百分比 |
|--------|------|--------|
| 严重 | {{critical}} | {{critical_percent}}% |
| 高 | {{high}} | {{high_percent}}% |
| 中 | {{medium}} | {{medium_percent}}% |
| 低 | {{low}} | {{low_percent}}% |
| 信息 | {{info}} | {{info_percent}}% |

### 按类别统计

| 类别 | 严重 | 高 | 中 | 低 | 总计 |
|------|------|-----|-----|-----|------|
{{#each by_category}}
| {{name}} | {{critical}} | {{high}} | {{medium}} | {{low}} | {{total}} |
{{/each}}

---

## 优先级修复建议

### 立即修复 (严重/高)

{{#each immediate_fixes}}
1. **{{title}}** ({{test_id}})
   - 类别: {{category}}
   - 风险: {{risk}}
   - 修复: {{remediation}}
   - 负责人: {{owner}}
   - 预估: {{estimate}}

{{/each}}

### 近期修复 (中)

[格式同上]

### 长期改进 (低/信息)

[格式同上]

---

## 附录

### 测试数据

{{#each test_data}}
- {{name}}: {{description}}
  - 格式: {{format}}
  - 位置: {{location}}
{{/each}}

### 截图和证据

{{#each evidence}}
- {{title}}: ![]({{path}})
  - 描述: {{description}}
{{/each}}

### 词汇表

{{#each glossary}}
- **{{term}}**: {{definition}}
{{/each}}

---

*本测试计划由 Security Use Case Generator 自动生成*
*测试框架: {{framework}}*
```

## 交互示例

### 示例 1: OWASP 测试套件

```
用户: 为我的电商网站生成 OWASP Top 10 测试用例

Security Use Case Generator:
  1. 分析应用架构
  2. 识别攻击面
  3. 为每个 OWASP 类别生成测试用例
  4. 包含测试步骤和预期结果
  5. 提供修复建议
```

### 示例 2: API 安全测试

```
用户: 生成 REST API 的安全测试用例

Security Use Case Generator:
  1. 分析 API 端点
  2. 应用 OWASP API Security Top 10
  3. 生成请求/响应示例
  4. 包含权限绕过测试
```

### 示例 3: 特定漏洞测试

```
用户: 专注于 SQL 注入和 XSS 的深度测试

Security Use Case Generator:
  1. 识别所有输入点
  2. 生成全面的注入载荷
  3. 包含盲注测试
  4. 提供自动化工具配置
```

## 集成点

**使用的引擎**:
- **qa-engine**: 攻击面识别
- **scoring-engine**: 风险评分
- **template-engine**: 测试计划渲染
- **document-engine**: 测试计划生成

**与其他技能协作**:
- **threat-modeling**: 基于威胁的测试用例
- **compliance-checker**: 合规要求的测试
- **impact-analyzer**: 漏洞影响评估

## 最佳实践

核心原则（详见 `shared/common-sections.yaml#best_practices.security_testing`）：

✅ **DO**:
- 从信息收集开始
- 结合自动化和手动测试
- 测试业务逻辑
- 验证修复效果
- 保持测试环境隔离

❌ **DON'T**:
- 只依赖自动化工具
- 忽视业务逻辑
- 在生产环境测试
- 跳过授权测试

## 输出格式

```yaml
result:
  success: true
  test_plan:
    framework: "{{framework}}"
    total_tests: {{count}}
    scope: {{scope}}

  test_categories:
    - name: "{{category}}"
      tests: {{count}}

  estimated_time: {{hours}} hours
  tools_required: {{tools}}

  output_path: "security/{{project_name}}-test-plan.md"
```

## 测试场景

```bash
# OWASP 完整测试
security-usecase-generator generate \
  --framework owasp \
  --target "https://api.example.com"

# API 安全测试
security-usecase-generator generate \
  --framework "owasp-api" \
  --openapi spec.json

# 特定漏洞测试
security-usecase-generator generate \
  --vulnerabilities "sql,xss,ssrf" \
  --depth "deep"
```
