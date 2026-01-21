---
name: document-engine
description: 文档处理引擎 - 结构化输出、目录生成、格式化、交叉引用、版本控制、多格式导出
version: 1.0.0
author: oh-my-pm-skills
tags: [engine, document, markdown, formatting, toc, cross-reference, versioning]
allowed-tools: Read, Write, Edit
model: inherit
---

# Document Engine

文档引擎负责处理所有文档相关的操作，包括结构化输出、格式化、版本控制和导出。

## When to Use This Engine

其他技能需要以下功能时调用此引擎：
- 生成结构化 Markdown 文档
- 格式化和美化现有文档
- 生成目录和交叉引用
- 文档版本控制集成
- 导出不同格式

## Core Process

### 步骤 1: 定义文档结构

```yaml
文档类型支持:
  prd: 产品需求文档
  threat_model: 威胁建模报告
  compliance_report: 合规检查报告
  user_stories: 用户故事集合
  design_doc: 技术设计文档
  api_spec: API 规范
  test_plan: 测试计划
  release_notes: 发布说明

标准结构:
  metadata:
    文档标题、版本、日期、作者、状态

  front_matter:
    文档元数据 (YAML)

  table_of_contents:
    自动生成目录

  sections:
    结构化章节内容

  back_matter:
    附录、参考资料
```

### 步骤 2: 内容格式化

#### Markdown 增强

```markdown
# 支持 GFM (GitHub Flavored Markdown)

## 表格

| 功能 | 优先级 | 复杂度 | 状态 |
|------|--------|--------|------|
| 用户认证 | P0 | 高 | 进行中 |

## 任务列表

### Sprint 1
- [x] 设计数据库
- [x] 实现 API
- [ ] 编写测试
- [ ] 文档更新

## 代码块

```python
def calculate_rice(reach, impact, confidence, effort):
    return (reach * impact * confidence) / effort
```

## 提示框

> **提示**: 这是一个提示信息

> **警告**: 需要注意的事项

> **错误**: 必须避免的错误
```

#### 结构化组件

```yaml
列表:
  无序列表:
    - 项目 1
    - 项目 2
      - 子项目 2.1

  有序列表:
    1. 第一步
    2. 第二步

  定义列表:
    **术语**: 定义

代码块:
  支持语言:
    - python, javascript, java, go, rust
    - yaml, json, xml
    - bash, shell
    - sql

表格:
  对齐:
    - 左对齐（默认）
    - 右对齐: -->
    - 居中: :--:

链接:
  内部: [文档标题](#章节锚点)
  外部: [链接文本](https://example.com)
  参考: [参考编号]
```

### 步骤 3: 生成目录

```markdown
## 目录

- [1. 问题陈述](#1-问题陈述)
  - [1.1 当前问题](#11-当前问题)
  - [1.2 影响范围](#12-影响范围)
- [2. 目标用户](#2-目标用户)
- [3. 解决方案](#3-解决方案)
  - [3.1 核心功能](#31-核心功能)
  - [3.2 技术架构](#32-技术架构)

---

自动生成规则:
  - 使用 # ## ### ### 作为级别
  - 自动生成锚点
  - 支持嵌套列表（最多 4 级）
  - 可配置目录深度
```

### 步骤 4: 版本控制集成

```yaml
Git 集成:
  自动提交:
    - 生成文档后自动 commit
    - 使用 Conventional Commits 格式
    - 提交信息包含文档类型和标题

  版本标签:
    - 文档版本号
    - 语义化版本 (SemVer)
    - 变更日志 (CHANGELOG.md)

  变更追踪:
    - 在文档中记录版本历史
    - 标注变更日期和原因
    - 变更对比

提交格式:
  docs(prd): add initial PRD for [产品名称]

  或

  docs(threat): update threat model with new mitigation strategies
```

### 步骤 5: 导出功能

```yaml
支持格式:
  markdown: 标准 Markdown (.md)
  html: 静态 HTML (.html)
  pdf: 可打印 PDF (.pdf)
  docx: Word 文档 (.docx)

导出选项:
  include_toc: true
  include_metadata: true
  syntax_highlight: true
  page_breaks: true  # PDF only
  template: "standard" | "professional" | "minimal"
```

## Document API

### 创建文档

```yaml
document_engine:
  action: "create"
  type: "prd"
  content: |
    # {{project_name}} PRD
    ...

  options:
    output_path: "docs/prd/[产品名称]-prd.md"
    generate_toc: true
    format: true
    auto_commit: true
    commit_message: "docs(prd): add initial PRD"
```

### 更新文档

```yaml
document_engine:
  action: "update"
  file_path: "docs/prd/[产品名称]-prd.md"

  changes:
    - section: "features"
      action: "append"
      content: |
        ### 新功能

        描述...

    - section: "timeline"
      action: "replace"
      content: |
        更新的时间线...

  options:
    create_backup: true
    update_version: true
    auto_commit: true
```

### 格式化文档

```yaml
document_engine:
  action: "format"
  file_path: "docs/prd/[产品名称]-prd.md"

  options:
    line_width: 100
    indent_spaces: 2
    list_style: "consistent"
    table_format: "compact"
    add_section_dividers: true
```

