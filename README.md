## 🚀 Way to AIC | 通往 AI 电商之路
---
### 🌐 官网 Website
- https://waytoaic.com  
- https://www.waytoaic.com  
---

### 👥 社群招募 Community
`Way to AIC 社群招募 | WaytoAIC.com`

<p align="center">
  <img src="https://github.com/user-attachments/assets/d9f8bbf4-2056-4780-975d-86c885b52bab" width="70%">
</p>

---

### 📣 公众号 WeChat Official Account
`维正 WaytoAIC`

<p align="center">
  <img src="https://github.com/user-attachments/assets/71c71a5c-e68a-4f30-9afb-f2b056619991" width="300">
</p>

---

### 🧠 知识星球 Xiaozhixing
`AI电商之路 WaytoAIC`

<p align="center">
  <img src="https://github.com/user-attachments/assets/9eccef07-0e84-45a7-a415-affcb18c928d" width="200">
  <img src="https://github.com/user-attachments/assets/4e99fbc3-1981-4fee-b113-c9821141102d" width="400">
</p>

---

### 🧩 About Way to AIC

**AIC = AI Commerce**

在 AI 重塑商业的时代，我们希望和每一个拥抱 AI 的卖家：

- 找到场景  
- 定义问题  
- 积累能力  
- 设计系统  

共同通往 AI 电商之路。

> Way to AIC 不是教学，不是工具，  
> 而是一条所有电商人共同走的进化之路。

### WaytoAIC 理念 | Principles

| 中文 | English |
|---|---|
| 场景先于方法 | Context before method |
| AI 的价值来自真实业务场景，而不是技术本身。 | AI creates value through real business contexts, not through technology alone. |
| 问题先于答案 | Problem before answer |
| 定义问题，比拥有工具更重要。 | Defining the problem matters more than collecting tools. |
| 系统胜过技巧 | System over tricks |
| 技巧是术，系统才是道，决定卖家的上限。 | Tricks are tactical; systems define long-term leverage and ceiling. |
| 共创优于独行 | Co-creation over solo progress |
| 我们相信，真正的进化发生在共同探索的过程中。 | Real evolution happens through shared exploration. |

# SIF MCP Skills

一组面向 Amazon 运营分析的 SIF MCP skills，覆盖流量诊断、关键词研究、广告结构分析，以及跨域路由。

This repository packages a small skill bundle for SIF MCP based Amazon analysis in Codex and OpenClaw. It focuses on traffic diagnosis, keyword research, ad structure analysis, and routing complex requests to the right tool domain.

## Quick Install

直接安装整套 skill：

```bash
curl -fsSL https://raw.githubusercontent.com/WaytoAIC/sif-mcp-skills/main/install.sh | bash
```

指定安装到 Codex 或 OpenClaw：

```bash
curl -fsSL https://raw.githubusercontent.com/WaytoAIC/sif-mcp-skills/main/install.sh | bash -s -- --target codex
curl -fsSL https://raw.githubusercontent.com/WaytoAIC/sif-mcp-skills/main/install.sh | bash -s -- --target openclaw
```

指定版本或分支：

```bash
curl -fsSL https://raw.githubusercontent.com/WaytoAIC/sif-mcp-skills/main/install.sh | bash -s -- --ref v1.0.1
```

## Included Skills

- `sif-mcp-router`: Route ambiguous SIF analysis requests to the right domain
- `sif-traffic-diagnosis`: Diagnose traffic changes and sales impact
- `sif-keyword-research`: Research keyword demand, trend, and ASIN keyword signals
- `sif-ad-analysis`: Analyze ad structure, contribution, and performance shifts

详细调用说明见 [SKILLS.md](./SKILLS.md)。

## Repo Structure

```text
.
├── install.sh
├── README.md
├── SKILLS.md
└── skills/
    ├── sif-ad-analysis/
    ├── sif-keyword-research/
    ├── sif-mcp-router/
    └── sif-traffic-diagnosis/
```

## When To Use Which Skill

- 你只知道要“查 SIF 数据”，先用 `sif-mcp-router`
- 你要看流量涨跌、结构变化、销量传导，用 `sif-traffic-diagnosis`
- 你要研究关键词价值或 ASIN 吃词，用 `sif-keyword-research`
- 你要拆 Campaign / Ad Group 结构，用 `sif-ad-analysis`

## SIF MCP 使用手册

适用对象：已经接入 `https://mcp.sif.com` 提供的 SIF MCP 服务，准备在 Codex / OpenClaw / Claude Code 里稳定做 Amazon 数据分析的人。

这份手册只回答 3 件事：

- 装好 MCP 之后怎么确认它真的可用
- 不同分析问题该走哪个 SIF 工具域
- 怎么配合本仓库里的 skill，把常见任务问得更稳

`skills` 的调用方法见 [SKILLS.md](./SKILLS.md)。

## 1. 这套 SIF MCP 能解决什么问题

