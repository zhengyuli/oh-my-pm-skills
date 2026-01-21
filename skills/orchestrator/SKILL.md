---
name: orchestrator
description: 技能编排器 - 根据上下文自动组合和调用技能，支持多步骤工作流
version: 2.0.0
author: oh-my-pm-skills
tags: [orchestration, workflow, skills-management]
allowed-tools: Read, Write, Edit
model: inherit
---

# Skills Orchestrator v2.0

技能编排器负责根据用户输入和上下文，自动选择、组合和调用合适的技能，支持复杂的多步骤工作流。

## When to Use This Orchestrator

当用户请求需要多个技能协作时，orchestrator 自动激活：
- 产品想法 → 完整 PRD（包含威胁建模、合规检查）
- 安全事件 → 响应流程（影响分析、用例生成）
- 需求评估 → 优先级排序 + JTBD 分析
- 审计准备 → 合规检查 + 测试用例 + 证据收集

## 工作流定义语言 (WDL)

### 工作流结构

```yaml
workflow:
  name: "workflow-name"
  description: "工作流描述"
  version: "1.0.0"
  author: "author"

  input:
    - name: "input_name"
      type: "string|object|array"
      required: true
      description: "输入描述"

  output:
    - name: "output_name"
      type: "string|object|array"
      description: "输出描述"

  skills:
    - id: "step-1"
      skill: "skill-name"
      action: "action_name"
      input:
        from: "workflow.input"
        transform: "{{data}}"
      output:
        to: "step-2.input"
      on_error: "continue|stop|fallback"

    - id: "step-2"
      skill: "another-skill"
      depends_on: ["step-1"]
      # ...

  parallel:
    - name: "branch-1"
      skills: ["skill-a", "skill-b"]
    - name: "branch-2"
      skills: ["skill-c", "skill-d"]

  fallback:
    on_failure: "workflow-error-handler"
    retry_policy:
      max_retries: 3
      backoff: "exponential"
```

### 编排模式

#### Pipeline 模式（顺序执行）

```yaml
模式: 步骤按顺序执行，每个步骤的输出作为下一步的输入

workflow:
  name: "prd-generation-pipeline"
  type: "pipeline"

  steps:
    1. research-assistant:analyze → 市场数据
    2. jtbd-analyzer:analyze → 用户需求
    3. qa-engine:validate → 澄清问题
    4. priority-evaluator:score → 功能优先级
    5. prd-generator:generate → 最终 PRD
```

#### Fan-out 模式（并行执行）

```yaml
模式: 多个技能并行执行，最后聚合结果

workflow:
  name: "comprehensive-analysis"
  type: "fan-out"

  parallel:
    branch-a:
      - threat-modeling:analyze
      - impact-analyzer:assess
    branch-b:
      - compliance-checker:verify
      - security-use-case-generator:generate

  aggregate:
    skill: "document-engine"
    action: "merge"
```

#### Feedback 模式（反馈循环）

```yaml
模式: 步骤执行后返回前面步骤，基于结果迭代

workflow:
  name: "iterative-refinement"
  type: "feedback"

  steps:
    1. prd-generator:generate → 草稿 PRD
    2. qa-engine:validate → 识别问题
    3. if quality < threshold:
         goto step 1  # 重新生成
       else:
         continue
    4. document-engine:create → 最终文档
```

#### Conditional 模式（条件分支）

```yaml
模式: 基于条件选择不同路径

workflow:
  name: "conditional-prd"
  type: "conditional"

  condition:
    if: input.is_security_product
    then:
      workflow: "security-prd-workflow"
    else:
      workflow: "standard-prd-workflow"
```

## 预定义工作流

### 工作流 1: full-security-prd

**用途**: 为安全产品生成完整的 17 节 PRD

