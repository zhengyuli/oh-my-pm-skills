# Citation Manager - 引用管理系统

> **版本**: 1.0.0
> **用途**: 为所有需要搜索数据的技能提供统一的引用管理机制
> **使用技能**: research-assistant, jtbd-analyzer, threat-modeling, forecast-engine, analytics-engine

---

## 核心功能

### 1. 引用格式标准

#### 引用编号格式

```yaml
引用编号规则:
  格式: "[来源缩写 年份]序号"
  示例:
    - "[Gartner 2024]¹"
    - "[IDC 2024]²"
    - "[SEC 2024]³"
    - "[Crunchbase 2024]⁴"

来源缩写映射:
  Gartner: Gartner
  Forrester: Forrester
  IDC: IDC
  SEC: SEC
  Crunchbase: CB
  TechCrunch: TC
  官网: Official
  其他: Other
```

#### 数据引用标注格式

```markdown
在报告正文中，每个数据点需要标注引用：

市场规摸为 $42.5 亿 [Gartner 2024]¹，年增长率 18% [IDC 2024]²。

Notion 拥有超过 3000 万用户 [Official 2024]³，最新融资估值达 100 亿美元 [CB 2024]⁴。
```

#### 参考文献章节格式

```markdown
## 参考文献

### 权威机构报告

[1] Gartner, Magic Quadrant for Cloud Security 2024
    - 发布日期: 2024-06
    - URL: https://www.gartner.com/en/documents/4123456
    - 访问状态: 需要注册
    - 备用链接: https://www.crowdstrike.com/blog/gartner-mq-2024
    - 搜索日期: 2025-01-22
    - 验证状态: 已通过 Tavily QNA 验证
    - 数据点: 市场规模、厂商排名

[2] IDC, Worldwide Cloud Security MarketScape 2024
    - 发布日期: 2024-05
    - URL: https://www.idc.com/research/4123457
    - 访问状态: 公开
    - 搜索日期: 2025-01-22
    - 验证状态: 未验证
    - 数据点: 市场预测、增长率

### 公司官方数据

[3] Notion, Official Website and Press Kit
    - 发布日期: 2024-12
    - URL: https://www.notion.com/press
    - 访问状态: 公开
    - 搜索日期: 2025-01-22
    - 验证状态: 已验证
    - 数据点: 用户数量、产品功能

### 投融资数据库

[4] Crunchbase, Notion Funding Rounds
    - 发布日期: 2024-03
    - URL: https://www.crunchbase.com/organization/notion
    - 访问状态: 需要注册
    - 备用链接: https://techcrunch.com/2024/03/15/notion-funding
    - 搜索日期: 2025-01-22
    - 验证状态: 已验证
    - 数据点: 融资历史、估值

### 媒体报道

[5] TechCrunch, "Notion reaches $10B valuation"
    - 发布日期: 2024-03-15
    - URL: https://techcrunch.com/2024/03/15/notion-valuation
    - 访问状态: 公开
    - 搜索日期: 2025-01-22
    - 验证状态: 未验证
    - 数据点: 估值、增长趋势
```

---

### 2. 引用收集流程

#### 步骤 1: 搜索时收集引用

```yaml
每次使用搜索引擎时:
  工具: WebSearch / Tavily / 其他
  收集信息:
    - 标题: 搜索结果的标题
    - URL: 完整链接
    - 发布日期: 如果可用
    - 来源名称: 网站/机构名称
    - 访问状态: 公开/需要注册
    - 数据点: 提取的具体数据

  存储格式:
    citations:
      - id: 1
        source: "Gartner"
        year: 2024
        title: "Magic Quadrant for Cloud Security 2024"
        url: "https://..."
        access_date: "2025-01-22"
        publication_date: "2024-06"
        access_status: "需要注册"
        verification_status: "已通过 Tavily QNA 验证"
        data_points: ["市场规模", "厂商排名"]
        search_method: "WebSearch"
```

#### 步骤 2: 数据点标注

```yaml
在报告中使用数据时:
  1. 确定数据点对应的引用 ID
  2. 在数据后添加引用标注: [来源 年份]ID
  3. 记录该引用被使用的位置

示例:
  数据: "市场规模 $42.5 亿"
  引用: citations[0] (Gartner 报告)
  标注: "市场规模 $42.5 亿 [Gartner 2024]¹"
  记录:
    used_in:
      - section: "市场概览"
        subsection: "市场规模"
        data_point: "$42.5 亿"
```