按当前仓库已覆盖的能力，可以把 SIF MCP 理解成 5 个域：

- 异常诊断：突然跌了，先找根因
- 流量与销量：最近到底涨了还是跌了，是否已经影响业务结果
- ASIN 吃词：一个 ASIN 靠哪些关键词在带量
- 关键词研究：一个词值不值得继续打
- 广告结构：广告预算花到了哪里，谁在带量，谁在拖后腿

一句话路由：

- 你关心“最近发生了什么”，优先看流量 / 销量
- 你关心“为什么突然变差”，优先看异常诊断
- 你关心“ASIN 靠什么词”，优先看反查关键词
- 你关心“这个词值不值得做”，优先看关键词研究
- 你关心“广告谁有效谁低效”，优先看广告结构

## 2. 装好后先验证什么

你已经装好 MCP，接下来不要直接上复杂任务，先做最小验证。

### 2.1 健康检查

先确认 MCP 服务能通：

- `ping`

预期：

- 能返回 `pong` 和时间戳，说明通道没问题

### 2.2 目录检查

再确认当前会话能看到 SIF 工具目录：

- `sif_catalog`

预期：

- 能列出流量、关键词、广告、异常诊断等工具

### 2.3 真实问题检查

最后跑一个真实但简单的问题，确认分析链能通。

推荐验证题：

```text
请使用 analyze_traffic_anomaly，
诊断 ASIN B0XXXXXXX 最近 4 周流量下跌的根因，
区分广告侧、自然侧和复合型问题。
```

如果这一步能跑通，后面再扩展到关键词和广告分析。

## 3. 在 Codex 里怎么提问最稳

SIF MCP 不适合“帮我分析一下”这种空话。对象越清楚，结果越稳。

建议每次至少补齐下面 4 个要素：

- 对象：`ASIN`、`Listing`、`关键词`
- 时间：最近 7 天、最近 4 周、本月、对比上月
- 目标：诊断、比较、复盘、找机会、拆结构
- 输出：结论、证据、动作建议

推荐句式：

```text
帮我分析 ASIN B0XXXXXXX 最近 4 周的自然流量变化，
判断是结构问题、关键词丢失，还是广告带量变弱，
最后给我 3 条本周优先动作。
```

```text
帮我判断关键词 "wireless earbuds" 现在是否值得继续重点投入，
看需求阶段、历史趋势、词根趋势和竞争强度，
最后直接给结论和风险。
```

```text
帮我拆 ASIN B0XXXXXXX 最近 30 天的广告结构，
从 ASIN、Campaign、Ad Group 三层看谁在带量、谁在掉量，
并给出保留、放大、收缩三类动作。
```

## 4. 问题类型怎么路由到工具域

### 4.1 异常诊断

适合问题：

- 上周流量为什么突然掉了
- 这次下跌主要是广告问题还是自然问题
- 有没有复合型异常

优先工具：

- `analyze_traffic_anomaly`

关键要求：

- 在任务描述里直接写出工具名 `analyze_traffic_anomaly`，触发更稳

### 4.2 流量与销量

适合问题：

- 最近流量为什么跌了
- 自然流和广告流的占比怎么变了
- 流量波动有没有传导到销量
- 这个 ASIN 最近表现是涨还是跌

优先工具：

- `ops_get_asin_traffic_trend`
- `ops_get_asin_traffic_trend_detail`
- `ops_get_listing_traffic_overview`
- `ops_get_listing_traffic_structure`
- `ops_get_asin_sales_trend`
- `ops_get_asin_sales_list`

### 4.3 ASIN 反查关键词

适合问题：

- 这个 ASIN 主要吃哪些词
- 哪些关键词真的在带流量
- 它在核心词上的竞争位置怎么样

优先工具：

- `ops_get_listing_keyword_distribution`
- `market_get_asin_keyword_signals`

### 4.4 关键词研究

适合问题：

- 这个词是不是还在增长
- 这个词处于什么需求阶段
- 竞争是不是太挤
- 词根和精确词哪个更值得投入

优先工具：

- `market_get_keyword_demand`
- `market_get_keyword_history`
- `market_get_keyword_root_trend`
- `market_get_keyword_competition`

注意：

- `market_get_keyword_demand` 当前只支持美国站

### 4.5 广告结构

适合问题：

- 广告结构是不是太散
- 哪个 Campaign 在带量
- 哪个 Ad Group 在浪费预算
- 最近广告打法是否发生变化

优先工具：

- `ads_get_asin_ad_structure`
- `ads_get_asin_ad_traffic_trend`
- `ads_get_asin_ad_feature_profile`
- `ads_get_asin_ad_historical_feature_profile`
- `ads_get_asin_ad_window_feature_profile`
- `ads_get_asin_campaign_contribution_overview`
- `ads_get_asin_campaign_changes`
- `ads_get_campaign_structure`
- `ads_get_campaign_traffic_trend`
- `ads_get_campaign_contribution_breakdown`
- `ads_get_ad_group_traffic_trend`
- `ads_get_ad_group_keyword_breakdown`