```yaml
workflow:
  name: "full-security-prd"
  description: "为安全产品生成包含威胁建模和合规的完整 PRD"
  duration: "1-2 days"
  skills: 8

  input:
    product_idea: string
    target_users: array
    key_features: array

  output:
    prd_document: file (17 sections)
    threat_model: file
    compliance_report: file
    test_plan: file

  pipeline:
    # 阶段 1: 市场和用户分析
    - id: "market-research"
      skill: "research-assistant"
      action: "market_analysis"
      input:
        product_idea: "{{workflow.input.product_idea}}"
        competitors: ["known-competitors"]
      output:
        market_data: object

    - id: "jtbd-analysis"
      skill: "jtbd-analyzer"
      action: "analyze"
      input:
        product_idea: "{{workflow.input.product_idea}}"
        target_users: "{{workflow.input.target_users}}"
      output:
        user_insights: object

    # 阶段 2: 需求澄清和优先级
    - id: "qa-validation"
      skill: "qa-engine"
      action: "generate_questions"
      input:
        context: "prd_generation"
        product_idea: "{{workflow.input.product_idea}}"
      output:
        questions: array

    - id: "collect-answers"
      type: "human_input"
      description: "用户回答问题"

    - id: "priority-scoring"
      skill: "priority-evaluator"
      action: "score"
      input:
        features: "{{workflow.input.key_features}}"
        model: "RICE"
      output:
        prioritized_features: array

    # 阶段 3: 安全分析（并行）
    parallel:
      branch-security:
        - id: "threat-model"
          skill: "threat-modeling"
          action: "analyze"
          input:
            system_description: "{{workflow.input.product_idea}}"
            methodology: "STRIDE"
          output:
            threat_model: object

        - id: "compliance-check"
          skill: "compliance-checker"
          action: "assess"
          input:
            frameworks: ["SOC2", "ISO27001"]
          output:
            compliance_report: object

      branch-testing:
        - id: "test-cases"
          skill: "security-use-case-generator"
          action: "generate"
          input:
            framework: "OWASP"
          output:
            test_plan: object

    # 阶段 4: 生成 PRD
    - id: "generate-prd"
      skill: "prd-generator"
      action: "generate"
      input:
        type: "prd-security"
        product_idea: "{{workflow.input.product_idea}}"
        market_research: "{{market-research.market_data}}"
        user_insights: "{{jtbd-analysis.user_insights}}"
        prioritized_features: "{{priority-scoring.prioritized_features}}"
        threat_model: "{{threat-model.threat_model}}"
        compliance_requirements: "{{compliance-check.compliance_report}}"
      output:
        prd_content: string

    # 阶段 5: 生成文档
    - id: "create-documents"
      skill: "document-engine"
      action: "create"
      input:
        prd: "{{generate-prd.prd_content}}"
        threat_model: "{{threat-model.threat_model}}"
        compliance: "{{compliance-check.compliance_report}}"
        test_plan: "{{test-cases.test_plan}}"
      output:
        files:
          - "docs/prd/{{product_slug}}-prd.md"
          - "docs/security/{{product_slug}}-threat-model.md"
          - "docs/compliance/{{product_slug}}-compliance.md"
          - "docs/security/{{product_slug}}-test-plan.md"

  on_success:
    message: "安全产品 PRD 生成完成！"
    next_steps:
      - "审阅生成的 PRD"
      - "与安全团队验证威胁模型"
      - "开始合规准备"
```

### 工作流 2: quick-prd

**用途**: 快速生成 Lean PRD（8 节）

```yaml
workflow:
  name: "quick-prd"
  description: "快速生成精简 PRD，适合 MVP 验证"
  duration: "1-2 hours"
  skills: 3

  input:
    product_idea: string

  output:
    prd_document: file (8 sections)

  pipeline:
    - id: "jtbd-quick"
      skill: "jtbd-analyzer"
      mode: "quick"
      action: "analyze"
      input:
        product_idea: "{{workflow.input.product_idea}}"

    - id: "qa-minimal"
      skill: "qa-engine"
      mode: "essential"
      action: "validate"
      questions: 3-5

    - id: "generate-lean-prd"
      skill: "prd-generator"
      action: "generate"
      input:
        type: "prd-lean"
        sections: 8
```

### 工作流 3: incident-response

**用途**: 安全事件响应流程

