# BTC Structure Break Trend

> A transparent, rule-based trend-following strategy for BTC perpetual futures — no black box, no guesswork.

---

## Overview

**BTC Structure Break Trend** is a price-action system that captures directional moves in Bitcoin by reading swing-point structure and waiting for confirmed breaks. It was built as a signal source for traders who want to understand *why* every trade is taken, not just that it was taken.

The core thesis: sustained BTC trends unfold through a repeating sequence of **structural breaks → corrective pullbacks → continuation**. This strategy identifies that cycle in real time and enters only when a confluence of conditions confirms the move is real.

Live on **Bitget Studio** (Playbook) · Paper trading since Jun 23, 2025 · Symbol: `BTCUSDT`

---

## Performance (Paper, May–Jun 2026)

| Metric | Value |
|---|---|
| Total Return | +35.6% |
| Max Drawdown | −20.6% |
| Win Rate | 100% |
| Profit Factor | ∞ |
| Avg Round Trip | +5.01% |
| Round Trips | 1 |
| Avg Hold Time | 29d 9h |

### Closed Trade
- **Direction:** Short  
- **Entry:** May 23 @ $73,822.48  
- **Exit:** Jun 22 @ $70,122.50  
- **Return:** +5.01% | P&L: +$3,559.84 over 29 days

---

## How It Works

### Entry Logic

**Long — all must be true simultaneously:**
1. Market structure is classified **bullish** (pattern of higher highs and higher lows confirmed in recent swing points)
2. A **bullish break of structure** is confirmed: price has closed above the most recent swing high
3. EMA fast (20) is above EMA slow (50)
4. Volume on the breakout candle exceeds 1.3× the 20-period average
5. Price has retraced to a qualifying level after the structural break

**Short — mirror conditions:**
1. Bearish structure (lower highs and lower lows)
2. Confirmed bearish break of structure
3. EMA fast below EMA slow
4. Volume confirmation
5. Qualifying retracement entry

### Exit Logic

Positions close via two mechanisms:

- **Signal Reversal** — when all entry conditions for the opposite direction are met, the current position closes and a new one opens in the reverse direction
- **Volatility Stop** — ATR-based stop loss (2× ATR, 14-period) prevents excessive loss on gap-driven or whipsaw moves

---

## Parameters

| Parameter | Value | Description |
|---|---|---|
| `ema_fast` | 20 | Fast EMA for trend bias |
| `ema_slow` | 50 | Slow EMA for trend bias |
| `swing_lookback` | 5 | Candles used to detect swing highs/lows |
| `volume_avg_period` | 20 | Lookback for volume baseline |
| `volume_threshold` | 1.3 | Minimum volume multiplier for entry |
| `atr_period` | 14 | ATR lookback for stop calculation |
| `atr_sl_mult` | 2.0 | ATR multiplier for stop distance |
| `leverage` | 3× | Futures leverage |
| `margin_budget` | $10,000 | Capital allocated per signal |

---

## Known Weaknesses

This strategy is designed for honest disclosure, not just marketing. It can underperform in:

- **Choppy, range-bound markets** — without a clear trend, structural reads flip rapidly and whipsaw losses compound
- **Gap-driven moves** — sharp overnight or news-driven gaps can breach stops before execution
- **Low-volume conditions** — the volume threshold filter may delay entry or cause missed moves in thin markets

---

## Built With

- **Bitget Studio** — Playbook deployment and paper trading
- **Bitget Agent Hub** — strategy monitoring
- Price-action methodology: classical swing structure analysis (no ML, no black-box model)

---

## Hackathon Submission

This project was submitted to the **Bitget AI Hackathon S1** under the Trading Agent category.

**Why it was built:** Most retail crypto traders either chase price or follow signals they don't understand. This playbook gives subscribers a verifiable, rule-based system they can audit trade-by-trade — every entry and exit has a documented reason.

**What's next:**
- Extend backtest window across multiple market regimes (2022 bear, 2023–2024 bull)
- Add a range-detection filter to pause signals during low-volatility consolidation phases
- Explore multi-timeframe confirmation for higher-conviction entries

---

## Author

**chiamakaclaire99** · Bitget Studio  
Strategy published Jun 23, 2026
