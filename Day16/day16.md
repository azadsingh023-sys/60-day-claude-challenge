## Day 16 — Fundamental Stock Research with Claude

**Goal:** Test Claude as a fundamental equity research assistant using a custom skill.

**What I built/ran:**
- Used a custom `stock-fundamental-research` skill to analyze **Reliance Industries (RELIANCE)**
- Generated a **Quick Take** (valuation, D/E, ROE/ROCE, growth trend, strengths/watch-points)
- Escalated to a **Deep Dive**: interactive HTML report with 8 tabs — Snapshot, Valuation, Growth, Health, Returns, Peers, Ownership, View
- Charts included: revenue/profit trend, quarterly EPS, OPM% trend, borrowings vs FCF, ROCE trend, peer P/E comparison, shareholding mix, FII/DII trend

**Key learnings:**
- Claude cross-checked data across multiple sources (Screener, TipRanks, MarketsMojo) and explicitly flagged where peer/sector figures disagreed instead of presenting a false-precision number
- The skill enforced guardrails automatically — no buy/sell/hold calls, every figure sourced
- Good example of a domain-specific skill turning a generic LLM into a repeatable, structured research workflow

**Output:** Interactive HTML dashboard (Chart.js) — not shared publicly due to financial content, available on request.

**Tomorrow:** Day 17 — TBD
