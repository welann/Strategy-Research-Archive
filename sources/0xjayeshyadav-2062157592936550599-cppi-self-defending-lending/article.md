# Onchain lending is missing CPPI: A loan that defends its own collateral

- Author: @0xjayeshyadav (jayesh)
- Published: Wed Jun 03 13:00:57 +0000 2026
- URL: https://x.com/0xjayeshyadav/status/2062157592936550599
- Likes: 39
- Retweets: 6
- Replies: 6
- Bookmarks: 26
- Views: 0

Most onchain loans die in the same dull and predictable way, where the collateral falls, a threshold is crossed, a liquidator closes the position at a penalty, and the borrower is left holding the loss on an asset that very often recovers a week later. We have spent five years making the price of credit smarter, and almost none of that energy on the thing that actually wipes people out, which is the liquidation itself.

I want to propose a different shape for the loan and it borrows a 40-year-old idea from traditional finance called Constant Proportion Portfolio Insurance, and it produces a loan that quietly defends its own collateral instead of waiting to be liquidated. Curve and f(x) have already shown the instinct works onchain. What nobody has done yet is name the mechanism for what it is, drive it off the right variable, and hand the borrower the dial that decides its risk. Let me walk through where lending has been, what this primitive is, the math that makes it work, where it can fail, and how a protocol could actually build it.

## Where onchain lending has actually innovated

The first generation of onchain lending was variable rate, and it still anchors the entire category. Compound v2 went live in May 2019 and Aave grew out of ETHLend, which launched in 2017, rebranded to Aave in 2018, and moved to a pooled liquidity model with Aave V1 in early 2020. Both set the borrow rate the same way, algorithmically from utilization. When more of a pool is borrowed, the rate climbs along an interest rate curve, which pulls in fresh supply and discourages new borrowing. The rate floats for everyone in the pool and updates every block as borrowing demand shifts.

This pooled variable model won decisively, and it still anchors the largest part of the market today. Aave alone holds around $13 billion of deposits in mid 2026, and Compound, now on its isolated market design called Comet, sits a little above $1 billion. It is worth noting how hard the rate side has been to improve even for the established ones. Aave shipped a stable rate borrowing option years ago, then disabled new stable rate borrows in November 2023 after a vulnerability was found in the stable rate logic, and fully deprecated it through governance in 2024. The dominant onchain lending experience today remains variable rate, and that has barely changed in years.

The current frontier is fixed rate lending, and this is where most of the recent design talent has gone. Pendle is the clearest example and the category leader, holding around $1.3 billion in mid 2026. It works by splitting a yield bearing asset into a Principal Token and a Yield Token, where the Principal Token behaves like a zero coupon bond that you buy at a discount and redeem at face value at maturity, which locks in a fixed yield. And in May 2026 Morpho published the Midnight whitepaper, a fixed rate, fixed maturity protocol where lending and borrowing are expressed as the trading of credit and debt units whose payoff is analogous to zero coupon obligations, with offers that do not lock capital until settlement. Midnight is freshly released and open sourced, and it signals where the serious builders are pointing, which is squarely at the rate.

So it is worth looking at the two axes of innovation side by side. On the axis of what credit costs, we have moved from variable to fixed and built a genuine toolkit along the way. On the axis of what happens when the collateral falls, almost nothing has changed, since the overwhelming majority of onchain debt is still protected by hard liquidation, a single line in price beyond which your position is closed and penalized, and that neglected second axis is the gap I care about.

## The exceptions that already point the way

Two protocols deserve full credit here, because they moved on exactly this problem and they moved first.

Curve's crvUSD introduced soft liquidation through a mechanism called LLAMMA, the Lending Liquidating AMM Algorithm. Instead of one liquidation price, your collateral is spread across a set of discrete price bands, anywhere from 4-50 of them, and each band acts as its own small liquidation zone. As the price falls through a band, that band's collateral is progressively sold into crvUSD. As the price recovers back through a band, the crvUSD buys the collateral back, which Curve calls de liquidation. Arbitrageurs do the actual trading, because LLAMMA quotes prices offset from the oracle so that rebalancing against external markets becomes profitable. The position is never slammed shut at one threshold, and its exposure is instead continuously shifted between the volatile asset and the stablecoin. crvUSD has run real borrowing through this design.

