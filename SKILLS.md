# SIF Skills 调用说明

这份文档专门回答一件事：装好 SIF MCP 之后，怎么在 Codex 里稳定触发本仓库附带的 4 个 skill。

## 1. 当前有哪些 skill

本仓库包含：

- `sif-mcp-router`
- `sif-traffic-diagnosis`
- `sif-keyword-research`
- `sif-ad-analysis`

角色分工：

- `sif-mcp-router`：总入口，先判断该走哪个工具域
- `sif-traffic-diagnosis`：只处理流量、结构、销量传导
- `sif-keyword-research`：只处理关键词研究和 ASIN 吃词
- `sif-ad-analysis`：只处理广告结构和分层贡献

## 2. 先安装，再谈调用

如果这些 skill 还没挂到 `~/.codex/skills`，先做软链接：

```bash
mkdir -p ~/.codex/skills
ln -s /Users/wesleyzane/Desktop/Codex/Sif/skills/sif-mcp-router ~/.codex/skills/sif-mcp-router
ln -s /Users/wesleyzane/Desktop/Codex/Sif/skills/sif-traffic-diagnosis ~/.codex/skills/sif-traffic-diagnosis
ln -s /Users/wesleyzane/Desktop/Codex/Sif/skills/sif-keyword-research ~/.codex/skills/sif-keyword-research
ln -s /Users/wesleyzane/Desktop/Codex/Sif/skills/sif-ad-analysis ~/.codex/skills/sif-ad-analysis
```

重开 Codex 会话后再测试触发。

## 3. skill 有两种触发方式

### 3.1 自然触发

你不写 skill 名，直接把任务描述清楚，Codex 也可能命中对应 skill。

例如：

```text
帮我分析 ASIN B0XXXXXXX 最近 4 周的流量结构变化，
看自然流和广告流哪个掉得更多，
并判断是否已经影响销量。
```

这类问题通常会命中 `sif-traffic-diagnosis`。

### 3.2 显式点名

如果你想让触发更稳，直接点名 skill。

例如：

```text
请使用 sif-keyword-research，
帮我判断关键词 "wireless earbuds" 现在是否值得继续重点投入。
```

这是最稳的方式，尤其适合复杂任务或多轮会话。

## 4. 什么时候用哪个 skill

### 4.1 `sif-mcp-router`

适合：

- 你只知道自己要“查 SIF 数据”，但还没决定走哪个工具域
- 你要跨域判断，例如“流量跌了，到底是关键词问题还是广告问题”
- 你想先做一轮路由，再决定是否深挖

推荐问法：

```text
请使用 sif-mcp-router，
帮我判断 ASIN B0XXXXXXX 最近 4 周的表现问题应该先从流量、关键词还是广告域切入，
并按最小工具组合给出分析结果。
```

### 4.2 `sif-traffic-diagnosis`

适合：

- 流量为什么跌了
- 哪个流量渠道掉得最明显
- 流量变化有没有传导到销量
- 需要复盘最近 2 到 8 周趋势

推荐问法：

```text
请使用 sif-traffic-diagnosis，
分析 ASIN B0XXXXXXX 最近 4 周流量趋势和流量结构，
判断自然流、广告流、品牌流分别发生了什么变化，
并说明是否已经影响销量。
```

如果要根因诊断，建议同时把工具名写进去：

```text
请使用 sif-traffic-diagnosis，
并调用 analyze_traffic_anomaly，
诊断 ASIN B0XXXXXXX 最近 4 周流量下跌的根因。
```

### 4.3 `sif-keyword-research`

适合：

- 一个关键词值不值得继续做
- 关键词处于什么需求阶段
- 词根趋势和精确词趋势怎么变化
- 一个 ASIN 靠哪些关键词在带量

推荐问法 1：

```text
请使用 sif-keyword-research，
研究关键词 "wireless earbuds"，
覆盖需求阶段、历史趋势、词根趋势和竞争格局，
最后直接回答现在值不值得继续重点投入。
```

推荐问法 2：

```text
请使用 sif-keyword-research，
反查 ASIN B0XXXXXXX 的核心流量词，
看哪些词在带量、哪些词更值得持续跟踪。
```

