# Polymarket 避雷指南

- Author: @YourAirdropETH (Y林YourAirdrop.AI)
- Published: 2026-04-17 19:42
- URL: https://x.com/yourairdropeth/status/2045105657691721787
- Article URL: http://x.com/i/article/2044774010551201792
- Source Type: X Article
- Capture Tool: twitter-cli
- Capture Note: 主帖正文只有文章链接，真正正文来自 X Article；`twitter article` 未返回正文配图或封面图。

## 正文

基于: 18 篇精读文献 (含 9 篇完整 PDF/HTML 学术论文) + 934K 笔 on-chain 交易分析 + 77K wallet 画像 + 14 个我亲自踩的方法论错误 + Polymarket 官方 leaderboard API 数据 + poly-maker 源码审计

## 第一章：你面对的现实

1.1 绝大多数人亏钱

一句话: 2.5 million 人里只有 172 人做到了 "稳定 passive income"。你进去的概率不是 50/50，是 0.007%。

1.2 利润极度集中

## 第二章：已被验证的"坑" (不要踩)

坑 1: 🚫 买 1-10c 的 longshot YES

数据: Becker 在 Kalshi 72M 交易上验证:

- 1c 的 YES 合约实际只有 0.43% 概率 win (不是 1%)
- 同价位 NO 合约有 1.57% 概率 win
- YES 和 NO 之间有 64 个百分点的差距
- 零售 taker 在 1-10c 区间占 YES volume 的 41-47% — 他们是"乐观税"的主要缴纳者

注意: 这个数据来自 Kalshi 不是 Polymarket。Reichenbach & Walther 在 Polymarket 上说"没有 general longshot bias"。但 Le (2026) 发现 Polymarket 政治市场有 underconfidence (方向一致, 只是不是所有品类)。

结论: 不管在哪个平台, 买便宜的 YES longshot 是零售亏钱的 #1 方式。

坑 2: 🚫 做 Generic LP / Market Making

多重验证:

- 我的 Phase 0: 934K 笔 Polymarket 交易, aggregate maker gross return = -8.19%
- @defiance_cr (poly-maker 作者, 曾 peak $700-800/day): 亲笔写在 GitHub README "In today's market, this bot is not profitable and will lose money"
- wanguolin LP rewards postmortem: 他写的是理论设计稿, 0 P&L 数据, 他自己说 "I do not [think it's worth it] either"
- Prediction Arena: 6 个 frontier LLM 用 $10K 真金白银做了 57 天, 全部亏钱 (-16% to -31% Kalshi)

唯一例外: 如果你有特定品类的定价 alpha (比如体育模型) 加持的 maker 策略, 理论上可能 work。但 generic "挂单收 reward" 在 2026 年已死。

坑 3: 🚫 让 AI 全自动交易

Prediction Arena (2604.07355) 是迄今最严格的测试:

- 6 个 frontier 模型: GPT-5.2, Claude Opus 4.5, Grok-4-20-checkpoint, GLM-4.7, Gemini 3 Pro, Grok 4.1 Fast
- 每个 $10K 真金白银, 57 天
- 全部亏钱, 最好的 (GLM-4.7) 也亏了 -16%
- 在 Polymarket 上亏得少一些 (平均 -1.1% vs Kalshi -22.6%), 因为 Polymarket 允许模型自选市场

关键发现: "Research quantity shows no correlation with outcomes" — 做更多研究不等于表现更好。

正确用法: AI 辅助选市场 + 过滤坏交易, 不是让 AI 自己下单。

坑 4: 🚫 抄别人的单

为什么看起来可行但实际不行:

- Polymarket data-api 能实时看到 top wallets 的交易 ✓
- 14 个持续盈利的 wallet 我都能追踪到 ✓
- 但: 延迟 30 秒+ → 你的 fill price 比他们差
- 但: 他们很多是 maker orders (挂限价等 dip fill), 你抄到的时候 dip 已经过了
- 但: 他们 $5K-$147K 单笔, 你 $50 跟进 → size 错配
- 但: 他们 per-market WR 只有 41-51%, 你随机抽 10 笔抄 → 样本噪声大

Della Vedova: "Execution timing determines profitability" — 他们的 edge 就是比你早。你抄不了一个"时间"。

坑 5: 🚫 跨平台套利 (Polymarket ↔ Kalshi)

IMDEA (2508.03474): 2024-2025 年总共 $40M 被提取。 但: Top 10 arbitrageurs 拿走 23%, 都是高频 bot。

Odaily: "Arbitrage window narrowing at visible rate" + settlement definition mismatch 风险 (2024 government shutdown 案例: 两边同时亏)。

坑 6: 🚫 Speed/Latency Trading

