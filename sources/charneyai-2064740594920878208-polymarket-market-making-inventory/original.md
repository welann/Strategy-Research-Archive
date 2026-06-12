# 原文归档：CharneyAI Polymarket 双边做市与库存管理

## 主帖

- 作者：`@CharneyAI`（Charney Chen）
- 原文链接：`https://x.com/charneyai/status/2064740594920878208?s=52`
- 标准链接：`https://x.com/CharneyAI/status/2064740594920878208`
- X Article：`http://x.com/i/article/2064734206341582849`
- 文章标题：`3-Polymarket 做市实录:吃单套利死于手续费之后,我转向了双边做市`
- 发布时间：`2026-06-11 00:04`（Asia/Shanghai）
- 抓取时间：`2026-06-12`
- 完整文章归档：`article.md`
- 是否有配图：无

主帖仅包含 X Article 链接，完整正文已通过 `twitter article --markdown` 保存至 `article.md`。

## 文章结构

原文主要讨论：

1. 作者此前在 Polymarket BTC 15 分钟涨跌市场做吃单套利，因为多腿没有原子成交而裸腿亏损约 `800 USDC`；
2. 短周期市场对吃单套利不友好，却可能因为换手率高而适合 maker 双边做市；
3. 用 `UP_WAC + DOWN_WAC < 1` 判断等量配平库存的结算利润，作者将其称为 `NoArb`；
4. 第一版对称双边挂单在趋势行情中遭遇逆向选择，只成交输的一侧，库存逐渐变成裸方向仓；
5. `NoArb` 只能描述配平库存，不能描述无法配对的剩余库存；
6. 真正复杂的部分不是报价，而是库存修复、停止条件和异常处理。

## 关键回复

评论区有人总结“玩到最后就是库存管理”，作者回复：

```text
是的，不管什么策略，再高级的模型，再怎么智能的 AI，最后全都是库存管理。
```

## 文中引用研究

- 论文：`Unravelling the Probabilistic Forest: Arbitrage in Prediction Markets`
- arXiv：`https://arxiv.org/abs/2508.03474`

论文报告其研究样本中约有 `4000 万美元`已实现套利利润。这个结果用于说明 Polymarket 存在可被提取的定价无效率，不代表 maker 天然获得这些利润。

