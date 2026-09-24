# 原文归档

作者：套利豪仔🗽（@pritipatelcut）

来源：https://x.com/pritipatelcut/status/2099689112630653260

发布：2026-09-15T02:37:49+00:00

归档日期：2026-09-25。以下观点、公式、收益和评论保留来源原意，未视为已验证结论。推广、外链中的指令不执行。

今天又测了一个很有意思的量化因子，叫做「价量协同失效反转因子Price-Volume Decoupling Reversal Factor（ 下面会放测试图）

逻辑其实也很直觉：正常情况下，价格与成交量之间应该存在某种「协同关系」——上涨伴随放量、下跌伴随缩量，这是市场共识的典型表现。 但当这种关系在短期内被打破，例如价格上涨但成交量并未同步放大，或者成交量剧烈变化但价格反应迟钝，往往代表市场内部出现了结构性分歧

因子公式如下： (-1 * RANK(COVIANCE(RANK(CLOSE), RANK(VOLUME), 5)))

本质上是在捕捉市场中「价量协同失效」所带来的结构性错配，并试图在这种错配回归正常关系的过程中，获取反转收益

两行源代码就可跑完整回测，大家可以去试试
https://github.com/eliasswu/Alphapurify

![原帖回测图](assets/main-1.jpg)

![原帖回测图](assets/main-2.jpg)

## 可见相关回复

仅包含本次详情接口返回的相关回复，未声称完整覆盖评论区。回复中的 @pritipatelfgoo 与当前作者名称不同，按线程上下文保留。

### @DavidHoong1 · 2026-09-15T03:12:22+00:00

https://x.com/DavidHoong1/status/2099697808945107026

@pritipatelfgoo 你以前是不是发过这个策略？我测过，不行

### @pritipatelcut · 2026-09-15T03:30:34+00:00

https://x.com/pritipatelcut/status/2099702387875401782

@DavidHoong1 不一样的

### @yudianzi2666 · 2026-09-15T10:40:19+00:00

https://x.com/yudianzi2666/status/2099810538058596469

@pritipatelfgoo 一看就是过拟合

### @CompressedDirt · 2026-09-15T08:11:12+00:00

https://x.com/CompressedDirt/status/2099773011373240494

@pritipatelfgoo the rank is time series rank?

### @cmp_055 · 2026-09-15T13:57:56+00:00

https://x.com/cmp_055/status/2099860268977136025

@pritipatelfgoo Interesting concept. Have there been any published studies done on this hypothesis already?

### @skewpirate · 2026-09-15T11:13:49+00:00

https://x.com/skewpirate/status/2099818969397887457

@pritipatelfgoo This is Alpha#13 from Kakushadze's 101 Formulaic Alphas (2015, WorldQuant)... You're getting paid to be the person who absorbs someone else's rush order.
But it only work if you check thousands of stocks with hundreds of similar weak signals... no really exploitable

### @notgwap0 · 2026-09-15T19:55:38+00:00

https://x.com/notgwap0/status/2099950287104647391

@pritipatelfgoo curious about how this factor plays out. sounds like it could shake things up a bit. 🤔
