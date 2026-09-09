# 小盘股Stock_Perp第二资本市场：BNC周末价格发现、OI风险容量与Ticker货币化

## 原文信息

- 作者：Danny（`@agintender`）
- 原文标题：`Stock Perp 将成为小盘股未来的主力战场`
- 原文链接：`https://x.com/agintender/status/2097276244341792817`
- X Article 链接：`https://x.com/i/article/2097272634673385472`
- 发布时间：`2026-09-08 18:49`
- 内容类型：市场结构 / 股票永续 / 小盘股衍生品基础设施
- 原文归档：[`sources/agintender-2097276244341792817-stock-perp-small-cap-primary-market/`](sources/agintender-2097276244341792817-stock-perp-small-cap-primary-market/)
- 文章内引用：2 条 X Article 已额外归档，1 篇 Substack 已有本地归档
- 配图：无
- 数据边界：本文涉及的 `BNC / FWDI / ONDS / AAOI` 成交额、`OI`、资金费率和市值数据均按作者原文记录，本次整理未独立复算实时市场数据

## 主题

这篇文章讲的不是“股票永续会取代股票”，而是一个更具体的市场结构变化：

**当一只小盘股有足够大的全球投机需求，但传统股票市场没有给它配套足够深的盘前盘后、期权、借券、做市和 OTC 基础设施时，crypto stock perp 可能在某些时间窗口里变成这只股票的第二资本市场。**

作者用 `BNC` 作为极端样本：美股休市时，`BNC` 股票没有新的现金市场成交，但 Binance、Bitget、Bybit 等交易所里的 `BNC perpetual` 仍在周末交易。按作者记录，当时 `BNC perp` 一段时间内成交额约为正股的 `25` 倍，`OI` 约 `8800 万美元`，相当于流通股票价值的一半以上，Binance 上 funding 一度达到每 `8` 小时 `+2%` 上限。

这组数字的真正含义不是“perp 一定更准”，而是：

```text
股票市场休息 -> 新闻和投机需求不休息 -> perp 继续交易
-> OI 储存风险偏好 -> funding 给拥挤方向定价
-> 周一开盘前，现金股票已经面对一套外部衍生品市场给出的候选价格
```

所以作者真正关心的问题是：

```text
哪些 ticker 会先出现一个比原股票市场更大的外围金融系统？
```

## 核心框架

### 1. 小盘股缺的不是故事，而是交易容量

很多小盘股并不缺叙事。

它们可能正好踩中 `AI`、无人机、量子计算、核电、太空、`crypto treasury`、`biotech` 等热门主题，社交媒体讨论很热，但传统市场能提供的交易工具有限：

- 正股订单簿浅；
- 盘前盘后流动性更薄；
- 期权链不完整，远月和价外档位深度不足；
- 做空需要 `locate / borrow availability / borrow fee`；
- 周末和节假日无法用现金股票表达新信息；
- 非美国用户进入美股账户体系成本高。

Stock perp 正好补这个缺口。它不需要设计几十个行权价，也没有到期日，用户用 `USDT / USDC` 抵押就可以表达多空和杠杆观点。

这也是作者说“小盘股缺的是赌场”的意思：不是说这些公司质量更好，而是说**投机需求已经存在，只是传统金融没有为它修好足够宽的交易通道**。

### 2. BNC 是极端样本，但不是通用样本

作者没有把所有小盘股都归为同一类，而是拿 `BNC / FWDI / ONDS / AAOI` 做对比。

| 标的 | 作者给出的状态 | 关键含义 |
|---|---|---|
| `BNC` | perp 成交和 `OI` 在特定窗口里明显压过正股 | 传统市场基础设施薄，crypto 衍生品可能成为临时主市场 |
| `FWDI` | perp `OI` 已达到流通股票价值的十几个百分点 | 公司资产负债表本身连接 Solana / DeFi，外围衍生品已有存在感 |
| `ONDS` | 有无人机、国防、自动化叙事，但正股和期权已经活跃 | crypto 只复制 ticker，没有解决传统市场解决不了的问题 |
| `AAOI` | AI 光通信高 beta，但正股和期权市场已经很深 | crypto 只能做外围增量桌子，很难夺取主价格发现 |

这个比较把筛选条件说清楚了：

