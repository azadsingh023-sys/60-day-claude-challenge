Day 45: AI Decision Strategist

Theme: Think Better. Decide Smarter.

What I built: An interactive AI-powered decision-support tool. It runs a 4-question interview (the decision & options, goal/timeline, gut instinct, biggest fear + reversibility) and generates a single-page HTML "Decision Report" dashboard covering:

The real decision & trade-off
Case for/against each option (upside, weakness, "best if you value")
Assumption Buster (hidden assumptions + named cognitive biases + blind spot)
Animated scored Decision Matrix (7 weighted dimensions)
Premortem for top 2 options
7-day real-world test plan
Final verdict + shareable summary cards

Key learning: Structuring a prompt as a strict, staged interview (one question at a time, no analysis until data collection is done) produces much sharper, more grounded output than asking an LLM to "analyze my decision" in one shot — the model can't rationalize toward a comfortable answer because it's forced to commit to a decisive verdict at the end, backed only by facts the user actually gave it.

Stack: Single-file HTML/CSS/JS, no dependencies, dark theme, CSS-only animations for the matrix bars.
