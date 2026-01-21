---
name: template-engine
description: 模板渲染引擎 - Handlebars/Mustache语法、变量插值、条件渲染、循环渲染、多格式输出
version: 1.0.0
author: oh-my-pm-skills
tags: [engine, template, rendering, validation, handlebars, markdown, report-generation]
allowed-tools: Read, Write, Edit
model: inherit
---

# Template Engine

模板引擎负责处理所有模板相关的操作，为其他技能提供统一的模板渲染能力。

## When to Use This Engine

其他技能需要以下功能时调用此引擎：
- 变量插值和替换
- 条件渲染
- 模板继承和组合
- 模板验证
- 循环渲染列表

## Core Process

### 步骤 1: 加载模板

```yaml
输入:
  template_path: .claude/templates/prd-standard.md
  template_ref: prd-security  # 可选：从模板库引用

输出:
  template_content: string
  template_metadata: object
```

### 步骤 2: 验证模板

检查：
- 语法正确性（YAML/Frontmatter）
- 必需变量是否定义
- 引用的子模板是否存在
- 循环继承检测

```yaml
验证规则:
  - 必需变量: {{project_name}}, {{date}}, {{author}}
  - 可选变量: {{version}}, {{status}}, {{tags}}
  - 模板语法: 遵循 Mustache/Handlebars 风格
  - 继承深度: 最大 5 层
```

### 步骤 3: 收集变量

根据模板类型收集必需的变量：

#### 通用变量（所有模板）

```yaml
{{project_name}}     # 项目名称
{{version}}          # 版本号（默认 1.0.0）
{{date}}             # 当前日期（ISO 8601）
{{author}}           # 作者
{{status}}           # 状态（draft/review/approved）
{{tags}}             # 标签数组
```

#### PRD 特定变量

```yaml
{{problem_statement}}     # 问题陈述
{{target_users}}          # 目标用户
{{success_metrics}}       # 成功指标
{{technical_requirements}} # 技术需求
{{user_stories}}          # 用户故事数组
{{features}}              # 功能列表
```

#### 安全特定变量

```yaml
{{threat_model}}          # 威胁模型（STRIDE）
{{compliance_framework}}  # 合规框架（SOC2/ISO27001）
{{security_requirements}} # 安全需求
{{risk_assessment}}       # 风险评估（DREAD）
{{owasp_controls}}        # OWASP 控制措施
```

### 步骤 4: 渲染模板

#### 变量插值

```markdown
# {{project_name}} PRD

**版本**: {{version}}
**日期**: {{date}}
**作者**: {{author}}

## 问题陈述

{{problem_statement}}
```

#### 条件渲染

```markdown
{{#if security_requirements}}
## 安全与隐私

{{security_requirements}}
{{/if}}

{{#if compliance_framework}}
## 合规与审计

本产品需符合 {{compliance_framework}} 框架要求。
{{/if}}
```

#### 循环渲染

```markdown
## 目标用户

{{#each target_users}}
- {{name}}: {{description}}
{{/each}}

## 用户故事

{{#each user_stories}}
### {{title}}

**作为** {{role}}
**我想要** {{want}}
**以便** {{benefit}}

**接受标准**:
{{#each acceptance_criteria}}
- {{.}}
{{/each}}
{{/each}}
```

#### 模板继承

**基础模板** (`prd-base.md`):
```markdown
# {{project_name}} PRD

{{> section-problem}}
{{> section-goals}}
{{> section-audience}}
{{> section-security}}  <!-- 条件包含 -->
```

**子模板** (`section-security.md`):
```markdown
## 安全与隐私

{{threat_model}}

{{risk_assessment}}
```

### 步骤 5: 验证输出

渲染后的验证：
- 所有变量已替换（无残留 `{{}}`）
- Markdown 结构完整
- 必需章节都存在
- 列表格式正确

## 支持的模板类型

### PRD 模板

