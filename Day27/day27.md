Day 27: Prior Authorization Story Simulator

Built a single-file, chat-style narrative simulator that explains 
US healthcare Prior Authorization through Rahul's (patient) journey, 
guided by Priya (healthcare ops specialist).

- 8 scenes: Doctor Visit → Insurance Roadblock → What is PA? → 
  Insurance Review → Denial → Appeal → Approval → Takeaways
- Chat bubbles built entirely with createElement + appendChild 
  (no innerHTML on the chat container)
- Rahul (left) and Priya (right) as chat bubbles; Dr. Patel and 
  narrator lines as centered italic text
- Branching choices after every scene affect dialogue and pacing
- Cited real data points: AMA 2023 PA Survey, staff-hours-per-denial stat
- Provider → Payer PA flow (no pharmacy step) explicitly modeled
- Dual takeaway summary: Patient perspective + System perspective 
  (denial rate, appeal rate, resolution time)
- Progress bar tracking scene 1-8
- Fictional "StarCare Health" labeled throughout as an illustrative example payer

Tech: HTML, Tailwind CSS (CDN), vanilla JS only — single self-contained file.
