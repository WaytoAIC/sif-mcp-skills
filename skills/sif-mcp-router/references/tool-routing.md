# SIF MCP 路由参考

## 场景到工具的映射

### 流量诊断

- 先看趋势：`ops_get_asin_traffic_trend`
- 再看拆分：`ops_get_asin_traffic_trend_detail`
- 再看全景 / 结构：`ops_get_listing_traffic_overview`、`ops_get_listing_traffic_structure`
- 如需判断业务结果是否已受影响：`ops_get_asin_sales_trend`

### ASIN 吃词分析

- 看词占比：`ops_get_listing_keyword_distribution`
- 看关键词上的排名与竞争位置：`market_get_asin_keyword_signals`

### 关键词是否值得做

- 看需求生命周期：`market_get_keyword_demand`
- 看历史数据：`market_get_keyword_history`
- 看词根与精确词的边界：`market_get_keyword_root_trend`
- 看竞争格局：`market_get_keyword_competition`

### 广告结构复盘

- ASIN 层：`ads_get_asin_ad_structure`、`ads_get_asin_ad_traffic_trend`
- ASIN 贡献层：`ads_get_asin_campaign_contribution_overview`
- Campaign 层：`ads_get_campaign_structure`、`ads_get_campaign_contribution_breakdown`
- Ad Group 层：`ads_get_ad_group_traffic_trend`、`ads_get_ad_group_keyword_breakdown`

### 突发异常

- 直接诊断：`analyze_traffic_anomaly`
- 注意在任务描述里写出工具名 `analyze_traffic_anomaly`

## 推荐问法

```text
帮我分析 ASIN B0XXXXXXX 最近 4 周的流量趋势，
并判断自然流、广告流、品牌流分别发生了什么变化。
```

```text
请使用 analyze_traffic_anomaly，
诊断 ASIN B0XXXXXXX 最近 4 周流量下跌的根因，
区分广告侧、自然侧和复合型问题。
```

```text
帮我判断关键词 "wireless earbuds" 是否值得继续重点投入，
需要覆盖需求阶段、历史趋势、词根趋势和竞争格局。
```

```text
帮我拆 ASIN B0XXXXXXX 最近 30 天广告结构，
看哪个 Campaign 带量最多，哪个 Ad Group 在拖后腿。
```
