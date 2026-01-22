# 🎯 Oh-My-PM-Skills

> 面向产品经理的 AI 技能集合系统 - 从市场研究、JTBD分析、威胁建模到PRD生成的全流程支持

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.1-green.svg)](https://github.com/zhengyuli/oh-my-pm-skills)
[![Claude Code](https://img.shields.io/badge/Claude_Code-Compatible-purple.svg)](https://code.anthropic.com)

---

## ✨ 特性

- 📊 **数据驱动决策** - RICE/ICE 优先级评估、A/B 测试分析、用户增长预测
- 🔒 **安全优先** - 内置 STRIDE 威胁建模、SOC 2 合规检查、安全测试用例生成
- 🤖 **AI 赋能** - 基于 Claude Code 的智能技能系统，自动化产品工作流
- 📝 **模板驱动** - 11 种专业模板，保证输出格式一致性
- 🔄 **工作流编排** - 支持多技能组合，一键生成完整产品分析报告

---

## 📦 安装

### 方式 1: 通过 Claude Code Marketplace

```bash
/plugin install https://github.com/zhengyuli/oh-my-pm-skills
```

### 方式 2: 手动安装

```bash
# 克隆仓库
git clone https://github.com/zhengyuli/oh-my-pm-skills.git
cd oh-my-pm-skills

# 确保目录结构正确
ls commands/ skills/ templates/
```

重启 Claude Code 即可加载插件。

---

## 🚀 快速开始

### 基础命令

```bash
# 快速生成 Lean PRD
/PM-PRD

# 全面产品分析（推荐）
/PM-Full-Analysis

# 威胁建模
/PM-Threat-Model

# 市场研究
/PM-Market-Research

# JTBD 用户洞察
/PM-JTBD

# 数据分析
/PM-Analytics

# 增长预测
/PM-Forecast

# 竞品分析
/PM-Competitor
```

### 使用示例

```
用户: /PM-Market-Research AI安全产品，进入评估

AI: [调用 research-assistant + forecast-engine + priority-evaluator]

    # 生成内容包括：
    - TAM/SAM/SOM 市场规模分析
    - Top 10 上市公司和创业公司竞品分析
    - Gartner/Forrester/IDC 权威报告引用
    - 客户画像和痛点分析
    - ICE 机会评估矩阵
    - 投资回报分析和盈亏平衡预测
```

---

## 📁 项目结构

```
oh-my-pm-skills/
├── .claude-plugin/
│   ├── marketplace.json      # Marketplace 配置
│   └── plugin.json           # Plugin 配置
├── commands/                 # 8 个用户命令
│   ├── PM-Analytics.md       # 数据分析报告
│   ├── PM-Forecast.md        # 增长预测报告
│   ├── PM-Threat-Model.md   # STRIDE 威胁建模
│   ├── PM-PRD.md             # PRD 文档生成
│   ├── PM-JTBD.md            # JTBD 用户洞察
│   ├── PM-Market-Research.md # 市场研究报告
│   ├── PM-Competitor.md      # 竞品分析
│   └── PM-Full-Analysis.md   # 一站式产品分析
├── skills/                   # 14 个技能
│   ├── core/                 # 核心技能 (4个)
│   │   ├── research-assistant/     # 市场研究
│   │   ├── jtbd-analyzer/          # JTBD 分析
│   │   ├── priority-evaluator/     # 优先级评估
│   │   └── prd-generator/          # PRD 生成
│   ├── engines/              # 分析引擎 (6个)
│   │   ├── analytics-engine/       # 数据分析
│   │   ├── forecast-engine/        # 预测引擎
│   │   ├── scoring-engine/         # 评分引擎
│   │   ├── document-engine/        # 文档引擎
│   │   ├── qa-engine/              # 质量保证
│   │   └── template-engine/        # 模板渲染
│   ├── security/             # 安全技能 (4个)
│   │   ├── threat-modeling/        # STRIDE 威胁建模
│   │   ├── compliance-checker/     # SOC2/ISO27001 合规
│   │   ├── impact-analyzer/        # CVSS 影响分析
│   │   └── security-use-case-generator/ # 安全用例生成
├── templates/                # 11 个模板
│   ├── prd/                  # PRD 模板
│   ├── security/             # 安全模板
│   ├── research/             # 研究模板
│   └── config.yaml           # 模板配置
├── CLAUDE.md                 # 项目文档
├── README.md                 # 本文件
└── .gitignore                # Git 忽略规则
```

---

## 🧩 核心技能

### 核心技能 (Core Skills)

| 技能 | 功能 | 输出 |
|------|------|------|
| **research-assistant** | 市场研究与竞品分析 | TAM/SAM/SOM、SWOT、竞争格局 |
| **jtbd-analyzer** | JTBD 用户动机分析 | 待办任务、四力量、雇佣标准 |
| **priority-evaluator** | RICE/ICE 优先级评估 | 功能排序、机会矩阵 |
| **prd-generator** | PRD 文档生成 | Lean/Standard/Security PRD |

### 分析引擎 (Engines)

| 引擎 | 功能 | 输出 |
|------|------|------|
| **analytics-engine** | 数据分析 | DAU/MAU、漏斗分析、A/B测试 |
| **forecast-engine** | 增长预测 | TAM/SAM/SOM、用户增长、收入预测 |
| **scoring-engine** | 评分系统 | RICE、ICE、DREAD 评分 |
| **document-engine** | 文档管理 | 文档生成、版本管理 |
| **qa-engine** | 质量保证 | 内容验证、问题生成 |
| **template-engine** | 模板渲染 | 变量插值、条件渲染 |

### 安全技能 (Security Skills)

| 技能 | 功能 | 输出 |
|------|------|------|
| **threat-modeling** | STRIDE/DREAD 威胁建模 | 威胁识别、风险评估、缓解措施 |
| **compliance-checker** | SOC2/ISO27001 合规检查 | 差距分析、审计清单 |
| **impact-analyzer** | CVSS 影响分析 | 风险评级、业务影响 |
| **security-use-case-generator** | OWASP 测试用例 | 测试计划、安全场景 |

---

## 📊 模板系统

### PRD 模板

| 模板 | 章节 | 适用场景 |
|------|------|---------|
| **prd-lean** | 8 节 | MVP验证、快速迭代 |
| **prd-standard** | 15 节 | 正式产品规划 |
| **prd-security** | 17 节 | 安全产品、合规要求 |

### 安全模板

| 模板 | 框架 | 适用场景 |
|------|------|---------|
| **threat-stride** | STRIDE + DREAD | 威胁建模报告 |
| **compliance-soc2** | SOC 2 TSC | 合规检查清单 |
| **security-test-plan** | OWASP | 安全测试计划 |

### 研究模板

| 模板 | 内容 | 适用场景 |
|------|------|---------|
| **market-research** | 市场规模、竞争、客户 | 市场进入评估 |
| **jtbd-analysis** | 四力量分析 | 用户洞察研究 |
| **competitor-analysis** | Porter's Five Forces | 竞品深度分析 |

---

## 🎯 使用场景

### 场景 1: 快速 PRD 生成

```bash
/PM-PRD

# 输入：产品想法
# 输出：8 节 Lean PRD（包含背景、目标、功能、指标等）
```

### 场景 2: 完整产品分析

```bash
/PM-Full-Analysis

# 输入：产品想法或市场机会
# 输出：6 份完整报告
#   - PRD 文档
#   - 市场研究报告
#   - JTBD 分析报告
#   - 增长预测报告
#   - 威胁建模报告
#   - 执行摘要
```

### 场景 3: 安全产品开发

```bash
/PM-Threat-Model

# 输入：产品功能列表
# 输出：STRIDE 威胁建模报告
#   - 威胁识别（6 类）
#   - DREAD 风险评分
#   - 缓解措施建议
#   - 合规检查清单
```

### 场景 4: 市场进入决策

```bash
/PM-Market-Research

# 输入：目标市场
# 输出：市场研究报告
#   - TAM/SAM/SOM 分析
#   - Top 10 竞品分析
#   - 客户画像和痛点
#   - ICE 机会评估
#   - 投资回报分析
```

---

## 🔧 技术架构

### 技术栈

- **模板引擎**: Handlebars/Mustache 风格
- **配置格式**: YAML
- **文档格式**: Markdown
- **AI 集成**: Claude Code Skills 系统

### 设计原则

1. **模块化** - 每个技能独立运作，可单独调用
2. **可组合** - 多个技能可组合使用完成复杂任务
3. **模板驱动** - 所有输出基于模板，保证格式一致性
4. **安全内置** - 安全考虑贯穿整个产品生命周期

---

## 📈 权威数据源

research-assistant 技能集成了以下权威数据源：

### 咨询机构报告
- **Gartner** - Magic Quadrant、Market Size、Vendor Matrix
- **Forrester** - Wave、Market Overview、Scorecards
- **IDC** - MarketScape、Market Forecast、Key Trends
- **CB Insights** - Emerging Trends、Funding Data、Unicorns

### 投资数据库
- **Crunchbase** - 融资历史、估值、投资人信息
- **PitchBook** - 交易条款、估值变化、投资组合

### 上市公司数据
- **SEC EDGAR** - 10-K、10-Q、8-K 财报文件
- **公司官网** - 投资者关系页面、产品路线图

---

## 🤝 贡献指南

欢迎贡献！请遵循以下步骤：

### 添加新技能

1. 在 `skills/` 下创建新目录
2. 创建 `SKILL.md` 文件，包含：
   ```yaml
   ---
   name: skill-name
   description: 技能描述
   version: 1.0.0
   author: oh-my-pm-skills
   tags: [tag1, tag2]
   allowed-tools: Read, Write, Edit
   model: inherit
   ---
   ```
3. 定义技能流程和输出格式

### 添加新模板

1. 在 `templates/` 下创建新文件
2. 使用 Handlebars 语法
3. 在 `config.yaml` 中注册
4. 添加示例数据到 `templates/examples/`

### 添加新命令

1. 在 `commands/` 下创建新文件
2. 定义调用的技能
3. 提供使用说明和示例

---

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE)

---

## 🌟 致谢

本项目基于以下资源和最佳实践：

- [Claude Code Documentation](https://code.anthropic.com/docs/en/intro)
- [STRIDE Threat Modeling](https://learn.microsoft.com/en-us/azure/architecture/patterns/threat-modeling)
- [RICE Prioritization](https://www.intercom.com/blog/rice-simple-prioritization-for-product-managers/)
- [Jobs to be Done](https://www.hbr.org/2016/09/know-your-customers-jobs-to-be-done)
- [Handlebars.js](https://handlebarsjs.com/)

---

## 📮 联系方式

- **作者**: Zhengyu Li
- **项目主页**: https://github.com/zhengyuli/oh-my-pm-skills
- **问题反馈**: https://github.com/zhengyuli/oh-my-pm-skills/issues

---

<div align="center">

**让 AI 成为产品经理的最强助手** ⚡

Made with ❤️ by Zhengyu Li

</div>
