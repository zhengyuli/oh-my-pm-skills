# {{project_name}} - STRIDE 威胁建模报告

**版本**: {{version}}
**日期**: {{date}}
**作者**: {{author}}
**框架**: STRIDE + DREAD

---

## 执行摘要

### 关键发现

{{#each key_findings}}
{{@index}}. {{finding}}
{{/each}}

### 风险统计

| 风险等级 | 威胁数量 | 占比 |
|---------|---------|------|
| 高风险 (8-10) | {{high_count}} | {{high_percentage}}% |
| 中风险 (5-7) | {{medium_count}} | {{medium_percentage}}% |
| 低风险 (1-4) | {{low_count}} | {{low_percentage}}% |

### 总体风险评分

**总体评分**: {{overall_risk_score}} / 10
**风险等级**: {{risk_level}}

---

## 系统概览

### 系统架构

```
{{architecture_diagram}}
```

### 系统边界

{{#each system_boundaries}}

#### {{name}}

**类型**: {{type}}
**信任级别**: {{trust_level}}

**数据流**:
{{#each data_flows}}
- {{from}} → {{to}}: {{data}} ({{protocol}})
{{/each}}

**关键资产**:
{{#each assets}}
- **{{asset}}**: {{sensitivity}} ({{value}})
{{/each}}

{{/each}}

---

## STRIDE 威胁分析

### 1. Spoofing (身份伪装)

{{#each spoofing_threats}}

#### {{title}}

**描述**: {{description}}

**目标组件**: {{target_component}}

**STRIDE 类别**: Spoofing (S)

**攻击场景**: {{attack_scenario}}

**现有控制**: {{existing_controls}}

**DREAD 评分**: {{dread_score}} / 10

| 维度 | 评分 | 说明 |
|------|------|------|
| Damage (损害) | {{damage}} | {{damage_reason}} |
| Reproducibility (可复现) | {{reproducibility}} | {{reproducibility_reason}} |
| Exploitability (可利用) | {{exploitability}} | {{exploitability_reason}} |
| Affected Users (受影响用户) | {{affected}} | {{affected_reason}} |
| Discoverability (可发现) | {{discoverability}} | {{discoverability_reason}} |

**风险等级**: {{risk_level}}

**缓解措施**:
{{#each mitigations}}
- [ ] {{measure}} (优先级: {{priority}}, 负责人: {{owner}}, 截止: {{due_date}})
{{/each}}

**预计成本**: ${{estimated_cost}}
**预计时间**: {{estimated_time}}

**残留风险**: {{residual_risk}}

{{/each}}

---

### 2. Tampering (数据篡改)

{{#each tampering_threats}}

#### {{title}}

**描述**: {{description}}

**目标组件**: {{target_component}}

**STRIDE 类别**: Tampering (T)

**攻击场景**: {{attack_scenario}}

**现有控制**: {{existing_controls}}

**DREAD 评分**: {{dread_score}} / 10

| 维度 | 评分 | 说明 |
|------|------|------|
| Damage | {{damage}} | {{damage_reason}} |
| Reproducibility | {{reproducibility}} | {{reproducibility_reason}} |
| Exploitability | {{exploitability}} | {{exploitability_reason}} |
| Affected Users | {{affected}} | {{affected_reason}} |
| Discoverability | {{discoverability}} | {{discoverability_reason}} |

**风险等级**: {{risk_level}}

**缓解措施**:
{{#each mitigations}}
- [ ] {{measure}} (优先级: {{priority}}, 负责人: {{owner}})
{{/each}}

**残留风险**: {{residual_risk}}

{{/each}}

---

### 3. Repudiation (行为抵赖)

{{#each repudiation_threats}}

#### {{title}}

**描述**: {{description}}

**STRIDE 类别**: Repudiation (R)

**攻击场景**: {{attack_scenario}}

**现有控制**: {{existing_controls}}

**DREAD 评分**: {{dread_score}} / 10

**风险等级**: {{risk_level}}

**缓解措施**:
{{#each mitigations}}
- [ ] {{measure}} (优先级: {{priority}}, 负责人: {{owner}})
{{/each}}

**残留风险**: {{residual_risk}}

{{/each}}

---

### 4. Information Disclosure (信息泄露)

{{#each information_disclosure_threats}}

#### {{title}}

**描述**: {{description}}

**STRIDE 类别**: Information Disclosure (I)

**攻击场景**: {{attack_scenario}}

**数据类型**: {{data_types}}
**敏感度**: {{sensitivity}}

**现有控制**: {{existing_controls}}

**DREAD 评分**: {{dread_score}} / 10

**风险等级**: {{risk_level}}

**缓解措施**:
{{#each mitigations}}
- [ ] {{measure}} (优先级: {{priority}}, 负责人: {{owner}})
{{/each}}

**残留风险**: {{residual_risk}}

{{/each}}

---

### 5. Denial of Service (拒绝服务)

{{#each dos_threats}}

#### {{title}}

**描述**: {{description}}

**STRIDE 类别**: Denial of Service (D)

**攻击场景**: {{attack_scenario}}

**现有控制**: {{existing_controls}}

**DREAD 评分**: {{dread_score}} / 10

**风险等级**: {{risk_level}}

**缓解措施**:
{{#each mitigations}}
- [ ] {{measure}} (优先级: {{priority}}, 负责人: {{owner}})
{{/each}}

**残留风险**: {{residual_risk}}

{{/each}}

---

### 6. Elevation of Privilege (权限提升)

{{#each elevation_threats}}

#### {{title}}

**描述**: {{description}}

**STRIDE 类别**: Elevation of Privilege (E)

**攻击场景**: {{attack_scenario}}

**现有控制**: {{existing_controls}}

**DREAD 评分**: {{dread_score}} / 10

**风险等级**: {{risk_level}}

**缓解措施**:
{{#each mitigations}}
- [ ] {{measure}} (优先级: {{priority}}, 负责人: {{owner}})
{{/each}}

**残留风险**: {{residual_risk}}

{{/each}}

---

## DREAD 风险评估

### 风险矩阵

| 威胁 | STRIDE | Damage | Repro | Exp | Aff | Disc | DREAD | 风险等级 |
|------|--------|--------|-------|------|-----|------|-------|---------|
{{#each threat_matrix}}
| {{name}} | {{stride}} | {{damage}} | {{repro}} | {{exp}} | {{affected}} | {{disc}} | {{dread}} | {{level}} |
{{/each}}

### 风险分布

**高风险威胁** (DREAD 8-10):
{{#each high_risk}}
- **{{threat}}**: {{dread}} 分
{{/each}}

**中风险威胁** (DREAD 5-7):
{{#each medium_risk}}
- **{{threat}}**: {{dread}} 分
{{/each}}

**低风险威胁** (DREAD 1-4):
{{#each low_risk}}
- **{{threat}}**: {{dread}} 分
{{/each}}

---

## 缓解措施

### 立即实施 (高风险)

{{#each immediate_mitigations}}
- [ ] **{{title}}** (威胁: {{threats}})
  - 描述: {{description}}
  - 优先级: P0
  - 负责人: {{owner}}
  - 截止: {{due_date}}
  - 预算: ${{budget}}
{{/each}}

### 近期规划 (中风险)

{{#each short_term_mitigations}}
- [ ] **{{title}}** (威胁: {{threats}})
  - 描述: {{description}}
  - 优先级: P1
  - 负责人: {{owner}}
  - 截止: {{due_date}}
{{/each}}

### 长期考虑 (低风险)

{{#each long_term_mitigations}}
- [ ] **{{title}}** (威胁: {{threats}})
  - 描述: {{description}}
  - 优先级: P2
  - 负责人: {{owner}}
{{/each}}

---

## 安全控制

### 技术控制

{{#each technical_controls}}
- **{{control}}**: {{description}}
  - 覆盖威胁: {{threats}}
  - 实施状态: {{status}}
  - 验证方法: {{verification}}
{{/each}}

### 管理控制

{{#each administrative_controls}}
- **{{control}}**: {{description}}
  - 覆盖威胁: {{threats}}
  - 实施状态: {{status}}
  - 验证方法: {{verification}}
{{/each}}

### 物理控制

{{#each physical_controls}}
- **{{control}}**: {{description}}
  - 覆盖威胁: {{threats}}
  - 实施状态: {{status}}
  - 验证方法: {{verification}}
{{/each}}

---

## 验证和测试

### 安全测试计划

{{#each security_tests}}
- **{{test_name}}**
  - 类型: {{type}}
  - 目标: {{target}}
  - 工具: {{tools}}
  - 频率: {{frequency}}
  - 责任人: {{owner}}
{{/each}}

### 验证方法

{{#each verification_methods}}
- **{{method}}**: {{description}}
{{/each}}

---

## 监控和响应

### 监控指标

{{#each monitoring_metrics}}
- **{{metric}}**: {{description}}
  - 阈值: {{threshold}}
  - 响应: {{response_action}}
  - 告警: {{alert}}
{{/each}}

### 事件响应

{{#each incident_responses}}
#### 威胁类型: {{threat_type}}
- 检测: {{detection}}
- 响应时间: {{response_time}}
- 响应步骤: {{response_steps}}
- 恢复: {{recovery}}
- 负责人: {{owner}}
{{/each}}

---

## 合规映射

### SOC 2 映射

{{#each soc2_mapping}}
- **{{control}}**: {{requirement}}
  - 相关威胁: {{related_threats}}
  - 控制措施: {{controls}}
{{/each}}

### ISO 27001 映射

{{#each iso27001_mapping}}
- **{{control}}**: {{requirement}}
  - 相关威胁: {{related_threats}}
  - 控制措施: {{controls}}
{{/each}}

---

## 附录

### 假设和前提

{{#each assumptions}}
- {{assumption}}
{{/each}}

### 使用的工具

{{#each tools_used}}
- **{{name}}**: {{purpose}}
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

*本报告由 Threat Modeling 技能自动生成*
*评估标准: STRIDE + DREAD*
