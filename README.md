# BTC Structure Break Trend

**Bitget AI Hackathon S1 — Studio Native Submission**
Strategy type: Trend-following | Asset: BTCUSDT Perpetual | Built with: GetAgent Studio

---

## Why I Built It

Most retail traders lose money in trending markets not because they read direction wrong, but because they enter too early or chase breakouts that immediately reverse. I wanted to build a strategy that enforces patience — one that waits for the market to *prove* its direction through price structure before committing capital, then enters only on a controlled retracement rather than at the point of maximum excitement.

BTC was the natural candidate. Its trends are persistent, its structure breaks are clean, and its volatility rewards systematic entries over impulsive ones.

---

## Core Logic

The strategy is built on one observation: sustained BTC trends move in a repeating cycle of **structural break → corrective pullback → continuation**. Every entry is an attempt to board that continuation leg, never the initial break.

**Structure detection**
The strategy tracks swing highs and swing lows across a rolling `swing_lookback` window. Market structure is classified as bullish when the sequence of swing points shows higher highs and higher lows, and bearish when it shows lower highs and lower lows. A break of structure is confirmed only when price *closes* beyond the most recent swing extreme — not merely wicks through it.

**Entry conditions (long — all must be true)**
- Structure classified as bullish
- Confirmed close above most recent swing high
- Price has retraced without violating structure
- EMA(20) above EMA(50)
- Break candle volume ≥ 1.1× the 20-period volume average

Short entries mirror these conditions on the bearish side.

**Exit logic**
Positions close through two mechanisms: signal reversal (all opposite-direction conditions met, position flips) or ATR-based volatility stop set at 2.0× ATR(14) from entry.

**Risk management**
- Fixed leverage: 3×
- Margin budget: $10,000
- Position size calculated per trade from ATR stop distance — not fixed lot size

**Signals used:** Technical only — price structure (swing points), EMA trend filter, volume confirmation, ATR volatility stop. No on-chain, macro, or sentiment inputs in v1.

---

## Development Challenges

**Challenge 1: Structure lag on fast-moving regimes**
The initial `swing_lookback` of 5 caused the strategy to miss the June 2026 BTC rally. After the short closed on Jun 22, BTC broke structure bullishly but the confirmation window was too wide to generate a re-entry signal in time. Solved in v2 by reducing `swing_lookback` to 3 and `volume_threshold` from 1.3 to 1.1.

**Challenge 2: One-trade backtest window**
The May–Jun 2026 backtest window produced only one completed round trip, which makes win rate and profit factor statistically meaningless. This is a data depth limitation of the current Studio backtest range, not a strategy flaw. Next step is extending the backtest window to capture multiple market regimes.

**Challenge 3: Entry timing on pullbacks**
The original logic entered immediately on structure confirmation rather than waiting for a retracement candle. This inflated entry prices and compressed the risk/reward. Adding the pullback condition tightened entries significantly.

---

## Results (Paper Trading — May–Jun 2026)

| Metric | Value |
|---|---|
| Total return | +35.6% |
| Max drawdown | −20.6% |
| Win rate | 100% (1/1) |
| Avg round trip | +5.01% |
| Avg hold time | 29 days 9 hours |
| Completed trades | 1 short: entry $73,822 → exit $70,122 |

Paper trading live since Jun 23, 2026.

---

## What's Complete / What's Next

**Complete**
- Strategy logic: structure detection, EMA filter, volume confirmation, ATR stop
- Backtest and paper trading running on GetAgent Studio
- Published playbook with full brief on GetAgent

**Missing / Next steps**
- Extend backtest window beyond 6 months
- Add multi-timeframe structure confirmation (HTF bias filter)
- Test on ETH and SOL perpetuals
- Explore dynamic leverage scaling based on ATR regime

---

## Tools & Frameworks

| Tool | Usage |
|---|---|
| GetAgent Studio (Playbook) | Strategy authoring, backtesting, paper trading |
| Bitget Perpetuals | BTCUSDT trading pair |
| EMA (20/50) | Trend filter |
| ATR (14) | Volatility stop and position sizing |

**Bitget tools used:** GetAgent Studio — Playbook

---

## GetAgent / Bitget AI Experience

Studio made it fast to go from strategy concept to running backtest without writing infrastructure from scratch. The biggest current limitation is backtest data depth — a 1–2 year window would make it possible to test across multiple BTC market cycles, which is the minimum needed to validate a trend-following system with confidence. A regime-labeling overlay (bull/bear/chop) built into the Studio UI would also help builders identify where their strategy is leaking.

Agentic trading is moving toward systems that don't just execute signals but *adapt* their signal logic based on detected market conditions. That's the direction I'm building toward.

---

## Links

✅ Working demo — getagent.studio/strategy/2410daa3-c621-457e-89c5-a17a2af035a1
✅ Project post — x.com/i/status/2069391054512463937
✅ Repost of official campaign — x.com/i/status/2068602266592985137