## 5. 推荐的分析顺序

不要一开始把所有工具都打一遍。更稳的方式是先拿第一层结论，再决定要不要下钻。

### 5.1 当问题是“为什么跌了”

推荐顺序：

1. `analyze_traffic_anomaly`
2. `ops_get_asin_traffic_trend`
3. `ops_get_listing_traffic_structure`
4. 必要时再补 `ops_get_asin_sales_trend`

### 5.2 当问题是“这个词值不值得做”

推荐顺序：

1. `market_get_keyword_demand`
2. `market_get_keyword_history`
3. `market_get_keyword_root_trend`
4. `market_get_keyword_competition`

### 5.3 当问题是“广告谁在带量”

推荐顺序：

1. `ads_get_asin_ad_structure`
2. `ads_get_asin_campaign_contribution_overview`
3. `ads_get_campaign_contribution_breakdown`
4. 必要时再下钻 `ads_get_ad_group_keyword_breakdown`

## 6. 可直接复制的问法模板

### 模板 A：流量下跌诊断

```text
请使用 analyze_traffic_anomaly，
帮我诊断 ASIN B0XXXXXXX 最近 4 周流量下跌的根因。
需要区分广告侧、自然侧、复合型，
并给出证据链和本周优先动作。
```

### 模板 B：ASIN 流量结构复盘

```text
帮我分析 ASIN B0XXXXXXX 最近一个月的流量趋势和流量结构，
看自然流、广告流、品牌流各自怎么变了，
并判断变化是否已经影响销量。
```

### 模板 C：关键词是否值得打

```text
帮我研究关键词 "wireless earbuds"，
看需求生命周期、历史趋势、词根趋势和竞争格局，
最后直接回答：现在值不值得继续重点投入。
```

### 模板 D：竞品吃词分析

```text
帮我反查 ASIN B0XXXXXXX 的核心流量词，
看哪些词在带量、它在这些词上的竞争位置如何，
最后给我 5 个最值得持续跟踪的词。
```

### 模板 E：广告结构拆解

```text
帮我拆 ASIN B0XXXXXXX 最近 30 天的广告结构，
从 ASIN、Campaign、Ad Group 三层看：
1. 谁在带量
2. 谁在掉量
3. 哪些结构需要合并、停投或单独观察
```

## 7. 建议模型按什么格式输出

如果你要的是“可执行结论”，建议直接在问题里要求按下面格式返回：

```text
1. 结论
2. 关键证据
3. 根因判断或机会判断
4. 本周优先动作
5. 还需要补查什么
```

团队复盘时可以再加：

```text
6. 风险提醒
7. 下一轮监控指标
```

## 8. 本仓库附带了哪些 skills

本仓库已经包含 4 个可复用 skill：

- `skills/sif-mcp-router`
- `skills/sif-traffic-diagnosis`
- `skills/sif-keyword-research`
- `skills/sif-ad-analysis`

推荐使用方式：

- 先用 `sif-mcp-router` 作为总入口
- 想让触发更稳，再显式使用对应的子 skill
- 只做单一问题时，优先直接点名子 skill，少走弯路

具体调用方式见 [SKILLS.md](./SKILLS.md)。

## 9. 如何把这些 skills 安装到 Codex

如果你想把这些 skill 挂到本机 `~/.codex/skills`，在本仓库根目录执行：

```bash
mkdir -p ~/.codex/skills
ln -s "$(pwd)/skills/sif-mcp-router" ~/.codex/skills/sif-mcp-router
ln -s "$(pwd)/skills/sif-traffic-diagnosis" ~/.codex/skills/sif-traffic-diagnosis
ln -s "$(pwd)/skills/sif-keyword-research" ~/.codex/skills/sif-keyword-research
ln -s "$(pwd)/skills/sif-ad-analysis" ~/.codex/skills/sif-ad-analysis
```

重开 Codex 会话后，可以用两种方式触发：

- 在问题里自然描述任务，命中对应 skill
- 直接点名 skill 名称，例如 `请使用 sif-ad-analysis`

## 10. 常见误区

- 只说“帮我分析一下”，但不带 ASIN / 关键词
- 一次塞进太多目标，既要流量又要广告又要竞品又要选词
- 不写时间范围，导致口径漂移
- 做异常诊断时没有明确写出 `analyze_traffic_anomaly`
- 研究关键词需求时忘了 `market_get_keyword_demand` 目前是美国站限定

## 11. 一个最小可用工作流

如果你今天就要开始用，直接按这个顺序：

1. 用 `ping` 确认 SIF MCP 通
2. 用 `sif_catalog` 看目录是否完整
3. 跑一条异常诊断模板验证分析链
4. 把 `skills` 软链接到 `~/.codex/skills`
5. 后续按任务类型选择 `sif-mcp-router` 或对应子 skill
