## Day 40 — NourishPath: AI Nutrition Strategy Assistant

**What I built:** A single-file HTML/CSS/JS app that turns a short user intake (goal, sex, age, height, weight, activity level, dietary pattern) into a personalized, prioritized nutrition strategy powered by the Claude API.

**Key pieces:**
- Deterministic BMR/TDEE/macro calculations (Mifflin-St Jeor) done in JS — Claude reasons on top of pre-computed numbers instead of doing arithmetic itself
- Strict JSON output contract from the system prompt (headline, ranked recommendations with priority + reasoning, closing note)
- Custom UI: dark summary card with macro bar, priority-tagged recommendation cards, empty/loading/error states
- Edge-case handling in the prompt: irrelevant notes ignored, medical conditions flagged toward a professional, disordered-eating signals shut off restrictive advice, calorie floor enforced, prompt-injection attempts declined

**Learning:** Reinforced that offloading deterministic math to code (not the LLM) and enforcing a strict JSON schema makes the UI far more reliable to build against.