#### 步骤 3: 生成参考文献章节

```yaml
生成参考文献时:
  1. 按来源类型分组:
     - 权威机构报告
     - 公司官方数据
     - 投融资数据库
     - 媒体报道
     - 其他来源

  2. 每个引用包含:
     - 编号: [1], [2], [3]...
     - 标题: 来源标题
     - 发布日期: YYYY-MM-DD
     - URL: 完整链接
     - 访问状态: 公开/需要注册
     - 备用链接: 如果主链接需要注册
     - 搜索日期: YYYY-MM-DD
     - 验证状态: 已验证/未验证
     - 数据点: 该引用提供的数据列表

  3. 输出三个部分:
     a. 报告主体中的上标引用 [Gartner 2024]¹
     b. 报告末尾的详细参考文献
     c. 独立的 URLs 清单文件
```

---

### 3. 跨技能引用共享

#### 引用上下文传递

```yaml
技能调用链:
  research-assistant (收集引用)
    ↓ 传递 citations
  jtbd-analyzer (使用引用)
    ↓ 传递 citations
  prd-generator (汇总引用)
    ↓ 生成最终报告
  document-engine (格式化引用)

传递格式:
  context:
    citations:
      - id: 1
        source: "Gartner"
        year: 2024
        title: "..."
        url: "..."
        # ... 完整引用信息
    citation_counter: 5  # 下一个引用的编号
```

#### 引用去重

```yaml
当多个技能使用同一来源时:
  去则:
    - 相同 URL → 使用已有引用编号
    - 相同来源 + 相同年份 + 相同数据点 → 使用已有引用编号

  示例:
    research-assistant: Gartner 报告 → [1]
    jtbd-analyzer: 使用相同 Gartner 报告 → 仍然使用 [1]
    prd-generator: 最终参考文献只有一个 Gartner 条目 [1]
```

---

### 4. 链接可访问性检测（强制执行）

**⚠️ 重要**: 所有引用链接必须在收集时进行可访问性检测，确保不出现 404、403、500 等错误。

#### 检测流程

```yaml
每次收集引用链接时必须执行:
  1. 即时检测:
     - 使用 mcp__fetch__fetch 或 web_reader 检测链接
     - 记录 HTTP 状态码
     - 记录响应时间
     - 记录内容类型

  2. 状态分类:
     - 可访问: HTTP 200-299
     - 重定向: HTTP 300-399 (跟随重定向)
     - 客户端错误: HTTP 400-499 (404, 403等)
     - 服务器错误: HTTP 500-599
     - 超时: 响应时间 > 30秒
     - 网络错误: DNS失败、连接失败等

  3. 处理策略:
     - 可访问: 标记为"已验证"，记录状态码
     - 需要注册: 尝试获取备用公开链接
     - 404/403/500: 立即丢弃该链接，搜索替代来源
     - 超时: 重试1次，仍超时则丢弃
```

#### 链接状态检测实现

```python
# 伪代码示例
def check_url_accessibility(url, timeout=10):
    """
    检测链接可访问性

    返回:
        {
            'accessible': bool,
            'status_code': int,
            'status': str,
            'response_time_ms': int,
            'content_type': str,
            'error': str (如果失败)
        }
    """
    try:
        # 使用 mcp__fetch 检测
        response = mcp__fetch__fetch(
            url=url,
            max_length=1000,  # 只检测头部，不下载完整内容
            timeout=timeout
        )

        return {
            'accessible': True,
            'status_code': 200,  # fetch 成功视为可访问
            'status': '可访问',
            'response_time_ms': response_time,
            'content_type': 'text/html',
        }

    except TimeoutError:
        # 超时：重试一次
        try:
            response = mcp__fetch__fetch(url=url, timeout=timeout*2)
            return {'accessible': True, 'status': '可访问(慢)', ...}
        except:
            return {'accessible': False, 'status': '超时', 'error': '连接超时'}

    except HTTPError as e:
        if e.status_code == 404:
            return {'accessible': False, 'status': '404 Not Found', 'error': str(e)}
        elif e.status_code == 403:
            return {'accessible': False, 'status': '403 Forbidden', 'error': str(e)}
        elif e.status_code >= 500:
            return {'accessible': False, 'status': f'{e.status_code} Server Error', 'error': str(e)}
        else:
            return {'accessible': False, 'status': f'HTTP {e.status_code}', 'error': str(e)}

    except Exception as e:
        return {'accessible': False, 'status': '网络错误', 'error': str(e)}
```