```yaml
workflow:
  name: "incident-response"
  description: "处理安全事件的完整响应流程"
  duration: "2-6 hours"
  skills: 4

  input:
    vulnerability_description: string
    severity: string

  output:
    impact_report: file
    mitigation_plan: file
    test_cases: file
    compliance_impact: file

  pipeline:
    # 阶段 1: 影响评估
    - id: "cvss-scoring"
      skill: "impact-analyzer"
      action: "assess"
      input:
        vulnerability: "{{workflow.input.vulnerability_description}}"
      output:
        cvss_score: number
        business_impact: object

    - id: "update-threat-model"
      skill: "threat-modeling"
      action: "update"
      input:
        new_vulnerability: "{{workflow.input.vulnerability_description}}"
      output:
        updated_threat_model: object

    # 阶段 2: 并行分析
    parallel:
      - id: "compliance-impact"
        skill: "compliance-checker"
        action: "assess_impact"
        input:
          vulnerability: "{{workflow.input.vulnerability_description}}"

      - id: "generate-tests"
        skill: "security-use-case-generator"
        action: "generate"
        input:
          vulnerability: "{{workflow.input.vulnerability_description}}"

    # 阶段 3: 响应计划
    - id: "mitigation-plan"
      skill: "template-engine"
      action: "render"
      input:
        template: "incident-response-plan"
        data:
          cvss: "{{cvss-scoring.cvss_score}}"
          impact: "{{cvss-scoring.business_impact}}"
          mitigations: "{{update-threat-model.mitigations}}"

  on_success:
    message: "事件响应计划已生成"
    priority: "high"
```

### 工作流 4: compliance-audit

**用途**: 合规审计准备

```yaml
workflow:
  name: "compliance-audit"
  description: "准备 SOC 2 / ISO 27001 审计"
  duration: "2-4 weeks"
  skills: 4

  input:
    framework: string (SOC2|ISO27001|GDPR)
    system_description: object

  output:
    gap_analysis: file
    evidence_checklist: file
    remediation_plan: file
    audit_readiness: number

  pipeline:
    - id: "initial-assessment"
      skill: "compliance-checker"
      action: "assess"
      input:
        framework: "{{workflow.input.framework}}"
      output:
        compliance_score: number
        gaps: array

    - id: "threat-model-review"
      skill: "threat-modeling"
      action: "map_to_compliance"
      input:
        framework: "{{workflow.input.framework}}"
      output:
        mapped_controls: object

    - id: "test-evidence"
      skill: "security-use-case-generator"
      action: "generate_evidence"
      input:
        framework: "{{workflow.input.framework}}"
        gaps: "{{initial-assessment.gaps}}"
      output:
        test_results: object

    - id: "remediation-plan"
      skill: "priority-evaluator"
      action: "prioritize"
      input:
        items: "{{initial-assessment.gaps}}"
        model: "RICE"
      output:
        prioritized_plan: object

    - id: "audit-package"
      skill: "document-engine"
      action: "create"
      input:
        gap_analysis: "{{initial-assessment.gaps}}"
        evidence: "{{test-evidence.test_results}}"
        remediation: "{{remediation-plan.prioritized_plan}}"
      output:
        audit_package: file
```

## 技能组合表

| 用户意图 | 工作流 | 必需技能 | 可选技能 | 输出 |
|---------|--------|---------|---------|------|
| 生成安全产品 PRD | full-security-prd | prd-generator, threat-modeling, compliance-checker | research-assistant, jtbd-analyzer, priority-evaluator, security-use-case-generator | 完整 PRD 包 |
| 快速 PRD 验证 | quick-prd | prd-generator, jtbd-analyzer | qa-engine | Lean PRD |
| 安全事件响应 | incident-response | impact-analyzer, threat-modeling | security-use-case-generator, compliance-checker | 响应计划 |
| 合规审计准备 | compliance-audit | compliance-checker, threat-modeling | security-use-case-generator, priority-evaluator | 审计包 |
| 功能优先级评估 | priority-evaluation | priority-evaluator | jtbd-analyzer, qa-engine | 排序报告 |
| 威胁建模 | threat-modeling-only | threat-modeling | research-assistant, impact-analyzer | 威胁模型 |
| 数据驱动产品决策 | data-driven-decision | analytics-engine, research-assistant | forecast-engine, priority-evaluator | 分析报告 + 预测 |
| 产品规划与预测 | product-forecasting | forecast-engine, research-assistant | analytics-engine, prd-generator | 增长预测 + 收入预测 |

## 工作流执行

### 执行引擎

```yaml
执行模式:
  sequential: 顺序执行每个步骤
  parallel: 并行执行独立分支
  conditional: 基于条件选择路径
  loop: 循环直到满足条件

错误处理:
  continue_on_error: 继续执行下一步
  stop_on_error: 停止工作流
  retry: 重试失败步骤
  fallback: 使用备用技能

超时控制:
  default_timeout: 120 秒
  skill_timeout: 60 秒
  workflow_timeout: 600 秒
```

### 执行状态

```yaml
状态:
  pending: 等待执行
  running: 正在执行
  completed: 成功完成
  failed: 执行失败
  skipped: 被跳过
  retrying: 重试中

结果:
  output: 步骤输出
  error: 错误信息
  duration: 执行时长
  timestamp: 时间戳
```