```text
Stock perp 机会 != 小市值
Stock perp 机会 = 大 attention + 小 traditional financial capacity
```

市值只是变量之一。更关键的是传统市场有没有给这只股票提供足够的衍生品、借券、盘外交易和全球交易入口。

### 3. `Perp OI / Equity Float` 是比 `short interest / float` 更适合的新指标

传统小盘股研究常看 `short interest / float`，因为它衡量可流通股票里有多少被借出做空。

但 stock perp 多了一层外部风险容量。perp 不需要真实股票数量增加，也不要求每一张合约都对应实际借券。只要多空双方愿意进来，清算系统和做市商愿意承接，外部就能生成新的经济敞口。

作者因此提出一个更适合这类市场的指标：

```text
Perp OI / Equity Float
```

它不等于 `synthetic shares`，因为每张 perp 同时有多头和空头，做市商也未必完全到股票市场对冲。但它能衡量一件事：

**这只股票外围衍生品市场已经储存了多少可被清算、换手、收 funding、收 spread 和影响候选价格的风险仓位。**

当这个比例从 `1%` 以下变成十几个百分点，甚至接近或超过 `50%`，它就不再只是旁边的小赌桌，而可能影响现金市场重新开盘时的价格锚。

### 4. OI 不是收入，但它是交易所和做市商的未来交易库存

作者特别区分了 `OI` 和收入。

`BNC` 有 `8800 万美元 OI`，不代表交易所收了 `8800 万美元`。但 `OI` 是未来交易活动的存量基础：

- 仓位会加仓、减仓和平仓；
- 极端行情会产生清算；
- funding 太贵会迫使换方向；
- 做市商需要持续调整 hedge；
- 交易所持续收 fee；
- 做市商持续赚 spread；
- market deployer 未来也可能分享交易活动收入。

这与 Hyperliquid `HIP-3` 这类机制可以接上：过去只有交易所经营市场，现在第三方也可以经营某个 ticker 的 perpetual market，并从交易活动中分成。

这里最重要的变化是，ticker 自身开始被产品化：

```text
上市公司 ticker -> perp market -> OI -> fee / funding / spread / liquidation activity
```

### 5. Funding 给拥挤方向标价，也可能变成武器

传统股票市场会告诉你“这家公司值多少钱”，stock perp 额外告诉你：

```text
现在持有这个方向观点，需要付多少钱？
```

当多头极度拥挤，funding 会推高到很贵；当空头极度拥挤，funding 可以成为逼空链条的一部分。

作者在主文里引用了自己关于 `ALPACA` 下架逼空的文章。那个案例的价值在于说明：低流动性永续市场里，funding 不只是锚定工具，也可以成为时间惩罚和仓位挤压工具。

放回 `BNC`，`+2% / 8h` 的 funding 意味着：

- 这不是普通多空表达，而是拥挤多头愿意支付极高持仓成本；
- 空头未必需要判断公司基本面崩盘，只要认为 funding 过高就可能站到另一边；
- vault 或做市策略可以围绕现货、tokenized stock、perp 和 funding 设计中性收益；
- 但如果没有可靠 hedge 和 borrow 路径，所谓中性很容易在跳空、清算和流动性断裂里失效。

### 6. 一只股票进入链上后，就不再只有一种形态

作者把 stock perp 和传统 `CFD` 区分开来：`CFD` 多数仍停留在 broker 数据库里，而 crypto 衍生品会继续接 DeFi。

一只股票未来可能同时存在：

- Nasdaq 正股；
- 传统 options；
- CEX stock perp；
- tokenized stock；
- 链上借贷抵押；
- LP 池；
- funding vault；
- prediction market；
- points / meme / community。

这会把一个 ticker 从单一证券代码，扩展成一整套金融 Lego。

对普通大票来说，这可能只是附属层；但对 `BNC / FWDI` 这类 crypto treasury 或链上资产强相关公司来说，它可能反过来影响公司的资本市场叙事。

### 7. “不增发也能货币化 ticker”只说对了一半

Perp 的确可以在不增加一股股票的情况下，围绕一家公司制造大量经济敞口。

但这里要分清谁赚钱：