#### 引用存储结构（增强版）

```yaml
context.citations:
  - id: 1
    source: "Gartner"
    year: 2024
    title: "完整标题"
    url: "https://..."

    # 链接可访问性检测（新增）
    url_check:
      accessible: true          # 是否可访问
      status_code: 200          # HTTP 状态码
      status: "可访问"          # 状态描述
      response_time_ms: 1250    # 响应时间
      content_type: "text/html" # 内容类型
      checked_at: "2025-01-22T10:30:00Z"  # 检测时间
      check_method: "mcp__fetch" # 检测方法

    # 备用链接（如果主链接不可用）
    alt_url: "https://..."
    alt_url_check:
      accessible: true
      status_code: 200
      status: "可访问"
      response_time_ms: 890
      checked_at: "2025-01-22T10:30:05Z"
      check_method: "mcp__fetch"

    # 其他字段
    access_date: "2025-01-22"
    access_status: "需要注册"  # 公开/需要注册/需要付费
    verification_status: "已验证可访问"  # 更新验证状态
    reliability: "高"
    data_points: ["市场规模", "厂商排名"]
    search_method: "WebSearch"
```

#### 链接失效处理策略

```yaml
当检测到链接不可访问时:
  1. 立即丢弃该链接
     - 不将其添加到 citations
     - 记录到失效链接日志

  2. 搜索替代来源
     - 使用相同关键词重新搜索
     - 优先选择可访问的链接
     - 重新进行可访问性检测

  3. 提供备用链接
     - 如果主链接需要注册，搜索公开的摘要或报道
     - 验证备用链接的可访问性

  4. 记录处理过程
     failures:
       - url: "https://failed-url.com"
         reason: "404 Not Found"
         timestamp: "2025-01-22T10:30:00Z"
         action: "已丢弃，使用替代来源"
         alternative: "https://alternative-url.com"
```

#### 批量检测（可选）

```yaml
对于已收集的引用列表:
  场景: 技能执行结束前，批量验证所有链接

  流程:
    1. 遍历 context.citations
    2. 对每个 citation.url 进行检测
    3. 更新 url_check 字段
    4. 标记不可访问的引用
    5. 生成链接可访问性报告

  输出示例:
    ## 链接可访问性检测报告

    总引用数: 15
    可访问: 13 (86.7%)
    不可访问: 2 (13.3%)

    ### 不可访问的链接

    - [5] TechCrunch 文章
      - URL: https://techcrunch.com/2024/03/15/invalid
      - 状态: 404 Not Found
      - 检测时间: 2025-01-22T10:35:00Z
      - 处理: 已标记为失效，需要重新搜索

    - [12] Crunchbase 配置
      - URL: https://crunchbase.com/organization/invalid
      - 状态: 403 Forbidden
      - 检测时间: 2025-01-22T10:35:05Z
      - 处理: 需要注册，已使用备用链接
```

#### URLs 清单文件中的可访问性信息

```markdown
## 详细 URLs 列表

| # | 数据类型 | 来源 | URL | 可访问性 | 状态码 | 响应时间 | 访问状态 | 备用链接 |
|---|---------|------|-----|---------|--------|---------|---------|---------|
| 1 | 市场规模 | Gartner | https://... | ✅ 可访问 | 200 | 1250ms | 需要注册 | https://... |
| 2 | 增长率 | IDC | https://... | ✅ 可访问 | 200 | 890ms | 公开 | - |
| 3 | 用户数据 | Official | https://... | ❌ 404 | 404 | - | - | https://... |
| 4 | 融资信息 | CB | https://... | ⚠️ 慢 | 200 | 8500ms | 需要注册 | - |

图例:
- ✅ 可访问: HTTP 200-299，响应时间 < 5秒
- ⚠️ 慢: HTTP 200-299，响应时间 >= 5秒
- ❌ 不可访问: HTTP 400-599 或其他错误
```

#### 检测配置

```yaml
链接检测配置:
  timeout: 10秒           # 单次检测超时时间
  retry: 1次              # 超时重试次数
  retry_timeout: 20秒     # 重试超时时间
  batch_size: 5           # 批量检测并发数（避免过载）
  require_alt: true       # 需要注册的链接必须提供备用链接

失败阈值:
  max_failures: 3         # 超过此数量则停止搜索，报告错误
  failure_rate: 0.5       # 失败率超过50%则警告
```