## 工作流 API

### 启动工作流

```yaml
orchestrator:
  action: "start_workflow"
  workflow: "full-security-prd"
  input:
    product_idea: "企业密钥管理系统"
    target_users: ["IT管理员", "安全工程师"]
    key_features: ["统一存储", "访问控制", "审计日志"]

  options:
    async: true
    notify_on_completion: true
    save_intermediate: true
```

### 查询状态

```yaml
orchestrator:
  action: "get_status"
  workflow_id: "{{workflow_id}}"

  output:
    status: "running"
    progress: 60
    current_step: "threat-modeling"
    completed_steps: ["market-research", "jtbd-analysis"]
    estimated_completion: "[完成时间]"
```

### 取消工作流

```yaml
orchestrator:
  action: "cancel"
  workflow_id: "{{workflow_id}}"
  reason: "用户取消"
```

## 错误处理

### 技能加载失败

```yaml
错误: skill_not_found
处理:
  1. 记录错误日志
  2. 尝试加载替代技能
  3. 如果失败，跳过该步骤
  4. 继续执行或根据配置停止

通知:
  message: "技能 {{skill_name}} 未找到，使用替代方案"
  fallback_skill: "{{fallback_skill}}"
```

### 超时处理

```yaml
错误: timeout
处理:
  1. 保存中间结果
  2. 标记步骤为超时
  3. 根据配置决定继续或停止
  4. 通知用户

重试策略:
  max_retries: 3
  backoff: "exponential"
  initial_delay: 1 秒
```

### 数据验证失败

```yaml
错误: validation_failed
处理:
  1. 识别缺失或无效数据
  2. 生成数据收集问题
  3. 等待用户输入
  4. 重新执行步骤
```

## 性能优化

### 并行执行

```yaml
策略: 识别独立步骤，并行执行

示例:
  威胁建模 + 合规检查 可并行执行
  市场研究 + JTBD 分析 可并行执行

性能提升: 50-70%
```

### 缓存

```yaml
缓存策略:
  skill_output: 缓存技能输出 (1 小时)
  template_rendered: 缓存渲染模板 (24 小时)
  research_data: 缓存研究数据 (7 天)

缓存失效:
  时间过期
  数据更新
  手动清除
```

### 增量执行

```yaml
策略: 只执行变更的步骤

适用:
  大型工作流
  多次迭代
  部分更新

实现:
  检测输入变更
  跳过未受影响步骤
  复用之前结果
```

## 最佳实践

✅ **DO**:
- 使用预定义工作流
- 监控工作流执行
- 保存中间结果
- 处理错误和超时
- 优化并行执行

❌ **DON'T**:
- 过度编排（超过 5 个技能）
- 创建循环依赖
- 忽视错误处理
- 跳过数据验证
- 硬编码工作流

## 集成点

此编排器被以下系统使用：
- **Claude Code**: 自动激活编排
- **用户**: 显式调用工作流
- **Sub-Agents**: 作为工作流引擎
- **CI/CD**: DevSecOps 集成

## 输出格式

### 工作流启动成功

```yaml
result:
  success: true
  workflow_id: "{{uuid}}"
  workflow_name: "{{workflow}}"
  status: "running"
  estimated_duration: "{{duration}}"

  steps:
    - id: "step-1"
      name: "{{step_name}}"
      skill: "{{skill}}"
      status: "pending"
    - id: "step-2"
      name: "{{step_name}}"
      skill: "{{skill}}"
      status: "pending"

  webhook_url: "{{callback_url}}"
```

### 工作流完成

```yaml
result:
  success: true
  workflow_id: "{{uuid}}"
  status: "completed"
  duration: "{{duration}}"

  outputs:
    prd_document: "{{path}}"
    threat_model: "{{path}}"
    compliance_report: "{{path}}"

  summary:
    total_steps: {{count}}
    completed: {{count}}
    failed: {{count}}
    skipped: {{count}}
```

## 测试场景

```bash
# 执行完整安全 PRD 工作流
orchestrator execute \
  --workflow "full-security-prd" \
  --input "product_idea=[产品名称]"

# 查询工作流状态
orchestrator status \
  --workflow-id "{{workflow_id}}"

# 取消工作流
orchestrator cancel \
  --workflow-id "{{workflow_id}}"
```
