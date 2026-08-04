# Day 10 / 60 — Building a Personal Portfolio Website with Claude

## 🎯 Objective
Explore how far Claude can go with a single, detailed prompt — generating a complete, production-ready personal portfolio website from a resume and a photo, with zero manual coding.

## 🧠 What I Did
1. Uploaded my CV (`.docx`) and a profile photo.
2. Gave Claude a structured prompt describing the sections I wanted: Hero, About, Skills, Projects, Achievements, Contact.
3. Asked for a single-file build — HTML + Tailwind CSS (CDN) + vanilla JS — with dark/light mode, animations, and mobile responsiveness.
4. Claude read the CV, extracted real experience and skills, embedded the photo, and generated a complete themed website in one pass.

## 🛠️ Tech Stack Used
- HTML5
- Tailwind CSS (via CDN — no build step)
- Vanilla JavaScript
- Google Fonts (Space Grotesk, Inter, JetBrains Mono)
- Single self-contained `.html` file (image embedded as base64)

## ✨ Key Features Generated
- Typing animation cycling through role titles
- Dark/light mode toggle with persistent styling
- Scroll-triggered reveal animations
- Animated skill bars
- Active nav-link highlighting on scroll
- Fully responsive layout (mobile → desktop)
- SEO meta tags (title, description, Open Graph)
- Contact form + direct email/phone/LinkedIn links

## 💡 What Surprised Me
- Claude didn't just template the content — it **read my actual CV** and turned 12+ years of ITSM/network engineering experience into recruiter-friendly copy, instead of generic placeholder text.
- The whole thing — layout, copy, animations, and photo integration — was ready in a few minutes.
- The design avoided generic "AI-look" defaults (no cliché cream/terracotta or stock dark+neon themes) and instead used a NOC/incident-log visual language that actually fit an IT operations profile.

## 📚 Prompting Lesson Learned
> The more structured and specific your prompt (sections, design preferences, content blocks), the closer the first draft lands to something usable — almost no back-and-forth needed.

Giving Claude clear **inputs** (uploaded files) + a clear **output structure** (section list) is far more effective than a vague one-liner like "build me a portfolio site."

## 🔗 Resources
- [Claude.ai](https://claude.ai)
- [Tailwind CSS](https://tailwindcss.com)

---
📌 Part of my **#60DaysOfClaude** challenge — daily hands-on exploration of Claude's capabilities.
