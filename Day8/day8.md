# 🌍 Day 8 — AI-Powered Dashboard | 60 Days Claude AI Challenge

**Date:** August 2, 2026
**Project:** Personal Environmental Health Analyzer
**Tool used:** Claude AI (Artifacts)

---

## 🎯 Today's Task
Build a fully interactive, data-driven dashboard using Claude — from raw data to a working, shareable application — without writing code manually.

## 🛠️ What I Built
A **Personal Environmental Health Analyzer**: an interactive dashboard analyzing real-time AQI and water-quality data across 14 Indian cities, featuring:
- Live metric cards, 6 interactive charts (AQI, PM2.5, PM10, ranking, distribution, seasonal trend)
- Filters (pollutant, risk level, state, AQI range) + city comparison mode
- A personal environmental health report card with A–F grades
- Risk-based health insights (air → lungs/sleep/energy; water → hair/skin)
- Personalized daily recommendations

## 💡 Key Learnings
1. **Claude can act as a full product team** — researcher, data cleaner, UX designer, and frontend developer — in a single workflow, not just a code generator.
2. **Prompt structure matters more than prompt length.** Breaking the task into clear sections (data rules → analysis → dashboard → design → output) got a far more complete result than one long paragraph would have.
3. **Data honesty is a feature.** Claude flagged which values were live vs. estimated instead of quietly guessing — a good reminder to always ask for source transparency in AI-generated analysis.
4. **Design and logic are separable asks.** Specifying tone (dark, premium, mobile-responsive) separately from functional requirements (filters, charts, scoring) produced a cleaner, more intentional UI.
5. **Iteration through instructions works better than manual edits.** Refining scope via natural language (e.g., "no code snippets, full working artifact") shaped the output more reliably than trying to fix it after the fact.

## 🚧 Challenges
- Balancing a **feature-rich brief** (5+ chart types, 6 filters, health scoring, recommendations) with a clean, non-cluttered UI.
- Making sure real-world data (AQI/water quality) was **researched, cited, and clearly labeled** rather than fabricated.

## 🔜 Next Steps
- Explore connecting this dashboard to a live API for real-time refresh instead of a static snapshot.
- Try Claude for a second data domain (e.g., finance or fitness tracking) to compare workflow differences.

<img width="2264" height="1586" alt="image" src="https://github.com/user-attachments/assets/8dd97345-8b1d-4205-aa9e-1c0ba1c047a2" />