f(x) Protocol does something structurally similar with its Liquidation Brake. When a leveraged position approaches its liquidation price, the protocol burns part of the position's debt, sells some backing collateral, and pulls the leverage ratio back down, which reduces risk while keeping the user's directional exposure rather than closing them out, and external keepers monitor positions and trigger it when needed. The protocol holds roughly $90 million in mid 2026.

Both of these are doing portfolio insurance on collateral, whether they describe themselves this way or not. They de-risk into a decline and re-risk into a recovery. That is the exact reflex of a strategy traditional finance formalized in the 1980s, and once you see the connection, a cleaner and more general version of the loan falls out.

## CPPI, stated plainly

Constant Proportion Portfolio Insurance was developed by Perold in 1986, extended to equities by Black and Jones in 1987, and given its formal treatment by Black and Perold in 1992. The idea is simple and it is built to protect a floor.

You define a floor, which is the value your portfolio must not fall below. You measure the cushion, which is how far you currently sit above that floor, so cushion = portfolio value - floor. You then hold an amount of the risky asset equal to a multiplier times that cushion, and you park the rest in a safe asset.

> risky exposure = m × (portfolio value - floor)

The whole behavior of the strategy follows from that single line, and it plays out intuitively as markets move. When the cushion is fat, you hold a lot of the risky asset. As losses eat into the cushion, your risky exposure mechanically shrinks toward zero, which moves you into the safe asset before you can breach the floor. When the cushion rebuilds, you lean back into the risky asset. The strategy sells into weakness and buys into strength.

Mapping that same structure onto a loan makes the correspondence exact. The floor sits just above the debt, at the debt plus a small gap margin I size later, because the collateral must never actually reach the debt, since the moment it drops under the debt you have bad debt and a liquidation. The cushion is your collateral value minus that floor, the safety buffer every borrower already watches, measured to the floor rather than all the way down to the debt. The risky asset is the volatile collateral, ETH or a BTC wrapper or SOL, and the safe asset is a stablecoin. A CPPI loan holds its collateral as a managed basket of the two, and it rebalances that basket as the cushion breathes. As your collateral falls toward the floor, the basket steps out of the volatile asset and into the stablecoin, defending it. As the cushion grows, it steps back into the volatile asset, handing you the upside. What changes is that the ordinary dips that would liquidate a normal position no longer kill this one, because it de-risks instead of crossing a single line, and the loan fails only if you stop paying interest, miss maturity, or the market gaps so violently that the basket cannot rebalance in time, which is the gap risk at the heart of this design.

## The math, and the numbers that decide everything

Take the simplest possible example, where your collateral is worth $100 and your loan is $70. Set the gap margin aside for this first pass so the floor sits at the debt of $70, which makes the cushion $30. Suppose you want to start fully in the volatile asset, so all $100 sits in BTC at origination. That choice sets your multiplier, because risky exposure = m × cushion, so $100 = m × $30, which means m ≈ 3.33. In the real design the floor sits a little above the debt, which shrinks the cushion and raises the multiplier needed for the same starting exposure, but the mechanism is identical.

That multiplier is not a cosmetic setting but the entire risk profile of the loan, and it is governed by the well known gap risk property of CPPI. It does two jobs at once, setting how much of your collateral starts in the volatile asset, which is m times the cushion capped at the whole position, and setting the size of gap you can survive between rebalances, which is 1/m. With m ≈ 3.33 that gap is 30%, so the loan defends its floor against any drop up to 30% that happens gradually enough to rebalance through, and it breaks the floor on a gap larger than that before the basket can react. A more conservative borrower who picks m = 2 starts at only 60% in the volatile asset, since exposure is 2 × $30 = $60, putting the other $40 in stablecoin from the start, which buys a wider 50% gap tolerance in exchange for upside. An aggressive borrower who picks m = 5 also starts fully in BTC, since 5 × $30 = $150 is capped at the $100 they hold, but the higher multiplier de-risks the basket faster once price slips and tightens its gap tolerance to 1/m, or 20%. This is the primary dial, a single and legible number that lets a borrower choose how much downside protection they are buying with how much forgone upside, and later the floor gives a second dial for how large a safe reserve to keep, neither of which any onchain lending protocol currently exposes.