| 模板 ID | 描述 | 章节 | 变量 |
|---------|------|------|------|
| `prd-standard` | 标准 15 节 PRD | 15 | 通用 + PRD |
| `prd-security` | 安全增强 17 节 PRD | 17 | 通用 + PRD + 安全 |
| `prd-lean` | 精简 MVP PRD | 8 | 通用 + PRD (核心) |

### 安全模板

| 模板 ID | 描述 | 框架 |
|---------|------|------|
| `threat-stride` | STRIDE 威胁建模 | STRIDE |
| `threat-dread` | DREAD 风险评估 | DREAD |
| `compliance-soc2` | SOC 2 检查清单 | SOC 2 |
| `compliance-iso27001` | ISO 27001 检查清单 | ISO 27001 |
| `security-usecase-owasp` | OWASP Top 10 用例 | OWASP |

### 工作流模板

| 模板 ID | 描述 | 涉及技能 |
|---------|------|---------|
| `workflow-security-prd` | 完整安全产品 PRD 流程 | 5 个技能 |
| `workflow-quick-prd` | 快速 PRD 生成 | 2 个技能 |
| `workflow-incident-response` | 安全事件响应 | 3 个技能 |
| `workflow-compliance-audit` | 合规审计准备 | 2 个技能 |

## Template API

### 调用格式

```yaml
template_engine:
  action: "render"
  template: "prd-security"
  variables:
    project_name: "[产品名称]"
    version: "1.0.0"
    date: "[日期]"
    author: "[作者]"
    status: "draft"
    problem_statement: "..."
    threat_model: "..."
    # ... 其他变量
  options:
    validate: true
    strict_mode: true
    remove_empty_sections: true
```

### 返回格式

```yaml
result:
  success: true
  content: "# [产品名称] PRD\n\n..."
  metadata:
    template_used: "prd-security"
    rendered_at: "[渲染时间]"
    variables_count: 15
    sections_count: 17
  warnings: []
  errors: []
```

## 错误处理

### 模板加载失败

```markdown
错误: template_not_found
信息: 模板 'prd-xyz' 不存在
解决: 检查模板 ID 是否正确，或使用可用模板列表
```

### 变量缺失

```markdown
错误: missing_required_variable
信息: 缺少必需变量 'project_name'
解决: 提供该变量值或使用默认值
```

### 循环继承

```markdown
错误: circular_inheritance
信息: 模板 A → B → C → A 形成循环
解决: 检查模板继承关系，打破循环
```

### 语法错误

```markdown
错误: template_syntax_error
信息: 第 15 行：未闭合的 {{#if}}
解决: 检查条件渲染语法
```

## 最佳实践

✅ **DO**:
- 使用有意义的变量名
- 为可选变量提供默认值
- 保持模板简洁（单个模板 < 500 行）
- 复用通用片段通过 `{{> partial}}`
- 验证所有输入变量

❌ **DON'T**:
- 嵌套超过 3 层的条件渲染
- 在模板中包含业务逻辑
- 使用过深的继承（> 5 层）
- 硬编码特定值（应使用变量）
- 跳过模板验证步骤

## 模板缓存策略

```yaml
cache:
  enabled: true
  ttl: 3600  # 缓存 1 小时
  invalidate_on:
    - template_change
    - variable_schema_change
```

## 性能优化

- 模板预编译（启动时）
- 变量预验证（渲染前）
- 增量渲染（大模板分段）
- 输出缓存（相同参数）

## 集成点

此引擎被以下技能使用：
- **prd-generator**: 渲染 PRD 文档
- **threat-modeling**: 渲染威胁模型报告
- **compliance-checker**: 渲染合规清单
- **security-use-case-generator**: 渲染测试用例
- **orchestrator**: 渲染工作流模板

## 测试模板

```bash
# 测试模板渲染
echo '{
  "template": "prd-lean",
  "variables": {
    "project_name": "测试项目"
  }
}' | template-engine render

# 验证模板语法
template-engine validate .claude/templates/prd-security.md

# 列出可用模板
template-engine list
```
