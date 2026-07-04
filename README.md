# Structural Support & Resistance for Argentine Equities

A structural analysis engine that detects horizontal support/resistance zones on
equities using swing structure and real volume, and publishes daily updated
charts for the Argentine market (BYMA / Merval).

This repository is **descriptive**: it documents the method and shows example
output. The engine itself is proprietary.

🔗 **Live charts (daily, in Spanish):** [jlpgraficos.com.ar](https://jlpgraficos.com.ar)

---

## What it does

Given OHLC + volume data, the engine builds a map of the levels where price has
historically found support or resistance, and how many times each level has been
respected.

The pipeline has two conceptual layers:

1. **Swing detection** — a single-pass state machine identifies confirmed highs
   and lows. Each extreme carries a **confirmation date**: the date on which it
   became known, not the date it occurred.
2. **Level clustering** — nearby swings are grouped into zones using an
   ATR-based distance criterion, so the output is a small set of meaningful
   zones rather than noise.

## What makes it different

Most open-source support/resistance tools draw levels using data from the
**future** without noticing — a level looks valid because the chart already
shows how price reacted to it.

This engine tracks a **confirmation date** for every extreme, which allows an
**as-of query**:

> *"Which levels existed on date X, using only what was known up to X?"*

The answer is honest — no lookahead. For anyone doing backtesting or studying
whether a method actually had an edge in real time, this is the property that
matters, and it is rarely handled correctly.

## Example output

*(Charts show levels that were already in place before price reacted to them.)*

![Example 1](examples/example_01.png)
![Example 2](examples/example_02.png)
![Example 3](examples/example_03.png)

> Drop your exported chart PNGs into `examples/` and update the paths above.

## Scope & honesty

- The levels are **descriptive**: they mark where price has reacted before.
- Turning that into a live entry mechanic — *when* a level becomes tradable — is
  ongoing work and is intentionally **not** part of this public repository.
- Nothing here constitutes financial advice.

## About

Built and maintained by an electromechanical engineer and active trader in the
Argentine market, as the engine behind [jlpgraficos.com.ar](https://jlpgraficos.com.ar).

Open to interesting conversations — feel free to reach out via GitHub.
