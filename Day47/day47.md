## 🚀 Day 47/60 – Content Intelligence Studio
### Build an AI-Powered Content Analysis Platform

Today's build: an AI content consultant that reviews social posts the way a newsroom panel would — not with a single generic AI score, but through a **team of specialist reviewers**, each with a production-grade system prompt, running live against the Claude API.

### 🧠 What it does
- Takes a LinkedIn/X post (text, optionally + screenshot/image) as input
- Spins up a dynamic **review desk** of 5–6 specialist AI reviewers:
  - Hook & Opening Line Analyst
  - Structure & Readability Editor
  - Engagement Psychology Strategist
  - Platform Fit & Algorithm Specialist
  - Message Clarity Reviewer
  - Visual Content Analyst *(when an image is attached)*
- Synthesizes every reviewer's output into one editor-in-chief report

### 📊 What you get back
- Overall content health score + category breakdown
- Strengths, weaknesses, missed opportunities
- Top 3 highest-impact improvements
- Platform-specific recommendations
- A ready-to-publish **rewrite**, alternative hooks & titles
- Publishing checklist, before/after comparison
- AI-estimated reach/engagement/shareability potential (clearly labeled as an estimate, not a guarantee)
- Follow-up prompts to go deeper

### ⚙️ Build notes
- Single self-contained HTML file — vanilla JS, no frameworks, no libraries
- Live calls to the Claude Messages API — zero hardcoded logic, no canned feedback, no placeholder scoring
- Strict plain-text response contract (no JSON) to eliminate parsing/formatting errors
- Dark-mode "editorial desk" UI: live reviewer status, activity log, animated score rings, retry/error handling
- Interview-first UX (MCQ-driven) before the actual analysis runs

### 💡 Takeaway
Multi-agent review panels > single monolithic prompts. Splitting judgment into narrow, specialized reviewers produces sharper, more defensible feedback than asking one model call to "grade everything at once" — and it mirrors how a real editorial team actually works.

**#60DaysOfClaude #ClaudeAI #BuildInPublic #AI #ContentStrategy #IndieHacker**