---

### 5. 引用验证和质量标注

#### 验证状态

```yaml
验证状态分类（增强版，包含链接可访问性）:

  已验证可访问:
    - 通过链接可访问性检测（HTTP 200-299）
    - 通过 Tavily QNA 验证数据准确性
    - 通过多个来源交叉验证
    - 数据一致性 > 90%
    - **这是唯一可用于最终报告的验证状态**

  未验证:
    - 仅通过单次搜索获取
    - 未进行链接可访问性检测
    - 未进行交叉验证
    - 数据一致性未知
    - **警告：不应在最终报告中使用**

  验证中:
    - 正在进行链接可访问性检测
    - 正在进行多源验证
    - 等待第三方确认

  链接失效:
    - HTTP 404/403/500 等错误
    - 链接无法访问
    - **必须丢弃或找到替代来源**

  需要备用链接:
    - 主链接需要注册/付费
    - 未找到可访问的备用链接
    - **必须先找到备用链接才能使用**
```

#### 验证流程

```yaml
每个引用必须经过完整的验证流程:

  步骤 1: 链接可访问性检测（强制）
    - 使用 mcp__fetch__fetch 检测
    - 记录 HTTP 状态码和响应时间
    - 如果不可访问，立即丢弃或找替代来源

  步骤 2: 数据准确性验证（推荐）
    - 使用 Tavily QNA 验证关键数据
    - 与多个来源交叉验证
    - 计算数据一致性

  步骤 3: 质量标注
    - 可靠性评估（高/中/低）
    - 时效性评估（实时/近期/历史/过期）
    - 完整性评估（完整/部分/缺失）

  步骤 4: 最终验证状态
    - 所有检查通过 → "已验证可访问"
    - 部分检查通过 → "未验证"（标注原因）
    - 链接失效 → "链接失效"（必须处理）
```

#### 数据质量标注

```yaml
每个引用标注数据质量:
  可靠性: 高/中/低
  时效性: 实时/近期/历史/过期
  完整性: 完整/部分/缺失

质量评估:
  高可靠性:
    - Gartner, Forrester, IDC
    - SEC 文件
    - 公司官方数据

  中可靠性:
    - Crunchbase, PitchBook
    - TechCrunch, VentureBeat
    - 行业分析报告

  低可靠性:
    - 社交媒体
    - 个人博客
    - 未验证的第三方
```

---

### 5. 输出文件格式

#### 独立 URLs 清单文件

```markdown
文件: outputs/references/YYYY-MMDD-[topic]-urls.md

# URLs 清单: [主题]

**生成日期**: YYYY-MM-DD
**搜索日期**: YYYY-MM-DD
**总链接数**: X

---

## 可访问性汇总

| 状态 | 数量 | 百分比 |
|------|------|--------|
| 公开 | X | XX% |
| 需要注册 | X | XX% |
| 需要付费 | X | XX% |
| 链接失效 | X | XX% |

---

## 详细 URLs 列表

| # | 数据类型 | 来源 | URL | 访问状态 | 备用链接 |
|---|---------|------|-----|---------|---------|
| 1 | 市场规模 | Gartner | https://... | 需要注册 | https://... |
| 2 | 增长率 | IDC | https://... | 公开 | - |
| 3 | 用户数据 | Official | https://... | 公开 | - |

---

## 按来源分组

### 权威机构

- [1] Gartner: https://...
- [2] Forrester: https://...
- [3] IDC: https://...

### 公司官方

- [4] Notion: https://...
- [5] Confluence: https://...

### 投融资

- [6] Crunchbase: https://...
- [7] PitchBook: https://...

### 媒体

- [8] TechCrunch: https://...
- [9] VentureBeat: https://...

---

*本文件由 Citation Manager 自动生成*
```

---

## 使用示例

### 示例 1: 在 research-assistant 中使用

```yaml
技能: research-assistant

执行流程:
  1. 搜索 Gartner 报告
     → 收集到引用[1]: Gartner Magic Quadrant 2024

  2. 搜索 IDC 报告
     → 收集到引用[2]: IDC MarketScape 2024

  3. 生成报告
     → 在"市场规模"章节: "$42.5 亿 [Gartner 2024]¹"
     → 在"增长率"章节: "18% CAGR [IDC 2024]²"

  4. 生成参考文献
     → 报告末尾添加完整参考文献章节

  5. 输出 URLs 清单
     → outputs/references/2025-0122-cloud-security-urls.md
```

