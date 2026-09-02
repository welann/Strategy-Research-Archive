# Boywus：用 trade feed 提前重建 shadow orderbook

- Author: @Boywus (Boywus)
- Published: 2026-09-02 22:14
- Status URL: https://x.com/Boywus/status/2095153506823074008?s=20
- Source Type: X long post
- Capture Tool: twitter-cli
- Capture Note: 原帖无配图、无外链。`twitter-cli` 同次返回中包含若干非相关推荐推文，本归档正文只保留主帖和与正文有关的回复；非相关条目在 `meta.json` 中说明。

## 主帖正文

讲一个在 `@RobinhoodCrypto` 的 `@Lighter_xyz` 上的技巧，能比别人更快处理行情，理论上也可以延升到其他交易所。

按照文档描述，一次 orderbook 的推送是 50ms，实测下来，中位数是接近的，一次更新会把上一次推送之后的所有变化合成一个 delta 信息推送给你。

但是这样子其实你是慢一些的，因为算上网络波动，p90 下来，已经大于 50ms 不少了，这个时候如果有大哥在进行大金额吃单，orderbook 其实可能已经被吃出 skew 了，你都还不知道。

技巧就是订阅 trade，一个 trade 帧里面有 trades 数据，是比 orderbook 先到达的，你可以做一个预测性质的 shadow orderbook，根据刚刚的 trades 信息，自己提前分析出情况，不等官方的 snapshot，变相的比别人快几十 ms。

本质上就是利用不同 market data channel 的更新频率差，拿 execution feed 去提前预测市场情况。

## 评论区关键补充

### 1. 本地重构状态可以迁移到 Uniswap V3 / V4

`@ZeoMEV` 回复：

根据订单流重建 orderbook 的思路还真是很多地方都能用上，univ3/v4 的本地模拟也是靠 swap 重构 tick 信息。

### 2. 作者回复

`@Boywus` 回复 `@ZeoMEV`：

还是你们搞 LP 的更敏感些。
