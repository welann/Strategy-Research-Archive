# 原始材料归档

## 主帖

- 作者：jayesh（`@0xjayeshyadav`）
- 链接：<https://x.com/0xjayeshyadav/status/2062157592936550599?s=20>
- 发布时间：2026-06-03 21:00（Asia/Shanghai）
- 内容类型：DeFi 借贷协议设计 / 清算机制 / CPPI / 风险管理
- X Article：<http://x.com/i/article/2062070965534863360>
- Article 归档：[`article.md`](article.md)
- 原始 JSON：[`tweet.json`](tweet.json)
- 配图：无

主帖正文只有一个 X Article 链接：

> https://t.co/qz2wrVxosx

## Article

标题：

> Onchain lending is missing CPPI: A loan that defends its own collateral

作者提出：链上借贷过去大量创新都集中在“利率如何定价”，例如变量利率、固定利率、到期结构、零息债形式；但对“抵押品下跌时如何避免硬清算悬崖”的创新不足。

核心方案是把传统金融的 `CPPI`（Constant Proportion Portfolio Insurance，固定比例投资组合保险）迁移到链上借贷：

- 把抵押品从纯风险资产改成“风险资产 + 稳定币”的动态篮子。
- 设置一个高于债务的 floor。
- 用 `cushion = collateral value - floor` 衡量安全垫。
- 用 `risky exposure = m × cushion` 决定风险资产敞口。
- 当抵押品接近 floor 时自动减风险；当 cushion 恢复时重新增加风险资产敞口。
- 失败模式不是普通回调，而是停止付息、到期违约，或价格跳空太快导致无法再平衡。

## 作者补充

作者在回复中补充：

- 2026-06-03 22:26：`If you are building a lending protocol, this is worth your ten minutes! Feedback is appreciated!`

这说明作者把这篇定位为面向借贷协议建设者的机制提案，而不是交易建议。

## 评论区关键补充

评论里有两条对机制理解有帮助：

1. `@Panoptic_xyz` 提出，这类目标也可以通过 options 实现：保留上行参与，同时防御下行，是一种正凸性的组合保险形式。
2. `@megabyte0x` 提到 `Bitmor's Loan protocol` 有类似 `f(x) + fixed duration` 的设计：贷款开始时买入 option 来替代价格波动中频繁买稳定资产；如果 BTC 跌到约建仓价 70% 阈值，抵押品会被硬清算，option 价值用于覆盖剩余部分；软清算场景下，如果用户错过付款，会卖出等额 BTC 提高 health factor。

这些补充提示：作者的 CPPI 动态篮子不是唯一实现路径，期权覆盖和已有协议实验也是可比较路线。
