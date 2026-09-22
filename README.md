# Execution & TCA Engine — Research Dashboard

A post-trade **transaction-cost analysis (TCA)** engine that decomposes a parent order's cost into its five
Implementation-Shortfall components and **closes the books on every order**. This repository hosts the
**dashboard sample only**.

**[Open the dashboard](https://supernicole.github.io/execution-cost-decomposition-dashboard/)** — a single self-contained HTML file (open it directly, no server needed).

---

## Scope — read this first

- This is a **research-grade demonstration**, not a live or production system, and **not a track record**.
- **Market data is real** (Sina / A-share, via akshare). **The order flow is model-generated** — real fills
  and quotes were not available, so the parent orders and their child fills are produced by a generator,
  with embedded costs in the fill prices. This is stated on the dashboard itself.
- The dashboard is shown to demonstrate an **analysis pipeline** — how execution cost is measured,
  attributed and defended — not to present performance.

## How to read the dashboard

| Pane | What it shows |
|---|---|
| Market and order-window panes | The context an order executed into (1-minute candles, volume, order window) |
| Child-order detail | Every child fill, so a parent order's cost can be followed fill by fill |
| Cost decomposition | The five Implementation-Shortfall components per order |
| Waterfall | The components tied back to the total — the books close, or the run does not stand |
| Impact model | The market-impact calibration and its fit |
| Reports / export | The per-order and aggregate output |

## Design notes

- **The method is validated before the output is trusted.** A known impact coefficient is embedded in the
  simulated fills and then recovered by the same estimator the engine uses — an embed → attribute →
  recover loop. Numerical self-checks (closed-form vs. tridiagonal first-order conditions vs. Monte Carlo)
  confirm the components agree to a tight tolerance.
- **No look-ahead.** The estimator is calibrated before it is pointed at anything unknown; guardrails run
  throughout.
- **Per-order book closure.** Every basis point of a parent order's cost is accounted for by construction.

## Source code

The engine source is not published here. This repository is the demo layer only.