This is also where I refuse to oversell the idea, because CPPI has a famous and instructive failure mode. The portfolio insurance strategies blamed for amplifying the Black Monday crash on 19 October 1987 were the synthetic put, dynamic hedging programs that sold index futures into the decline and created a feedback loop. Reputable post mortems, including the Brady Commission, treat portfolio insurance as having amplified the crash rather than caused it, and on that day portfolio insurers were roughly 40% of non market maker futures selling. Strictly speaking CPPI was not the named culprit, since the 1987 programs were the option replication variety, but CPPI shares the same de-risk into declines reflex and the same gap risk. The lesson is not that the mechanism is broken, but that gap risk is real, that you must set the multiplier with respect to how violently the asset can move between rebalances, and that you cannot rebalance through a true discontinuity.

## This is live, working machinery in traditional finance

Far from dying in 1987, CPPI is alive and widely used, one of the standard engines behind capital-protected products. Those products are a large corner of traditional finance, with structured-product sales hitting a record near $1.4 trillion in 2024 by Structured Retail Products' count, and CPPI issuance specifically was making a comeback that year, which makes it current practice rather than a museum piece.

What matters for us is that traditional finance has spent decades learning to tame CPPI's gap risk, by keeping the multiplier conservative, charging a premium for guaranteeing the floor, overlaying options on the underlying, and rebalancing often enough that gaps stay small. That is exactly the toolkit a protocol would inherit, and it is the same gap risk that showed up onchain, in public, in the protocol that pioneered soft liquidation.

## What the honest version costs

If I am proposing this, I owe you the downsides in full, because they are not hypothetical, and there are three of them:

1. The bleed comes from trading the basket back and forth, because continuously selling the volatile asset on the way down and buying it back on the way up is, mechanically, selling low and buying high, and it erodes value whenever the price chops sideways inside the rebalancing range. Curve documents this directly for crvUSD and is admirably blunt that the loss is hard to quantify, because it depends on the number of bands, the speed of the move, and how deep the collateral's liquidity is. Their own worked example, for a position that spent more than half its life in soft liquidation, shows a loss of 6.37%, and they note that the erosion accrues both on the way down and on the way back up while you are in range. A CPPI loan inherits exactly this convexity cost. You are, in effect, short volatility, and you pay for the floor protection in whipsaw.

2. Forgone upside follows, because a position that de-risks near the bottom and only partially rebuys on the recovery has sold its dip. The borrower trades the chance to ride a full rebound for the certainty of not being liquidated. That is a real trade, and some borrowers will not want it. The sharpest version of this cost is cash lock, the point where the basket has fully de-risked into USDC and the cushion is zero, so even a sharp rally cannot rebuild the position and its upside is frozen. In a perpetual fund that state is close to permanent, but in a loan it is an exit ramp rather than a trap, because the borrower can top up collateral to inject fresh cushion and re-risk, or simply sit safely in USDC just above the debt and repay at maturity, and a borrower who wants more room can set a higher floor up front, so the locked position parks well above the debt, a choice I come to in the build section.

3. Gap risk is the one that matters most, and it is the most concrete of the three. Soft liquidation is a buffer, not a guarantee, and crvUSD still keeps a hard liquidation backstop that closes the position if health reaches zero. We saw why on 10 October 2025, when the crash produced roughly $19 billion of liquidations across crypto in a single day, the largest on record. Curve's CRV long LlamaLend market could not rebalance fast enough through that gap, and it was left with about $700,000 of bad debt, backed at roughly 70% of stated value, with a market based recovery proposed in April 2026. This is not a reason to abandon the design, but rather the proof that any honest CPPI loan must ship with a hard liquidation backstop and a funded reserve for the gap that the math cannot rebalance through.

## Why this belongs onchain, and why it can bring fresh capital

The core of the argument turns on shape rather than magnitude, because a CPPI loan does not promise to be safer than holding the bare asset, and what it changes instead is the way the risk is shaped, converting a discontinuous, all at once liquidation cliff, complete with a penalty, into a continuous, smaller, more predictable cost that you can see coming and price in advance.

That shape is precisely what risk averse capital is built to buy. The entire capital protected product industry exists because a very large pool of money will accept lower expected upside in exchange for a defended floor and no sudden holes. Onchain lending has, so far, offered that pool almost nothing except a liquidation cliff, whereas a loan whose collateral defends its own floor is the onchain expression of a product structure that this capital already understands and already allocates more than $1 trillion a year toward.