Odaily verbatim: "Not recommended unless technical background + willing to invest time in system development. Retail participation described as increasingly virtually impossible."

Powell 讲话案例: 8 秒内合约从 $0.65 → $0.78。你 8 秒内甚至看不到新闻。

坑 7: 🚫 在 Weather 市场上买 favorite

Le (2026): Weather markets 短期 θ < 1.0 (overconfident)。市场标 70c 的天气事件, 实际只有 <70% 概率发生。和 political markets 方向完全相反。

如果你在 weather 上做和 "买 favorite" 策略一样的事, 你系统性亏钱。

这是我自己数据里 weather maker +26.47% 的解释: maker 在 weather 上倾向于卖 favorite → 因为 favorite 被高估 → 卖方赚。

## 第三章：这个市场到底谁在赚钱

3.1 赚钱者画像 (基于 leaderboard + wallet 分析)

14 个同时出现在 30d + 7d + 1d 排行榜 top50 的钱包:

- 68% 做 Sports (足球/NBA/MLB/NHL/UFC/网球/电竞)
- 86% 在 0.30-0.70 中间价位交易 (不是 97-99c!)
- 50% maker-heavy (用限价单入场, 等 dip fill)
- Per-market WR 只有 41-51% — 输的市场比赢的多, 但赢的金额 > 输的金额

3.2 赚钱的真正机制

Della Vedova (222M Polymarket trades):

> "Traders with above-random forecasting accuracy earn negative returns because they arrive late. Traders with near-random accuracy earn positive returns through execution quality alone."

翻译:

- 预测得准不赚钱 — retail 选对 winner 51.3% 的时候仍然亏, 因为执行太差
- 执行得好才赚钱 — bot 只有 coin-flip 准确率但赚了 $133M, 因为进出价格好

3.3 品类定价偏差 (Le 2026, 292M trades)

## 第四章：如果你还是要做,  3 条可行路径

路线 A: 97-99c Bonding

****具体方法隐藏****

路线 B: Political Favorite

****具体方法隐藏****

路线 C: Multi-outcome Arbitrage

****具体方法隐藏****

## 第五章：心态红线

1. 不要把 Polymarket 当收入来源

172 / 2,500,000 = 0.007%。你在这 172 人里的概率极低。把它当学习平台和小额实验, 不要把房租赌进去。

2. 不要因为赢了几笔就加仓

grok-4-20-checkpoint (frontier LLM) 曾经 +15.5% peak, 然后一天跌 -8.99% — 因为多个 correlated weather positions 同时结算。即使是最好的模型也会被集中风险打穿。

3. 不要和 HFT 抢

- 跨平台套利: HFT 吃完了
- 5/15min crypto: 动态 fee 杀死了
- Live-game 实时下注: 你的反应比 bot 慢 1000x

你能做的是 HFT 不屑做的事: 锁 $97 资金 3 周赚 $1 (97-99c bonding), 或者在政治市场上利用 θ=1.31 的 calibration 偏差。这些回报太低, HFT 的资金成本 cover 不了。

4. 不要忽视 fee

2026-03-30 fee expansion 后:

- Sports: 3% taker fee
- Crypto: 7.2%
- Politics/Finance: 4%
- Weather/Culture: 5%
- Geopolitics: 0% (唯一免费品类)

Fee 公式: fee = rate × price × (1-price)

- 在 50c: fee = 4% × 0.5 × 0.5 = 1.0% of notional
- 在 80c: fee = 4% × 0.8 × 0.2 = 0.64%
- 在 97c: fee = 4% × 0.97 × 0.03 = 0.12%

极端价格的 fee 最低, 这也是 97-99c 策略能 survive fee 的原因。

5. 不要相信"X 上有人赚了 $Y"

Odaily 引用的 @defiance_cr "$700-800/day" 是 2024 peak。同一个人 2026 年 GitHub 上写 "not profitable, will lose money"。

所有"我赚了"的帖子都是 survivorship bias + gross 不扣 loss。

6. Sports 校准很好 = 没有免费午餐

Le (2026) 的 292M 交易分析显示 Sports 的 θ ≈ 1.0 (完美校准)。市场标 70% 的比赛真的大约 70% 赢。

你在 sports 上的 edge 只能来自: (1) 执行更好 (limit order 等 dip) 或 (2) 你真的比市场更懂这项运动。

如果你没有 (1) 或 (2), 在 sports 上你就是那个被 top wallet 吃掉的 retail。

## 附录：文献溯源表

****已隐藏****

## 评论区补充

作者在抓取到的评论区中没有补充新的策略细节。评论区主要是读者反馈，包括“数据扎实”“少走弯路”“不亏钱胜过亏钱”等，没有改变正文核心结论。
