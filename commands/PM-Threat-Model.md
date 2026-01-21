# PM-Threat-Model: STRIDE 威胁建模

系统安全威胁建模和风险评估。

## 调用的技能

```
1. skills/security/threat-modeling
   ↓ STRIDE 威胁识别和 DREAD 评分

2. skills/engines/scoring-engine
   ↓ 风险评分计算和排序

3. skills/engines/template-engine
   ↓ 使用 threat-stride.md 模板输出
```

## 威胁建模框架

- **STRIDE 分析**:
  - S: Spoofing (身份伪装)
  - T: Tampering (数据篡改)
  - R: Repudiation (行为抵赖)
  - I: Information Disclosure (信息泄露)
  - D: Denial of Service (拒绝服务)
  - E: Elevation of Privilege (权限提升)

- **DREAD 评分** (1-10):
  - Damage (损害)、Reproducibility (可复现)
  - Exploitability (可利用)、Affected (受影响)
  - Discoverability (可发现)

## 开始

请提供：
- 系统架构和组件描述
- 数据流和信任边界
- 关键资产清单