注意：

- `market_get_keyword_demand` 当前只支持美国站，所以研究需求强度时最好明确 `US`

### 4.4 `sif-ad-analysis`

适合：

- 广告结构复盘
- 哪个 Campaign 在带量
- 哪个 Campaign / Ad Group 在拖后腿
- 最近广告打法是不是变了

推荐问法：

```text
请使用 sif-ad-analysis，
拆解 ASIN B0XXXXXXX 最近 30 天的广告结构，
从 ASIN、Campaign、Ad Group 三层看谁在带量、谁在掉量，
最后给我保留、放大、收缩三类动作建议。
```

如果你已经知道某个 `campaignId`，可以继续追问：

```text
继续使用 sif-ad-analysis，
下钻 campaignId=SUBD，
看哪个 Ad Group 和关键词在驱动变化。
```

## 5. 推荐的调用策略

### 5.1 先总入口，再子 skill

适合复杂问题：

1. 先用 `sif-mcp-router`
2. 让它判断该走哪个域
3. 再明确切到子 skill 深挖

### 5.2 直接点名子 skill

适合单一问题：

- 流量问题直接用 `sif-traffic-diagnosis`
- 关键词问题直接用 `sif-keyword-research`
- 广告问题直接用 `sif-ad-analysis`

这样比“一个 prompt 里塞全部诉求”更稳。

## 6. 推荐你在 prompt 里补哪些字段

为了让 skill 路由和工具调用更准，建议 prompt 里补齐这些信息：

- 对象：`ASIN`、`关键词`
- 站点：如 `US`
- 时间：最近 7 天、最近 4 周、最近 30 天
- 目标：诊断、复盘、找机会、拆结构
- 输出：结论、证据、动作建议

高质量示例：

```text
请使用 sif-ad-analysis，
分析 US 站 ASIN B0XXXXXXX 最近 30 天广告结构，
目标是找出带量 Campaign、掉量 Campaign 和低效 Ad Group，
输出结论、证据和本周动作建议。
```

## 7. 多轮会话怎么接着问

第一轮拿结论，第二轮再下钻，不要第一轮就把问题写爆。

推荐方式：

1. 第一轮：

```text
请使用 sif-mcp-router，
看 ASIN B0XXXXXXX 最近 4 周表现变差的主要问题落在哪个域。
```

2. 第二轮：

```text
继续使用 sif-traffic-diagnosis，
把最近 4 周自然流和广告流拆开讲，
并结合销量趋势判断影响程度。
```

3. 第三轮：

```text
继续使用 sif-ad-analysis，
重点下钻掉量最大的 Campaign。
```

## 8. 常见失败写法

- “帮我看一下这个产品”
- “帮我分析最近情况”
- “把流量、广告、竞品、关键词、利润一起看一下”
- 不写 `ASIN`
- 不写时间范围
- 做异常诊断时不写 `analyze_traffic_anomaly`

这些写法最大的问题不是“模型看不懂”，而是工具路由会飘。

## 9. 最小可复制 prompt 清单

### 路由入口

```text
请使用 sif-mcp-router，
帮我判断 ASIN B0XXXXXXX 最近 4 周的问题应该先从哪个 SIF 工具域切入，
并给出最小分析路径。
```

### 流量诊断

```text
请使用 sif-traffic-diagnosis，
并调用 analyze_traffic_anomaly，
诊断 ASIN B0XXXXXXX 最近 4 周流量下跌的根因，
并结合销量趋势给出本周动作。
```

### 关键词研究

```text
请使用 sif-keyword-research，
研究关键词 "wireless earbuds" 在 US 站的需求、趋势和竞争，
最后直接回答值不值得继续重点投入。
```

### ASIN 吃词

```text
请使用 sif-keyword-research，
反查 ASIN B0XXXXXXX 的核心流量词，
找出最值得持续跟踪的 5 个词。
```

### 广告结构

```text
请使用 sif-ad-analysis，
拆解 ASIN B0XXXXXXX 最近 30 天的广告结构，
看谁在带量、谁在掉量、谁需要停投或收缩。
```