It also widens what you can safely borrow against, because volatile collateral is dangerous in a hard liquidation world where a single wick is fatal, whereas in a CPPI world the collateral self hedges as it approaches the floor, which makes a long tail of volatile assets more usable as collateral at a given level of lender safety, as long as the multiplier is set with respect to how violently each asset can gap.

## How a protocol could actually build this

I would build it as an isolated lending market, in the spirit of the minimal, immutable market designs the category has converged on, with four pieces.

One choice sits above those four pieces, which is the interest rate. CPPI is independent of how the rate is set, so it can sit on top of either a variable rate or a fixed one, and a variable-rate version is entirely valid and worth building. The version I am proposing pairs it with a fixed rate and a fixed maturity, because that completes the one quadrant nobody has built, a loan that is both fixed rate and self-defending, and it most closely mirrors the capital-protected products this idea borrows from.

1. The collateral is held as a CPPI managed basket of the volatile asset and a stablecoin, not as pure volatile collateral. The borrower picks the multiplier at origination, which is the product. A conservative borrower picks a low multiplier and starts with more stablecoin and a wider gap tolerance. An aggressive borrower picks a high multiplier and keeps more upside and more gap risk.

2. A rebalancing engine moves the basket as the cushion changes. You can do this the LLAMMA way, by quoting prices that pay arbitrageurs to rebalance for you, or with an explicit keeper network executing through a batch auction or a CoW style settlement to blunt MEV and slippage, priced off a robust, manipulation resistant oracle. Rebalance frequency is a real parameter, since rebalancing more often shrinks gap risk but raises the whipsaw bleed, and that tradeoff should be tuned per collateral asset.

3. You set the floor above the debt rather than on it, and you keep a hard liquidation backstop in the band between them. The floor sits higher because the rebalancing swaps are neither instant nor free, so slippage or a fast move can carry the collateral through the floor before the basket has finished converting to USDC, and if the floor were the debt itself that overshoot would land below the debt and create bad debt directly. By placing the floor at the debt plus a modest margin, the basket is fully de-risked into USDC by the time collateral reaches that floor, and the space down to the debt is a protective band.

4. That band is also where the liquidator incentive lives, because if collateral pierces the floor despite the de-risking, the hard backstop fires inside the band while the collateral still exceeds the debt, so a liquidator closes the position and takes a bonus out of the remaining margin, the lender is still made whole, and bad debt only occurs if price gaps clean through the band below the debt. The margin should be modest, since a wide one de-risks too early and bleeds more upside, so its size is tuned to expected slippage and how violently the asset can gap. You also fund a reserve for residual bad debt out of a spread charged to borrowers, which is the onchain analog of the gap risk premium a structured products desk already charges for guaranteeing a floor.

5. You grow it the way this kind of risk shape wants to grow. Start with blue chip collateral and conservative multipliers, where gap risk is smallest and the floor is most defensible. Target the capital that wants yield without a liquidation cliff, which is treasuries, DAOs, and the more conservative end of allocators, and let curators build vaults on top that package specific multiplier and collateral policies for specific risk appetites. The TVL story here is not degens chasing a number, but patient capital that was never going to accept a liquidation cliff in the first place, finally being offered a shape it recognizes.

## TL;DR

- Onchain lending still mostly hard-liquidates, so one sharp wick can close a position that would have recovered days later.

- CPPI lending holds your collateral as a basket of the volatile asset and a stablecoin, and de-risks it toward a floor as your cushion shrinks, so the loan glides down instead of crossing a single liquidation line.

- The borrower's dial is the multiplier m, where risky exposure = m × cushion and 1/m is the gap it can survive, so a higher m keeps more exposure and less gap protection while a lower m does the reverse.

- Curve's crvUSD and f(x) already proved soft liquidation works onchain, and CPPI is a 40-year-old technique in traditional finance, so the new part is naming it, driving it off the cushion, and handing the borrower the dial.

- It is not free, since it carries whipsaw bleed, forgone upside, and gap risk that still needs a hard-liquidation backstop, so it reshapes risk rather than removing it.

- That smoother shape, a glide instead of a cliff, is exactly what conservative capital already buys in traditional finance, which is the real case for bringing fresh capital onchain.

If you build in this direction, or you think the gap risk kills it, I want to hear the argument. This is a proposal, not a product, and it gets better by being attacked.
