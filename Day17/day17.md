## Day 17 — E85 Paradox Fuel Cost Dashboard

**Goal:** Analyze a 53-record fuel dataset (CNG, Diesel, EV, Petrol E20, E85) and 
build a single-file HTML dashboard comparing real running costs.

**What it does:**
- Groups data by fuel type, computes Cost/km, CO₂/km, Maintenance/km, avg refuel/recharge time
- Breaks down Cost/km & Maintenance/km by vehicle age bucket (New / Mid-life / Aged / Old)
- Surfaces the "E85 Paradox": 18% cheaper pump price vs Petrol, but 3.6% higher cost/km 
  due to lower mileage — break-even pump price calculated at ₹79.1 (E85 sells at ₹82)
- Scores E85 out of 10 (cost 4pt / CO₂ 3pt / refuel 2pt / maintenance 1pt weighting)
- Personal vehicle callout: Tata Tiago EV — ₹1.75/km, cheapest & lowest-maintenance 
  fuel type in the dataset, ~₹1,051/month at 600 km usage

**Tech:** Pure HTML/CSS/JS, hand-built SVG charts (bar, doughnut, line, animated gauge) — 
no chart libraries. Dark navy glassmorphism UI, responsive 375px–1440px.

**Files:** `day17_e85_dataset_optimised.csv`, `day17_dashboard.html`
