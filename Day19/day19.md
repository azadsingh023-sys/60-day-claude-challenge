## Day 19/60 — Football Intelligence Hub

**Date:** [add today's date]

**What I built:**
A multi-stage Football Intelligence system powered by an Excel workbook as the data backbone. Claude acts as analyst, quiz master, and personality assessor across 3 stages:

- **Stage 1 — Prediction Report:** Analyzes historical performance, current contender form, and live 2026 World Cup group-stage results to predict winner/runner-up/dark horse with confidence scores, evidence, and risks.
- **Stage 2 — Football IQ Quiz:** Adaptive 5-question quiz (beginner → advanced) scored into a Football Awareness classification.
- **Stage 3 — Messi vs Ronaldo Personality Match:** Trait-based quiz (ambition, leadership, creativity, etc.) mapped to compatibility % with each legend + a football personality archetype.

**Key learning:**
- Structuring a single workbook as a multi-table data source Claude can reason across (historical stats, live results, user-input trait tables)
- Designing a staged, adaptive conversational flow that adjusts depth to the user's stated expertise level
- Using scoring/classification logic to turn open-ended answers into a structured "profile" output

**Tools:** Claude (chat), Excel workbook as data source