### 示例 2: 在 jtbd-analyzer 中使用

```yaml
技能: jtbd-analyzer

输入: 包含 citations 的上下文
  context.citations: [来自 research-assistant 的引用]

执行流程:
  1. 如果需要搜索补充数据
     → 使用 Citation Manager 添加新引用

  2. 使用已有引用
     → 在用户画像中引用市场数据: [Gartner 2024]¹

  3. 更新引用列表
     → 合并新旧引用，重新编号

  4. 传递给下一个技能
     → context.citations: [完整的引用列表]
```

### 示例 3: 在 prd-generator 中汇总

```yaml
技能: prd-generator

输入: 包含所有引用的上下文
  context.citations: [来自所有前置技能的引用]

执行流程:
  1. 收集所有技能的引用
  2. 去重（相同 URL 只保留一个）
  3. 重新按使用顺序编号
  4. 在 PRD 末尾生成完整的参考文献章节
  5. 输出独立的 URLs 清单文件
```

---

## 最佳实践

✅ **DO**:
- 每次搜索都记录完整的引用信息
- **必须对每个链接进行可访问性检测**
- 使用一致的引用格式
- 提供备用链接（当主链接需要注册时）
- 标注验证状态和数据质量
- 定期验证链接可访问性
- 丢弃不可访问的链接并搜索替代来源
- 在 URLs 清单中包含可访问性信息

❌ **DON'T**:
- 只记录 URL 不记录其他信息
- **跳过链接可访问性检测**
- 混用不同的引用格式
- 忽略数据来源的可靠性
- 不标注验证状态
- **使用 404、403、500 等失效链接**
- 在最终报告中使用"未验证"或"链接失效"的引用
- 忽略链接检测失败

---

## 集成点

此组件被以下技能使用：
- **research-assistant**: 主要引用收集者
- **jtbd-analyzer**: 使用和扩展引用
- **threat-modeling**: 可能需要行业威胁数据引用
- **forecast-engine**: 使用市场数据引用
- **analytics-engine**: 使用数据引用
- **prd-generator**: 汇总所有引用
- **document-engine**: 格式化引用章节

---

## 技术实现说明

### 引用存储结构

```yaml
context.citations:
  - id: 1                    # 引用编号（从1开始）
    source: "Gartner"        # 来源名称
    source_type: "权威机构"  # 来源类型
    year: 2024               # 年份
    title: "完整标题"
    url: "https://..."

    # 链接可访问性检测（强制）
    url_check:
      accessible: true          # 是否可访问
      status_code: 200          # HTTP 状态码
      status: "可访问"          # 状态描述
      response_time_ms: 1250    # 响应时间
      content_type: "text/html" # 内容类型
      checked_at: "2025-01-22T10:30:00Z"  # 检测时间
      check_method: "mcp__fetch" # 检测方法

    alt_url: "https://..."   # 备用链接（可选）
    alt_url_check:           # 备用链接检测（如果有）
      accessible: true
      status_code: 200
      status: "可访问"
      response_time_ms: 890
      checked_at: "2025-01-22T10:30:05Z"
      check_method: "mcp__fetch"

    publication_date: "2024-06"
    access_date: "2025-01-22"
    access_status: "需要注册" # 公开/需要注册/需要付费
    verification_status: "已验证可访问"  # 更新：包含链接检测
    reliability: "高"        # 高/中/低
    data_points:             # 该引用提供的数据
      - "市场规模"
      - "厂商排名"
    search_method: "WebSearch"
    used_in:                 # 使用位置（可选）
      - "市场概览/市场规模"
      - "竞争分析/厂商排名"

  citation_counter: 5        # 下一个引用的编号
```

### 引用函数

