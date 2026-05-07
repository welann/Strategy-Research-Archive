# Happy arbitrage on arbitrum without local node. 记一次无本地节点的套利

- Author: @hklst4r (Weilin (William) Li)
- Published: 2026-04-23 09:41
- Status URL: https://x.com/hklst4r/status/2047128806549328186?s=52
- Article URL: http://x.com/i/article/2047120702986244096
- Source Type: X link post + X article
- Capture Tool: twitter-cli
- Capture Note: 顶层推文本身只有一条链接，正文实际写在 X Article 里。本文归档以文章正文为主，并保留关键评论区补充。

## 原文标题

Happy arbitrage on arbitrum without local node. 记一次无本地节点的套利

## 原文正文

The recent Kelp DAO attack creates bankrun on multiple lending protocols, especially AAVE. The WETH market on Ethereum, Arbitrum, and Mantle all witnesses a 100% utilization rate.

Existing users wants to exit while some speculators wants to buy their Aave ETH at a discount (earning the risk premium). As a result, multiple protocols created trading venus for exiting Aave ETH including @0xfluid and Uniswap.

https://x.com/0xfluid/status/2046971208550486244?s=20

A natural arbitrage path then appears: Buying aWETH on the market, remove liquidity when there is. As many users are repaying their ETH (though they can buy Aave ETH to repay at a discount), sometimes there would be liquidity, which was devoured by MEV bots within several blocks.

I feel it's extremely hard to compete on Ethereum with such a high bribe ratio. And given the umbrella mechanism of Aave, the depeg of Aave ETH is only at ~0.3%. Not much profitability. I turned to arbitrum. The depeg was once reaching 10% (1 Aave ETH = 0.9 ETH) before Arbitrum annouces their rescue of funds. I started to perform this arbitrage on arbitrum to join this game.

However I don't have a powerful enough machine to run a local arbitrum node. And competition looks already very strong. I did some research on this and below are the tricks I used.

Most arbitrages follow the pattern of buy in advance, withdraw later (because uniswap may not have much instant liquidity at the time there is liquidity). Meaning they would require capital to perform the arbitrage. But when large repayment is observed, they fail to extract the maximum value. Instead I performed a bit on-chain routing to find best prices and routes across multiple DEXs. As Arbitrum does not order transactions based on gas price, I can pay a very low gas price; so a little more gas consumption is acceptable.

So how about delay? Arbitrum (besides the timeboost part) is FCFS. The faster you can send your transaction, the earlier it is included. On the information-getting side, I run the arbitrage with third-party RPC to fetch repayment events, which has an astonishing low delay; on the execution side, I rented multiple serves around the world to ping the sequencer and finally able to locate it. I rented multiple servers located near Arbitrum's main sequencer and, after applying some network level tricks, made the sending delay also lowered to 10~30 ms (without considering the arbitrum chain delay of 250ms as specified in their doc).

With this setup, I had the bot running, and earned a much larger share than average of bots competing for this opportunity. Even when another guy joining with timeboost (arbitrum's unique MEV ordering protocol), I was still able to earn a fair share.

This is just a toy and I do not expect to earn much about it. But I'm surprised that this took me only 1 hour but yields such good results. Maybe, sometimes, running an arbitrage bot does not require a local node. : )

## 评论区与补充

### 1. 有读者直接问到了“落后几个 block”这个最核心的问题

- 时间：2026-04-23 11:55
- 作者：`@changq1ng`
- 内容：自己之前在 `Arbitrum` 上也做过类似事情，监听事件后发起套利交易，但总是落后 `3` 个 `block`，竞争者能做到 `T+2`，所以一次都没赚到，追问作者收到 `event` 后能在几个 `block` 内上链。

### 2. 另一位实操者补充：真正最难的不是识别机会，而是“发交易”

- 时间：2026-04-23 12:44
- 作者：`@lucas_wang77129`
- 内容：实操一天赚了 `0.7 WETH`，但认为最大难点就是发交易本身，包括官方 `RPC` 的 `feed`、`Alchemy` 的 `pending pool`、地理位置、算法和技术能力，最后选择退出。

### 3. 评论区强化了正文的一个结论

- 这个机会的核心不只是“知道有折价”，而是：
  - 谁先拿到还款事件
  - 谁先把交易送到 sequencer
  - 谁能把发送延迟压得更低
