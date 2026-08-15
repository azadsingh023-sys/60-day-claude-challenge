## Day 21 — Digital Footprint & Privacy Dashboard

**Goal:** Explore how Claude can turn a simple list of apps into a structured, transparent privacy-analysis dashboard — without ever pretending to have real personal data.

**What I built:**
A single-file interactive HTML dashboard that takes a "digital footprint" (15 reported apps — Instagram, WhatsApp, Google Pay, Amazon, Roblox, etc.) and generates:
- Digital Footprint Score & Privacy Score (0–100, color-coded)
- Exposure Heatmap (category × data-type)
- Company Exposure Ranking (parent-company concentration)
- Data Collection Matrix
- Risk Radar (SVG, 6 exposure dimensions)
- "Digital Twin" inferred profile
- Most Valuable Data Assets ranking
- Live Privacy Improvement Simulator (toggle actions → score updates in real time)

**Key constraint I designed for:** every output had to be explicitly labeled **Fact** vs **Estimate**, with no claims of certainty and no implication of accessing real private/company databases. This turned into a good exercise in prompt-level guardrails, not just UI design.

**Stack:** Vanilla HTML/CSS/JS, SVG for the radar chart, dark "cybersecurity ops" visual theme (Space Grotesk + Inter + JetBrains Mono).

**Takeaway:** Claude handles nuanced, rule-bound output generation (facts vs. inference, privacy framing) well when the boundaries are spelled out explicitly in the brief — the constraints did more design work than the styling did.

`#60DaysOfClaude` `Day 21/60`

---

Want me to tweak the tone (more casual / more technical) or shorten either one further?
