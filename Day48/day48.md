Day 48: Compare & Decide Builder

Goal: Build a research-backed, interactive decision tool comparing project management platforms for a company-wide rollout.

What I built:

Interviewed by Claude (MCQ-style) on category, audience, decision criteria, sourcing preference, and weighting model
Compared Jira, Asana, monday.com, and ClickUp across 4 criteria: Ease of Use, Security & Compliance, Scalability, Support Quality
Live weight-adjustable ranking engine (vanilla JS, no libraries)
Sources panel citing G2, Atlassian Trust Center, Asana Trust Center, monday.com Compliance Hub, ClickUp Security Policy
Collapsible "How this was researched" panel — flags every estimated/synthesized score vs. directly-sourced metric, and documents a source conflict (ClickUp's ease-of-use score)

Stack: Single-file HTML/CSS/JS, no external dependencies

Key learning: Forcing explicit "estimate" vs "sourced" flags in the data model made the output far more trustworthy than a generic comparison — and surfaced a real disagreement between sources instead of hiding it.
