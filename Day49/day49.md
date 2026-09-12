Day 49: Personal AI Playbook

Built a single-file HTML/CSS/JS app that turns repetitive network 
engineering and ITSM tasks into reusable AI prompt workflows.

Features:
- Dashboard with starter workflows (VLAN config, incident summaries, 
  RCA, firewall checks, stakeholder emails, study plans)
- Prompt Builder: assemble prompts from modular blocks (role, objective, 
  context, constraints, reasoning strategy, output format, tone, 
  examples, quality checks) with live preview
- Loop Builder: converts a prompt into a self-checking, iterative 
  loop (goal, evaluation criteria, improvement strategy, stop 
  conditions, safety rules)
- Full CRUD on saved workflows: search, filter, favorite, duplicate, 
  edit, delete — all via localStorage
- Dark/light mode, keyboard shortcuts, JSON import/export, 
  first-run onboarding

Stack: Vanilla HTML/CSS/JS, no external libraries.