- 如果公司和 perp 市场没有商业关系，外部成交不会自动变成公司收入；
- 直接赚钱的是交易所、做市商、market deployer、套利者、LP 和 funding receiver；
- 只有当发行人、tokenization provider、oracle provider、market deployer、DeFi protocol 建立授权、分发或收入关系时，公司才可能真正把 ticker 持续货币化。

所以“不稀释也能收割”不能理解成公司自动拿钱。

更准确的说法是：

```text
投机与发行被拆开
市场可以先围绕 ticker 生成衍生品活动
公司是否能捕获这部分价值，取决于后续商业结构和监管许可
```

## 观察指标

如果要把这篇文章转成研究清单，重点不应只看“哪只股票上了 perp”，而要看下面这些指标。

| 指标 | 观察意义 |
|---|---|
| `Perp OI / Equity Float` | 外围衍生品仓位池相对现金股票流通盘有多大 |
| `Perp Volume / Spot Volume` | crypto 市场是否在特定窗口压过正股交易 |
| `Weekend / Holiday Gap` | 美股休市时，perp 是否提前形成候选价格 |
| `Funding Level` | 多空拥挤程度和持仓成本 |
| `Options OI / Spread / Strike Depth` | 传统衍生品是否已经满足投机需求 |
| `Borrow Availability / Borrow Fee` | 现金股票做空通道是否充分 |
| `Tokenized Wrapper Liquidity` | 链上现货库存是否可用于抵押、借贷、LP 和 hedge |
| `Index / Mark Methodology` | 休市时价格是否可能被本地订单簿和清算反馈自我推动 |
| `Venue Cross-Reference` | 多个交易所是否互相参考，导致外部价格其实来自同一组衍生品市场 |

最重要的筛选式可以写成：

```text
候选标的 =
  高 attention
+ 小 float
+ 弱 options
+ 弱 borrow
+ 弱盘前盘后
+ 有 crypto-native 用户
+ 有 tokenized stock / crypto treasury / 链上对冲资产
```

## 和仓库已有材料的关系

### 1. 接上 Stock Perp 休市定价文章

仓库里的《Stock_Perp休市定价：Impact_Price、EWMA、Mark护栏与清算反馈环》回答的是：

```text
当 Nasdaq 关门后，交易所如何生成 Index 和 Mark？
```

这篇文章回答的是：

```text
哪些股票会让这套休市价格生产机制变得真正重要？
```

前者偏机制，后者偏标的筛选和市场结构。

### 2. 接上 bStock 定价权文章

《bStock与股票永续的定价权》把 `Perp / bStock / Borrow / Cash Market` 分成不同功能层：

```text
Perp 负责快速表达多空与杠杆
bStock 负责保存可持有和可抵押的股票风险库存
Borrow / Conversion 负责纠错
Cash Market 最终验证
```

这篇文章进一步说明，当标的是传统金融基础设施不足的小盘股时，`Perp` 不只是候选价格层，还可能先生成比正股更大的外围风险市场。

### 3. 接上 ALPACA 逼空案例

作者引用 `ALPACA` 的意义在于：funding 和清算机制在低流动性市场里可以被武器化。

如果小盘股 stock perp 的 `OI / float` 做到很高，而现金股票又休市，类似风险并不会凭空消失。区别只是标的从 crypto token 变成了股票 ticker。

## 风险与限制

### 1. 原文数字需要独立复算

文章中的 `BNC / FWDI / ONDS / AAOI` 成交额、`OI`、funding、流通市值和 perp/spot 比值是作者在 `2026-09-08` 的观察口径。

这些数字高度时点化。真正用于交易前，应重新核对：

- 各交易所是否仍上线对应合约；
- 交易所成交额是否存在重复统计或刷量；
- `OI` 是否按名义价值统一口径；
- 正股成交额使用的是 regular session、premarket、after-hours 还是全日口径；
- float 和可借券规模是否已变化；
- funding 上限和结算频率是否已调整。

### 2. Perp 成交领先不等于价格发现正确

周末 perp 先交易，只说明它先给出候选价格。

它可能是：

- 真实新信息的价格发现；
- crypto 用户情绪过冲；
- 做市商库存再平衡；
- 薄盘口被推出来的价格；
- funding 驱动的仓位挤压；
- 多个平台互相参考后的循环报价。

要证明它真的领先现金市场，需要逐秒比较 `perp / premarket / opening auction / cash open` 的 lead-lag，而不是只比较成交额和开盘前后价格。