## 文档模板

### PRD 模板结构

```markdown
---
title: "{{project_name}} 产品需求文档"
version: "{{version}}"
date: "{{date}}"
author: "{{author}}"
status: "{{status}}"
tags: [prd, {{category}}]
---

# {{project_name}} PRD

**版本**: {{version}}
**日期**: {{date}}
**作者**: {{author}}
**状态**: {{status}}

---

## 目录

{{toc}}

---

## 1. 问题陈述

{{problem_statement}}

## 2. 目标用户

{{target_users}}

...

---

*本文档由 Document Engine 自动生成*
*版本历史: {{changelog}}*
```

### 威胁模型模板结构

```markdown
---
title: "{{project_name}} STRIDE 威胁建模"
version: "{{version}}"
date: "{{date}}"
author: "{{author}}"
framework: "STRIDE"
---

# {{project_name}} - STRIDE 威胁建模报告

## 目录

{{toc}}

---

## 1. 执行摘要

{{executive_summary}}

## 2. 系统边界

{{system_boundaries}}

## 3. STRIDE 分析

### 3.1 Spoofing (伪装)

{{spoofing_threats}}

...

---

## 附录

{{appendix}}

*本文档遵循 STRIDE 威胁建模方法论*
```

## 格式化规则

### 标题层级

```markdown
# 一级标题 (H1) - 文档标题，每个文档只有一个

## 二级标题 (H2) - 主要章节

### 三级标题 (H3) - 子章节

#### 四级标题 (H4) - 细节说明

##### 五级标题 (H5) - 极少使用，避免过深嵌套

###### 六级标题 (H6) - 不推荐使用
```

### 列表格式

```markdown
# 无序列表 - 使用连字符 (-)

- 第一项
- 第二项
  - 嵌套项
  - 另一个嵌套项
- 第三项

# 有序列表 - 使用数字

1. 第一步
2. 第二步
   1. 子步骤 2.1
   2. 子步骤 2.2
3. 第三步
```

### 表格格式

```markdown
# 紧凑表格

| 列1 | 列2 | 列3 |
|-----|-----|-----|
| 数据1 | 数据2 | 数据3 |

# 对齐表格

| 左对齐 | 居中 | 右对齐 |
|:-------|:----:|-------:|
| left   | center | right |
```

### 代码块

```markdown
# 行内代码
使用 `反引号` 包裹代码

# 代码块
```语言
代码内容
```

# 围栏代码块（推荐）
```python
def hello():
    print("Hello, World!")
```
```

## 版本控制集成

### Conventional Commits

```yaml
文档相关提交类型:
  docs: 文档更新
  docs(prd): PRD 更新
  docs(threat): 威胁模型更新
  docs(compliance): 合规文档更新
  docs(fix): 文档修正

提交格式:
  docs(type): brief description

  详细描述（可选）

  关联 issue: #123
```

### 版本历史

```markdown
## 版本历史

| 版本 | 日期 | 变更 | 作者 |
|------|------|------|------|
| 1.2.0 | [日期] | 添加安全章节 | [作者] |
| 1.1.0 | [日期] | 更新技术规格 | [作者] |
| 1.0.0 | [日期] | 初始版本 | [作者] |
```

### 变更日志

```markdown
# 变更日志

## [1.2.0] - [日期]

### 新增
- 添加安全与隐私章节
- 添加威胁建模附录

### 变更
- 更新技术架构图
- 调整优先级排序

### 修复
- 修正表格格式问题
- 补充缺失的验收标准
```

## 导出功能

### HTML 导出

```yaml
选项:
  theme: "github" | "gitbook" | "custom"
  include_css: true
  syntax_highlight: "highlight.js" | "prism"
  responsive: true
  include_toc: true
  toc_sticky: true
```

### PDF 导出

```yaml
选项:
  page_size: "A4" | "Letter"
  margin: "2cm"
  font: "Helvetica" | "Arial" | "custom"
  include_page_numbers: true
  toc_page: true
  header: "文档标题"
  footer: "页码"
```

## 最佳实践

✅ **DO**:
- 使用一致的标题层级
- 保持每行 < 100 字符
- 添加有意义的 Alt 文本（图片）
- 使用语义化的标记
- 定期更新版本历史

❌ **DON'T**:
- 嵌套超过 4 层标题
- 混用不同的列表样式
- 忽略可访问性
- 硬编码路径和 URL
- 跳过版本控制

## 集成点

此引擎被以下技能使用：
- **prd-generator**: 生成 PRD 文档
- **threat-modeling**: 生成威胁模型报告
- **compliance-checker**: 生成合规清单
- **security-use-case-generator**: 生成测试用例
- **所有其他技能**: 文档格式化和输出

## 测试示例

```bash
# 创建新文档
document-engine create \
  --type prd \
  --output docs/prd/[产品名称]-prd.md

# 格式化现有文档
document-engine format docs/prd/[产品名称]-prd.md

# 生成目录
document-engine toc docs/prd/[产品名称]-prd.md

# 导出 PDF
document-engine export \
  --input docs/prd/[产品名称]-prd.md \
  --format pdf \
  --output docs/prd/[产品名称]-prd.pdf
```
