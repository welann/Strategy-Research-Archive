# 核验记录

核验日期：2026-10-10，北京时间。

- [William F. Sharpe：The Sharpe Ratio（1994）](https://web.stanford.edu/~wfsharpe/art/sr/SR.htm)：均值和标准差按同一常数缩放，夏普不变。用于限定原文“换资金分母，夏普当然不同”的表述；动态分母、非一致基准或不同收益对象另论。
- [Andrew W. Lo：The Statistics of Sharpe Ratios（2002，论文副本）](https://traders.berkeley.edu/papers/The-Statistics-of-Sharpe-Ratios.pdf)：区分iid、平稳收益与时间聚合，相关性会影响年化和估计。用于说明计算比率与简单√N年化的条件不同。
- [David H. Bailey、Marcos López de Prado：The Deflated Sharpe Ratio（2014）](https://www.davidhbailey.com/dhbpapers/deflated-sharpe.pdf)：DSR针对多重试验选择偏差和非正态影响，涉及样本长度、偏度、峰度、候选夏普分布与有效独立试验数。

整理者算术校核：0.5×√(10,000×252)=约793.7；为原文假设例子的机械年化结果，不能当作组合实盘绩效。固定正数对同一超额收益序列的缩放不改变夏普。Sortino下行偏差的说明用于澄清数学口径，没有对任何真实策略计算该指标。

未核验：原文历史熔断次数等旁支事实、任何具体策略的风险概率与容量。概率0.1%没有事件频率说明；资金规模、单笔收益、压力参数和百万次筛参均按教学假设处理。

来源范围：395个文章内容块、1张装饰封面。公开接口报告7条回复但未取得正文；twitter-cli状态检查为AUTH_NEEDED，评论补充无法确认。
