# Attribution method and conventions

## Scope and denominators

The ledger contains 38 closed option positions and 86 fill or expiry records from July–August 2025. Thirty positions are attributed, representing 94.13% of total opening premium. There are 24 losing positions overall; 18 have formal attribution and appear in the losing-trades chart.

Premium is the sum of actual opening purchases, quantity-weighted and including the contract multiplier. Whole-book figures divide by all 38 positions' opening premium; trade-level figures divide by that position's opening premium. P&L is gross option execution P&L, before fees and currency conversion effects. Fees are a separate −1.08% of total premium; after-fee P&L is −13.27%, before currency conversion effects.

The headline's “only net drag” refers to the three repricing factors. Residual, proxy-gap and unattributed items are also negative and remain separate. The 60% / 25% / 9% losing-trade figures divide the attributed losing positions' net factor contributions by gross losses across all 24 losing positions. The remainder includes residuals, proxy gaps and losses without attribution. These are different denominators from whole-book net P&L.

## Pricing and paths

All 30 formal position attributions use European Black-Scholes, with a fixed 4.3% rate, zero dividend yield and ACT/365F time to the configured expiry clock. CRR American pricing is used only in a historical UBER anchor comparison and convergence diagnostics; it is not mixed into the whole-book contributions.

| Path | Positions | Observations used |
| --- | ---: | --- |
| A | 5 | Intraday execution states |
| B | 21 | Execution states plus intervening daily closes |
| C | 4 | Daily closing proxies; executions reconciled separately |
| D | 7 | No separable market states; not attributed |
| E | 1 | Index option outside model scope; excluded from attribution |

Each adjacent pair of states is fully repriced in the fixed order **spot → vol → time**. Segment contributions are multiplied by the inventory actually held during that segment, then summed. This is not an entry-Greek Taylor expansion: spot includes nonlinear price effects, vol is not simply vega × change in IV, and time is not simply theta × elapsed time. Cross-effects depend on the sequence, generally entering the later repricing step. The formal results do not separately split delta and gamma or attribute rho.

## IV and observation quality

Execution-state IVs are solved from actual fills, paired with Massive underlying VWAP from the containing minute. Daily marks pair OptionMetrics IvyDB closing option bid/offer midpoints with the same source's underlying close. Path C uses closing proxies throughout; actual executions do not become calibration marks.

Points are screened for prices below intrinsic, insufficient time value and excessive relative quote width. If either endpoint is unidentifiable, IV is frozen at the last identifiable anchor known at the segment's start, and only spot and time are repriced. A newly identifiable endpoint anchors the following segment. No future IV is backfilled; zero vol contribution in a frozen segment is a convention, not evidence of unchanged market volatility. The record contains 106 calibration points, of which 96 are identifiable.

## Reconciliation and limits

For each modeled segment, **residual = observed mark P&L − spot − vol − time**. For closing-proxy paths, **execution P&L = spot + vol + time + residual + signed fill-to-close proxy gap**. The proxy gap combines timing and execution differences; it is not isolated slippage or IV error. Fees and currency effects are not folded into residual. Unattributed positions are retained separately.

Net residual is 6.98% of absolute whole-book gross net P&L. This is reconciliation, not predictive accuracy: fill-calibrated endpoint prices fit those same fills by construction. No independent, execution-time quote/IV error distribution was established for all 38 positions. Earnings, short maturities, deep-OTM quotes, omitted early exercise and closing proxies limit interpretation.

The waterfall uses unrounded saved aggregates with rounded labels. The losing-trades chart includes the 18 attributed losers, ordered by original gross loss without displaying amounts. Its four stacks show spot, vol, time and residual; dots show actual gross P&L. Proxy gaps are not stacked, so the stack's net need not equal the dot for a proxy-path trade. Both charts contain normalized results only.
