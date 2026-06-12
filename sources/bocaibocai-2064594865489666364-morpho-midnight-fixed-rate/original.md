# 原文归档：bocaibocai Morpho Midnight 固定利率协议

## 主帖

- 作者：`@bocaibocai_`（菠菜菠菜｜bocaibocai）
- 原文链接：`https://x.com/bocaibocai_/status/2064594865489666364?s=20`
- 标准链接：`https://x.com/bocaibocai_/status/2064594865489666364`
- X Article：`http://x.com/i/article/2059941028120150016`
- 文章标题：`一文读懂 Morpho Midnight：当链上借贷遇上固定利率与定期市场`
- 发布时间：`2026-06-10 14:25`（Asia/Shanghai）
- 抓取时间：`2026-06-12`
- 完整文章归档：`article.md`
- 是否有配图：无

主帖仅包含 X Article 链接，完整正文已通过 `twitter article --markdown` 保存至 `article.md`。

## 文章结构

原文依次讨论：

1. `Midnight` 的定位；
2. 从 `Aave / Compound` 到 `Morpho Blue` 再到 `Midnight` 的演化；
3. 固定利率与固定到期的动机；
4. 信用凭证、债务凭证与零息折价定价；
5. `Offer / Ratifier / Maker callback / Consumption group / Merkle root`；
6. 链下路由与利率 tick；
7. 定期市场的清算和坏账记账；
8. `Enter gate / Liquidator gate` 与粗粒度授权；
9. 结算费、持续费及其对 RWA、Curator 和机构信贷的意义。

## 关键回复

### 上线时间

- 问：`那么~啥时候能用呢`
- 作者回复：`很快～`

### 与既有固定收益协议的关系

评论区有人质疑“这不就是 Pendle”，也有人补充 `Fira Lend` 同样提供固定利率市场。

这些评论说明：固定利率、定期和零息式定价本身并不是全新概念。分析 `Midnight` 时，应重点比较其抵押借贷、报价、资本调用、路由和清算结构，而不是把“固定利率”本身当作创新。