### 3. 外围风险容量会放大尾部，而不是自动提高效率

`Perp OI / Equity Float` 升高有两面：

- 好处是市场有更多表达观点的工具；
- 坏处是清算、funding、mark、oracle 和做市商 hedge 会形成更复杂的反馈环。

如果 perp 的外部价格被现金市场验证，它就是价格发现；如果它在休市期间自我循环，它可能只是杠杆仓位互相踩踏。

### 4. 监管和税务不是空白

作者强调得很对：stock perp 的问题不是“没有监管”，而是产品跑到了法律分类之间。

它可能同时涉及：

- single-stock derivatives；
- security-based swap；
- 离岸交易所；
- stablecoin margin；
- tokenized stock collateral；
- DeFi lending；
- cash-settled derivative taxation；
- 不同司法辖区的用户分发限制。

所以不能把 stock perp 理解成监管套利的永久空间。更现实的判断是：它在监管跟上之前会先形成市场，但市场越大，越会倒逼监管明确分类。

### 5. 公司不一定能捕获衍生品活动价值

如果外部交易所擅自围绕 ticker 上 perp，公司没有授权、没有分成、没有 tokenized stock 合作，也没有把 treasury 或 DeFi 产品接进去，那么交易再热闹也可能只是外围玩家赚钱。

公司真正受益，需要至少满足一项：

- tokenized stock 发行或授权关系；
- oracle / market deployer / exchange 商业关系；
- treasury 资产能进入链上抵押、借贷、staking 或 LP；
- 外围市场反过来改善融资条件或股票流动性；
- 公司有能力用更高股价做更低成本融资或回购。

否则“不增发也能货币化 ticker”只停留在交易所和做市商层面。

## 扩散分析

### 1. 可以做一个 Stock Perp Watchlist

这篇最适合工程化成一个筛选器，而不是只保存观点。

核心字段可以是：

```text
ticker
market_cap
free_float
perp_venues
perp_oi
perp_volume_24h
spot_volume_regular
spot_volume_premarket_afterhours
options_oi
average_option_spread
borrow_fee
borrow_availability
funding_rate
weekend_price_gap
tokenized_stock_liquidity
crypto_treasury_exposure
perp_oi_to_float
perp_volume_to_spot_volume
```

然后按三类标的分层：

- `BNC 型`：传统市场薄、crypto attention 强、perp 可能临时主导；
- `FWDI 型`：公司资产负债表已经接 DeFi，外围衍生品和公司叙事相互强化；
- `AAOI / ONDS 型`：故事强，但传统市场已经提供足够交易容量，perp 更像外围补充。

### 2. 真正的事件窗口可能是周末和长假

平时美股开盘时，现金市场、期权、盘前盘后和借券通道都能参与纠错。

但周末、长假和突发公告时，现金股票沉默，stock perp 仍然交易。最值得看的是：

```text
周五收盘价
-> 周末 stock perp 价格路径
-> funding 与 OI 变化
-> 周一盘前第一笔报价
-> 开盘集合竞价
-> regular session 前 30 分钟是否回归或确认
```

如果多次出现现金市场开盘后跟随 perp，而不是 perp 被现金市场修正，才说明价格发现权真的在迁移。

### 3. 对交易者来说，edge 可能来自“基础设施缺口”而不是方向判断

这类机会的核心不是猜公司好坏，而是识别哪里存在结构缺口：

- 股票休市但信息持续更新；
- 做空通道堵塞但 perp 可以 short；
- 传统期权太宽但 perp 可以表达杠杆；
- tokenized stock 可以抵押但 borrow 市场还没成熟；
- funding 极端但可对冲资产不足；
- OI 已经足够大但 oracle 仍然按旧股票市场假设设计。

方向交易只是在这些缺口上下注。更稳的研究方向是观察价差、funding、OI、borrow 和开盘修正之间的关系。

## 一句话结论

Stock perp 对小盘股最大的变化不是增加一个合约，而是在传统金融交易容量不足的 ticker 旁边生成一个全天候、可杠杆、可清算、可收 funding 的外围资本市场；真正值得盯的是 `Perp OI / Equity Float`、周末价格发现和这套外部风险容量会不会反过来改写正股开盘。