```python
def get_next_citation_number(context):
    """获取下一个引用编号"""
    return context.get('citation_counter', 1)

def add_citation(context, citation_data):
    """添加新引用并返回引用编号

    重要: 添加前必须验证链接可访问性
    """
    # 检查链接可访问性
    url_check = check_url_accessibility(citation_data['url'])

    # 如果链接不可访问，尝试处理
    if not url_check['accessible']:
        # 记录失败
        log_failure(citation_data['url'], url_check)

        # 尝试搜索替代来源
        alternative = find_alternative_source(citation_data)
        if alternative:
            citation_data['url'] = alternative['url']
            citation_data['alt_url'] = alternative.get('alt_url')
            url_check = check_url_accessibility(citation_data['url'])
        else:
            # 找不到替代来源，拒绝添加
            raise ValueError(f"链接不可访问且无替代来源: {citation_data['url']}")

    # 添加检测信息到引用数据
    citation_data['url_check'] = url_check

    # 如果有备用链接，也进行检测
    if 'alt_url' in citation_data:
        alt_check = check_url_accessibility(citation_data['alt_url'])
        citation_data['alt_url_check'] = alt_check

    # 添加引用
    citation_id = get_next_citation_number(context)
    citation_data['id'] = citation_id
    citation_data['verification_status'] = '已验证可访问' if url_check['accessible'] else '链接失效'

    context['citations'].append(citation_data)
    context['citation_counter'] = citation_id + 1

    return citation_id

def check_url_accessibility(url, timeout=10):
    """检测链接可访问性

    返回:
        {
            'accessible': bool,
            'status_code': int,
            'status': str,
            'response_time_ms': int,
            'content_type': str,
            'checked_at': str (ISO 8601),
            'check_method': str
        }
    """
    from datetime import datetime
    import time

    start_time = time.time()
    checked_at = datetime.utcnow().isoformat() + 'Z'

    try:
        # 使用 mcp__fetch 检测
        response = mcp__fetch__fetch(
            url=url,
            max_length=1000,  # 只检测头部
            timeout=timeout
        )

        response_time_ms = int((time.time() - start_time) * 1000)

        return {
            'accessible': True,
            'status_code': 200,
            'status': '可访问',
            'response_time_ms': response_time_ms,
            'content_type': 'text/html',
            'checked_at': checked_at,
            'check_method': 'mcp__fetch'
        }

    except TimeoutError:
        # 超时：重试一次
        try:
            response = mcp__fetch__fetch(url=url, timeout=timeout*2)
            response_time_ms = int((time.time() - start_time) * 1000)
            return {
                'accessible': True,
                'status_code': 200,
                'status': '可访问(慢)',
                'response_time_ms': response_time_ms,
                'content_type': 'text/html',
                'checked_at': checked_at,
                'check_method': 'mcp__fetch'
            }
        except:
            return {
                'accessible': False,
                'status_code': 0,
                'status': '超时',
                'response_time_ms': timeout * 1000,
                'content_type': None,
                'checked_at': checked_at,
                'check_method': 'mcp__fetch',
                'error': '连接超时'
            }

    except HTTPError as e:
        response_time_ms = int((time.time() - start_time) * 1000)
        status_code = getattr(e, 'status_code', 0)

        if status_code == 404:
            status = '404 Not Found'
        elif status_code == 403:
            status = '403 Forbidden'
        elif status_code >= 500:
            status = f'{status_code} Server Error'
        else:
            status = f'HTTP {status_code}'

        return {
            'accessible': False,
            'status_code': status_code,
            'status': status,
            'response_time_ms': response_time_ms,
            'content_type': None,
            'checked_at': checked_at,
            'check_method': 'mcp__fetch',
            'error': str(e)
        }

    except Exception as e:
        response_time_ms = int((time.time() - start_time) * 1000)
        return {
            'accessible': False,
            'status_code': 0,
            'status': '网络错误',
            'response_time_ms': response_time_ms,
            'content_type': None,
            'checked_at': checked_at,
            'check_method': 'mcp__fetch',
            'error': str(e)
        }

def find_alternative_source(citation_data):
    """为失效的链接搜索替代来源

    返回:
        {
            'url': 'https://alternative-url.com',
            'alt_url': 'https://another-alternative.com' (可选)
        }
        或 None (如果找不到替代来源)
    """
    # 使用相同关键词重新搜索
    query = f"{citation_data['source']} {citation_data['title']}"

    try:
        results = WebSearch(query)

        # 过滤可访问的链接
        for result in results[:5]:  # 检查前5个结果
            url_check = check_url_accessibility(result['url'])
            if url_check['accessible']:
                return {'url': result['url']}

        return None

    except Exception as e:
        # 搜索失败，记录错误
        log_error(f"搜索替代来源失败: {e}")
        return None

def format_citation_reference(citation):
    """格式化引用标注"""
    return f"[{citation['source']} {citation['year']}]"
```

---

*此文档是 Oh-My-PM-Skills 技能系统的共享组件*
*版本: 1.0.0 | 最后更新: 2025-01-22*
