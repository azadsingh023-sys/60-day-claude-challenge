# NetVault — Implementation Blueprint (Days 2–10)

**Project:** NetVault — a local, dashboard-first network inventory tool for tracking switches, VLANs, ports, and sites.
**Builder profile:** Total beginner to coding. 30–60 minutes/day available. No prior project shipped.
**Tech stack (locked — do not change mid-build):** Plain HTML + CSS + JavaScript, single page, no framework, no backend server. Data is stored in the browser using `localStorage`, seeded from a bundled `data.js` sample dataset (100+ switches across multiple sites). Optional CDN library: Chart.js (for one simple chart) — free, no install, no signup.
**Deployment target:** Runs locally by double-clicking `index.html` (or via VS Code "Live Server" extension). No hosting, no cloud account, no cost. Demo is a screen recording.
**Repo:** Same GitHub repo already used for the "60 Days of Claude" challenge — this project lives in its own subfolder, e.g. `/netvault`.

> **How to use this document:** Each day below is self-contained. At the start of each day, start a **new AI chat**, paste that day's section in full, and say "Let's start Day X." The AI should not need to ask you to re-explain the project — everything it needs is in that day's block plus the "Project Context" section right below.

---

## Project Context (paste this at the top of every new day's chat if the AI seems to need it)

- **Product:** NetVault — single-page local web app for network inventory tracking.
- **Core entities:**
  - `Switch`: `id`, `name`, `ipAddress`, `site`, `location` (e.g. rack/room), `model`, `portCount`, `vlans` (array of VLAN IDs assigned on that switch), `status` (Active/Inactive/Maintenance), `notes`, `lastUpdated`.
  - `VLAN`: `id` (VLAN ID number), `name`, `description`.
  - `Site`: just a string list for now (e.g. "Main Campus", "Library Block", "Hostel Block", "Admin Building") — not a full object in v1.0.
- **Views:** (1) Dashboard — summary cards + one chart. (2) Inventory Table — searchable/filterable list of all switches. (3) Add/Edit Switch — a modal form. (4) Export/Import — JSON backup/restore buttons.
- **Explicitly OUT of v1.0 (do not build, do not suggest):** user accounts/login, multiple permission levels, live SNMP/device polling, real-time alerting, config version history, cloud hosting, mobile app, database server of any kind.
- **File structure (final, do not restructure):**
  ```
  /netvault
    index.html
    /css
      style.css
    /js
      data.js        (sample seed data)
      storage.js      (load/save to localStorage)
      render.js       (draws dashboard + table)
      filters.js      (search/filter logic)
      crud.js         (add/edit/delete logic)
      app.js          (wires everything together, runs on page load)
    /assets           (icons/images if any — optional)
    README.md
  ```

---

## Day 2 — Setup: Environment & Confirmed Architecture

🎯 **Objective:** Get a working development environment and a "Hello World" version of the app running locally, proving the whole toolchain works before any real feature is built.

📖 **What I'll learn:** How a web project's files relate to each other (HTML/CSS/JS), what a code editor is, how to open a local file in a browser, and (optionally) how to use a "Live Server" so changes auto-refresh.

🛠 **Features to build:** None yet — this is pure setup. Output is a blank page that says "NetVault is running."

📝 **Step-by-step implementation plan:**
1. Install [Visual Studio Code](https://code.visualstudio.com/) (free) if not already installed. This is your code editor for the rest of the project.
2. In VS Code, install the extension "Live Server" (by Ritwick Dey) — lets you preview HTML changes instantly in a browser.
3. Create the folder structure exactly as shown in "Project Context" above.
4. Create `index.html` with a minimal skeleton: `<html><head><title>NetVault</title></head><body><h1>NetVault is running</h1></body></html>`.
5. Right-click `index.html` in VS Code → "Open with Live Server." Confirm it opens in your browser and shows the heading.
6. Create empty placeholder files for all the `.js` and `.css` files listed in the structure, and link them in `index.html` (`<link>` for CSS, `<script>` for JS) — even though they're empty, confirm no errors appear in the browser console (View → Developer Tools → Console).
7. Initialize a git repo in this folder (or a subfolder of your existing 60-day-challenge repo) and make your first commit: "Day 2: project scaffold."
8. Push to GitHub.

📂 **Files/folders created:** entire folder structure above, all files empty except `index.html` skeleton and empty linked files.

🔗 **Tools:** VS Code, Live Server extension, Git, GitHub (already set up from the challenge).

🧪 **Testing tasks:** Open browser console — zero errors. Confirm Live Server auto-refreshes when you save a change to `index.html`.

🐞 **Common issues:**
- Blank page / 404: check the file paths in your `<link>`/`<script>` tags match the actual folder names exactly (case-sensitive on some systems).
- Live Server not appearing in right-click menu: restart VS Code after installing the extension.
- Console shows "Failed to load resource": a `<script src="...">` path is wrong — check spelling and folder slashes.

✅ **End-of-day checklist:**
- [ ] Folder structure created exactly as specified
- [ ] `index.html` opens via Live Server and shows heading with zero console errors
- [ ] All empty JS/CSS files linked correctly
- [ ] Git repo initialized, first commit pushed to GitHub

📸 **Expected state / screenshot to capture:** Browser window showing "NetVault is running," VS Code file explorer showing the full folder tree, and the empty browser console (as proof of zero errors).

➡️ **Handoff notes for Day 3:** Folder structure and empty files exist. Nothing renders yet except a heading. Day 3 replaces the heading with the real page skeleton (dashboard area + table area + nav) and adds base CSS — still no real data.

---

## Day 3 — Design: Page Skeleton, Data Model & Styling Foundation

🎯 **Objective:** Build the static visual skeleton of all three views (Dashboard, Inventory Table, Add/Edit form) with placeholder content, and finalize the exact JavaScript data shape for a Switch and a VLAN.

📖 **What I'll learn:** How HTML sections/divs form a page layout, how CSS classes control appearance, and how to plan a JavaScript data structure (`object` and `array`) before writing logic against it.

🛠 **Features to build:** Static, non-functional layout only — top nav/header, a "Dashboard" section with 4 empty summary card placeholders, an "Inventory" section with an empty table (headers only: Name, IP, Site, Model, Ports, VLANs, Status, Actions), and a hidden modal `<div>` for the Add/Edit form (fields but no working save button yet).

📝 **Step-by-step implementation plan:**
1. In `index.html`, build the structure: `<header>` with app title "NetVault" and two nav buttons ("Dashboard" / "Inventory"), a `<section id="dashboard">`, a `<section id="inventory">` (hidden by default, toggled by nav), and a `<div id="modal" class="hidden">` containing a `<form>` with inputs matching the Switch fields from Project Context.
2. In `dashboard` section, add 4 `<div class="card">` placeholders with labels: "Total Switches," "Total VLANs," "Sites," "Active Alerts" (static "0" for now — Day 5 makes these real). Leave a `<div id="chart-area"></div>` placeholder for the chart.
3. In `inventory` section, add a search `<input>`, a site `<select>` dropdown (empty options for now), and a `<table>` with the header row only (no rows yet — Day 4 adds real rows).
4. Write `css/style.css`: pick a simple color palette (e.g. dark navy header, white cards, one accent color), style the header, the cards as a responsive grid (CSS Grid or Flexbox, 4 cards per row on desktop, stacking on narrow screens), the table (zebra striping, readable padding), and the modal (centered overlay with a semi-transparent background).
5. Add a small amount of JS in `app.js` just to toggle between Dashboard/Inventory sections when nav buttons are clicked, and to show/hide the modal (open on an "Add Switch" button, close on a cancel button or clicking outside it).
6. In `js/data.js`, write out the **final data shape** as comments (not real data yet) so Day 4 has an exact target:
   ```js
   // Example shape — Day 4 will generate ~100 of these
   // { id: "sw-001", name: "SW-LIB-01", ipAddress: "10.10.1.1", site: "Library Block",
   //   location: "Rack A2", model: "Cisco Meraki MS120", portCount: 24,
   //   vlans: [10, 20, 30], status: "Active", notes: "", lastUpdated: "2026-09-15" }
   ```
7. Commit: "Day 3: static page skeleton, styling, data model finalized."

📂 **Files/folders modified:** `index.html` (full skeleton), `css/style.css` (real styles), `js/app.js` (nav + modal toggle only), `js/data.js` (data shape comment only).

🔗 **Tools/libraries:** None beyond plain CSS/JS. (Optional: Google Fonts CDN link if you want a nicer font — free, no signup.)

🧪 **Testing tasks:** Click nav buttons — sections switch correctly. Click "Add Switch" — modal opens/closes correctly. Resize browser window — cards and table remain readable (basic responsiveness check).

🐞 **Common issues:**
- Modal not centering: confirm it uses `position: fixed` with flexbox centering on its overlay parent, not `position: static`.
- Nav toggle not working: check that section `id`s in HTML exactly match the strings your JS is looking for (case-sensitive).
- Cards not wrapping on mobile width: confirm CSS Grid has `grid-template-columns: repeat(auto-fit, minmax(...))` rather than a fixed 4-column layout.

✅ **End-of-day checklist:**
- [ ] Header + nav toggle Dashboard/Inventory sections correctly
- [ ] 4 dashboard cards visible in a responsive grid
- [ ] Inventory table shows correct header row, no data rows yet
- [ ] Modal form opens/closes with all Switch fields present as inputs
- [ ] Data shape for a Switch object finalized and documented in `data.js` as a comment

📸 **Expected state/screenshot:** Dashboard view showing 4 empty cards; Inventory view showing empty table with headers; modal open showing the empty Add Switch form.

➡️ **Handoff notes for Day 4:** Visual skeleton is done and will not change structurally again. Day 4's only job is to generate ~100+ realistic sample Switch objects in `data.js`, load them via `storage.js` into `localStorage` on first run, and render them as real rows in the Inventory table via `render.js`. No editing/deleting yet — read-only rendering only.

---

## Day 4 — Implementation Part 1: Sample Data + Read-Only Rendering

🎯 **Objective:** Populate the app with a realistic, large sample dataset and get the Inventory table displaying real rows, plus wire up first-run data loading into `localStorage`.

📖 **What I'll learn:** How JavaScript arrays of objects work, how `localStorage.setItem`/`getItem` persists data between page reloads, and how to loop over data to build HTML dynamically (`.map()` or a `for` loop building table rows).

🛠 **Features to build:** Full sample dataset (100+ switches, 5 sites, 15–20 VLANs), first-run seeding into `localStorage`, and a working (read-only) Inventory table that renders every switch as a row.

📝 **Step-by-step implementation plan:**
1. In `js/data.js`, replace the comment with a real exported array `const sampleSwitches = [ ...100+ objects... ]` following the exact shape from Day 3. Generate variety: 5 sites (e.g. "Main Campus," "Library Block," "Hostel Block," "Admin Building," "Engineering Block"), realistic VLAN IDs shared across switches (e.g. VLAN 10 = "Staff," VLAN 20 = "Students," VLAN 30 = "Guest-WiFi," VLAN 40 = "IoT/CCTV," VLAN 99 = "Management"), mixed status values (mostly "Active," a few "Maintenance"/"Inactive" for realism).
2. Also define `const sampleVlans = [ {id:10, name:"Staff", description:"..."}, ... ]`.
3. In `js/storage.js`, write `loadData()`: checks if `localStorage.getItem('netvault_switches')` exists; if not, saves `sampleSwitches` into it (`JSON.stringify`) as the first-run seed; if it exists, loads and parses the existing saved data instead (so future days' edits persist across reloads). Write matching `saveData(switches)` to overwrite storage after any change.
4. In `js/render.js`, write `renderTable(switches)`: clears the table body and rebuilds one `<tr>` per switch, showing Name, IP, Site, Model, Port Count, VLANs (comma-joined), Status, and an "Actions" cell (placeholder buttons, non-functional until Day 7).
5. In `js/app.js`, on page load: call `loadData()`, then call `renderTable()` with the result, so the table is populated immediately when the page opens.
6. Populate the site `<select>` dropdown options dynamically from the unique site names found in the data (don't hardcode them twice).
7. Commit: "Day 4: sample data + read-only inventory rendering."

📂 **Files/folders modified:** `js/data.js` (full dataset), `js/storage.js` (load/save functions), `js/render.js` (table rendering), `js/app.js` (calls load + render on startup).

🔗 **Tools/libraries:** None new. Browser DevTools → Application tab → Local Storage, to visually confirm data was saved.

🧪 **Testing tasks:** Reload the page multiple times — table should show the same 100+ rows every time (proving persistence works, not re-randomizing). Open DevTools → Application → Local Storage → confirm a `netvault_switches` key exists with real JSON data. Manually edit one value in DevTools' Local Storage, reload, confirm the table reflects the edited value (proves render reads from storage, not from the hardcoded sample array).

🐞 **Common issues:**
- Table stays empty: check `renderTable()` is actually being called after `loadData()` resolves, and that you're appending rows to the correct `<tbody>` element, not the `<table>` itself.
- Data resets every reload: your `loadData()` isn't checking for existing storage before overwriting it — always check-then-seed, never seed unconditionally.
- `JSON.parse` errors: `localStorage` only stores strings — make sure every save uses `JSON.stringify` and every load uses `JSON.parse`.

✅ **End-of-day checklist:**
- [ ] `data.js` contains 100+ realistic sample switches across 5 sites and 15–20 VLANs
- [ ] First page load seeds `localStorage`; subsequent reloads read from storage, not re-seed
- [ ] Inventory table renders every switch as a row with correct columns
- [ ] Site dropdown populated dynamically from actual data

📸 **Expected state/screenshot:** Inventory table fully populated with 100+ rows; DevTools Local Storage panel showing the saved `netvault_switches` key with real data.

➡️ **Handoff notes for Day 5:** Real data now exists and persists. Dashboard cards still show static "0" placeholders. Day 5's only job is to calculate real numbers (counts, per-site breakdown) from this same stored data and display them on the dashboard cards + one chart. No table/CRUD changes today.

---

## Day 5 — Implementation Part 2: Live Dashboard & Chart

🎯 **Objective:** Make the 4 dashboard cards show real, calculated numbers from the stored data, and add one simple chart visualizing switches-per-site.

📖 **What I'll learn:** Basic data aggregation in JavaScript (counting, grouping with `.reduce()` or a simple loop), and how to use a free charting library (Chart.js via CDN) to turn numbers into a visual.

🛠 **Features to build:** Dashboard cards showing live Total Switches, Total VLANs, Total Sites, and Switches Needing Attention (count of status ≠ "Active"); one bar chart showing switch count per site.

📝 **Step-by-step implementation plan:**
1. Add the Chart.js CDN script tag to `index.html` (`<script src="https://cdn.jsdelivr.net/npm/chart.js">`) — free, no signup, no build step.
2. In `js/render.js`, write `renderDashboard(switches)`: calculates `totalSwitches = switches.length`, `totalVlans` (count unique VLAN IDs across all switches, or use `sampleVlans.length`), `totalSites` (count unique site values), `needsAttention` (filter where `status !== "Active"`, count).
3. Update the 4 card `<div>`s' text content with these calculated numbers each time `renderDashboard()` runs.
4. Write a small grouping function: build an object like `{ "Main Campus": 23, "Library Block": 18, ... }` by looping over switches and incrementing a counter per site.
5. Feed that grouped object into a Chart.js bar chart rendered inside `#chart-area`: site names on the X axis, switch counts on the Y axis.
6. In `app.js`, call `renderDashboard(switches)` alongside `renderTable(switches)` on page load, using the same loaded data (don't load it twice).
7. Style the "Needs Attention" card to stand out visually (e.g., amber/red accent) only when its count is greater than 0 — a nice, cheap "impressive" touch for the demo.
8. Commit: "Day 5: live dashboard metrics + site breakdown chart."

📂 **Files/folders modified:** `index.html` (Chart.js CDN tag, `<canvas>` element inside `#chart-area`), `js/render.js` (dashboard calculation + chart rendering), `js/app.js` (call renderDashboard on load).

🔗 **Tools/libraries:** Chart.js (CDN, free).

🧪 **Testing tasks:** Confirm all 4 card numbers match what you'd get by manually counting a filtered/sorted view of the data. Confirm chart bars visually match the per-site counts. Temporarily change a few switches' `status` in DevTools Local Storage to "Maintenance," reload, confirm "Needs Attention" card updates correctly.

🐞 **Common issues:**
- Chart not appearing: confirm the Chart.js `<script>` tag loads **before** your own `render.js` script tag in `index.html` (order matters).
- Numbers show `NaN` or `undefined`: check you're reading the right property names — a typo like `swtich.site` vs `switch.site` is the most common cause.
- Chart re-draws on top of itself and looks broken after multiple reloads: make sure you're not creating a new Chart.js instance without destroying the previous one — store the chart instance in a variable and call `.destroy()` before re-creating it.

✅ **End-of-day checklist:**
- [ ] All 4 dashboard cards show correct, live-calculated numbers
- [ ] Bar chart renders and accurately reflects per-site switch counts
- [ ] "Needs Attention" card visually highlights when count > 0
- [ ] Dashboard and table both read from the same single data source (no duplication)

📸 **Expected state/screenshot:** Dashboard view showing 4 populated cards and a bar chart with 5 site bars.

➡️ **Handoff notes for Day 6:** Dashboard and table are both fully data-driven and correct. Day 6 adds search/filter on top of the existing table — this changes what subset of data gets passed into `renderTable()`, but does not change `renderTable()`'s own logic.

---

## Day 6 — Implementation Part 3: Search & Filter

🎯 **Objective:** Make the Inventory table actually useful at scale — instantly searchable by name/IP and filterable by site and VLAN.

📖 **What I'll learn:** How to use `.filter()` on arrays with multiple combined conditions, and how to wire an `<input>`'s "typing" event (`input` event) to live-update a view without a page reload.

🛠 **Features to build:** A live search box (matches switch name or IP address as you type), a site filter dropdown (already populated from Day 4), and a VLAN filter dropdown; all three combine (AND logic) and update the table instantly.

📝 **Step-by-step implementation plan:**
1. In `js/filters.js`, write `applyFilters(allSwitches, searchTerm, selectedSite, selectedVlan)`: starts with the full array, then chains `.filter()` calls — keep switches where `name` or `ipAddress` includes `searchTerm` (case-insensitive), AND `site === selectedSite` (skip this filter if "All Sites" selected), AND `vlans.includes(Number(selectedVlan))` (skip if "All VLANs" selected). Return the filtered array.
2. Populate the VLAN filter `<select>` dynamically from `sampleVlans` (Day 4), same pattern as the site dropdown.
3. In `app.js`, add event listeners: on every keystroke in the search box and every change of either dropdown, call `applyFilters()` with current values, then pass the result into `renderTable()` (re-using Day 4's function unchanged) — this is what makes the table "live."
4. Add a small "Showing X of Y switches" text near the table that updates with the filtered count vs. total count — a cheap but effective UX touch.
5. Add a "Clear Filters" button that resets the search box and both dropdowns back to defaults and re-renders the full table.
6. Commit: "Day 6: live search and multi-filter for inventory table."

📂 **Files/folders modified:** `js/filters.js` (new filtering logic), `js/app.js` (event listeners wiring filters to render), `index.html` (VLAN filter dropdown element if not already scaffolded on Day 3).

🔗 **Tools/libraries:** None new.

🧪 **Testing tasks:** Type a partial switch name — table narrows correctly. Type a partial IP — table narrows correctly. Select a site — only that site's switches show. Select a VLAN — only switches with that VLAN show. Combine search + site + VLAN together — results respect all three at once. Click "Clear Filters" — table returns to full 100+ rows.

🐞 **Common issues:**
- Filter feels "laggy" typing fast: this is very unlikely at ~100 rows with plain JS, but if it happens, ensure you're not re-reading/re-parsing `localStorage` on every keystroke — filter the already-loaded in-memory array instead.
- VLAN filter doesn't match anything: check whether VLAN IDs are stored as numbers vs. the dropdown value being a string — use `Number()` to convert before comparing.
- Search box loses focus after typing one character: you're likely re-rendering the search input itself inside `renderTable()` — the input element should live outside the table's re-rendered area.

✅ **End-of-day checklist:**
- [ ] Search box filters by name and IP, live, case-insensitive
- [ ] Site and VLAN dropdown filters work independently and combined
- [ ] "Showing X of Y" counter updates correctly
- [ ] Clear Filters button resets everything correctly

📸 **Expected state/screenshot:** Inventory view with an active search term + site filter applied, showing a narrowed result set and the "Showing X of Y" counter.

➡️ **Handoff notes for Day 7:** Table is now fully searchable/filterable and reads from a single in-memory array that mirrors `localStorage`. Day 7 adds the ability to actually change that data — Add, Edit, Delete — which must call `saveData()` (Day 4) after every change and re-run the current filters so the table stays accurate.

---

## Day 7 — Implementation Part 4: Add, Edit, Delete (CRUD)

🎯 **Objective:** Make the "Add Switch" modal (built visually on Day 3) actually save new switches, and make existing rows editable and deletable.

📖 **What I'll learn:** How to read values out of a form, basic form validation, how to generate a simple unique ID, and how to update an array (add/replace/remove an item) then persist the change.

🛠 **Features to build:** Working "Add Switch" form (creates a new switch and adds it to the table), "Edit" button per row (opens the same modal pre-filled, saves changes to that switch), "Delete" button per row (with a confirmation prompt).

📝 **Step-by-step implementation plan:**
1. In `js/crud.js`, write `addSwitch(formData, allSwitches)`: validate required fields (name, IP, site — reject empty name or malformed IP with a simple visible error message, not a browser `alert()`), generate a new `id` (e.g. `"sw-" + Date.now()`), push the new object into the array, call `saveData()`, return the updated array.
2. Write `updateSwitch(id, formData, allSwitches)`: find the switch by `id`, replace its fields with the form's new values, call `saveData()`, return the updated array.
3. Write `deleteSwitch(id, allSwitches)`: filter out the switch with that `id`, call `saveData()`, return the updated array.
4. Wire the modal's Save button: if the modal was opened via "Add," call `addSwitch()`; if opened via an "Edit" button, call `updateSwitch()` with the existing switch's `id`. Track which mode the modal is in with a simple variable (e.g. `editingId = null` for add, or set to the switch's id for edit).
5. Wire each row's "Edit" button (from Day 4's placeholder) to open the modal and pre-fill every field with that row's current values.
6. Wire each row's "Delete" button to show a `confirm("Delete this switch?")` browser confirmation before calling `deleteSwitch()`.
7. After any add/edit/delete, re-run the currently active filters (Day 6) and re-render both the table and the dashboard (Day 5), since counts have changed.
8. Add simple inline validation messages (e.g., red text under a field) for: empty name, empty/invalid IP format, port count not a positive number.
9. Commit: "Day 7: full add/edit/delete functionality with validation."

📂 **Files/folders modified:** `js/crud.js` (new file with add/update/delete logic), `js/app.js` (wire modal save button, edit/delete button listeners), `index.html` (ensure modal form has a hidden field or JS variable tracking edit-mode).

🔗 **Tools/libraries:** None new.

🧪 **Testing tasks:** Add a new switch — confirm it appears in the table immediately and the dashboard counts update. Edit an existing switch's site — confirm it moves correctly under site filtering and the chart updates. Delete a switch — confirm it disappears from the table and all counts decrease by 1. Try submitting the Add form with an empty name — confirm a validation message appears and nothing is saved. Reload the page after each operation — confirm changes persisted (this is the real proof `localStorage` is working end-to-end).

🐞 **Common issues:**
- Edited switch appears as a duplicate instead of replacing the original: your `updateSwitch()` is pushing a new object instead of finding-and-replacing by `id` — double check the `id` comparison.
- Changes don't survive a page reload: confirm `saveData()` is actually being called inside each CRUD function, not just updating the in-memory array.
- Delete removes the wrong row: confirm the Delete button's click handler is capturing the correct row's `id` (a common bug is all buttons referencing the last row's `id` due to a closure/loop issue — pass the `id` explicitly via a `data-id` attribute on the button instead).

✅ **End-of-day checklist:**
- [ ] Add Switch creates a new, correctly-saved entry
- [ ] Edit pre-fills and correctly updates the right switch
- [ ] Delete removes the correct switch after confirmation
- [ ] Dashboard and filters both reflect changes immediately
- [ ] Basic validation prevents obviously bad data (empty name, bad IP, non-numeric ports)
- [ ] All changes survive a full page reload

📸 **Expected state/screenshot:** Modal open in "Edit" mode with pre-filled data; table showing a freshly added switch; a validation error message displayed on an invalid form submission.

➡️ **Handoff notes for Day 8:** Core functionality is complete — this is a real, working CRUD app. Day 8 is about resilience (export/import so data isn't trapped in one browser) and visual polish, not new core features. Resist the urge to add new entity types or fields at this stage.

---

## Day 8 — Polish: Export/Import, Visual Pass, Empty States

🎯 **Objective:** Make the app feel finished and trustworthy — add a way to back up/restore data (since `localStorage` is tied to one browser), and do a full visual polish pass.

📖 **What I'll learn:** How to trigger a file download from JavaScript, how to read an uploaded file back into your app, and general UI polish techniques (spacing, empty states, hover feedback).

🛠 **Features to build:** "Export Data" button (downloads current data as a `.json` file), "Import Data" button (lets you upload a previously exported `.json` file to restore/replace data), a proper empty state (what the table looks like if filters match zero results), hover/focus states on buttons, and a final consistent visual pass.

📝 **Step-by-step implementation plan:**
1. In `js/storage.js`, write `exportData(switches)`: convert the array to a JSON string, create a `Blob`, generate a temporary download link (`<a>` element with `download="netvault-backup.json"`), and programmatically click it to trigger the browser's save dialog.
2. Write `importData(file, callback)`: use `FileReader` to read the uploaded `.json` file's text, `JSON.parse()` it, validate it's an array before accepting it, call `saveData()` with the new data, then call the callback to re-render everything.
3. Wire both buttons in `app.js`; the Import button should use a hidden `<input type="file">` triggered by a visible styled button (a common pattern — file inputs are ugly by default).
4. In `render.js`, update `renderTable()` so that when the filtered array is empty, it shows a friendly message row ("No switches match your filters — try clearing them") instead of a blank table.
5. Do a full CSS polish pass: consistent spacing (pick one spacing scale, e.g. multiples of 4px/8px, and use it everywhere), button hover states (slight color shift or shadow), consistent border-radius across cards/buttons/modal, make sure the color of the "Needs Attention" card and any status badges (Active = green, Maintenance = amber, Inactive = gray) are consistent.
6. Add small loading/transition polish: e.g., a subtle fade-in when the modal opens (`transition: opacity`), not required but cheap and effective for the demo.
7. Write the `README.md`: what NetVault is, screenshot, how to run it locally (double-click `index.html` or use Live Server), and how to export/import data.
8. Commit: "Day 8: export/import, empty states, visual polish pass, README."

📂 **Files/folders modified:** `js/storage.js` (export/import functions), `js/render.js` (empty state), `js/app.js` (wire export/import buttons), `css/style.css` (polish pass), `README.md` (new).

🔗 **Tools/libraries:** None new (uses built-in browser `Blob`/`FileReader` APIs).

🧪 **Testing tasks:** Export data, open the downloaded `.json` file in a text editor — confirm it's valid, readable JSON matching your current data. Clear `localStorage` entirely (DevTools → Application → Clear Storage), reload (app re-seeds sample data), then Import your previously exported file — confirm your real data comes back, not the sample seed. Trigger the empty state by searching for a nonsense term — confirm the friendly message appears instead of a blank table.

🐞 **Common issues:**
- Downloaded file is empty or says `[object Object]`: you forgot `JSON.stringify()` before creating the `Blob` — the Blob needs a string, not a raw JS object.
- Import silently does nothing: check the `FileReader`'s `onload` callback is where you put your `JSON.parse` and `saveData` logic — reading a file is asynchronous, so this logic can't run immediately after calling `.readAsText()`.
- Imported data "corrupts" the app (blank dashboard, errors): add a basic shape check before accepting imported data — confirm it's an array and that the first item has a `name` property, otherwise reject with a friendly error rather than saving garbage.

✅ **End-of-day checklist:**
- [ ] Export downloads a valid, correctly-formatted `.json` backup
- [ ] Import correctly restores previously exported data
- [ ] Empty search/filter results show a friendly message, not a blank table
- [ ] Consistent spacing, button states, and status badge colors across the whole app
- [ ] README written with clear "how to run" instructions

📸 **Expected state/screenshot:** The downloaded JSON file open in a text editor; the empty-state message showing after a no-match search; final polished dashboard + inventory views side by side.

➡️ **Handoff notes for Day 9:** Feature set is 100% complete and will not change again. Day 9 is entirely about testing what already exists and fixing bugs — no new features, no matter how tempting.

---

## Day 9 — Testing: Full QA Pass & Bug Fixing

🎯 **Objective:** Deliberately try to break the app across realistic scenarios, log every issue found, and fix them — this is what makes v1.0 feel trustworthy rather than "demo-only."

📖 **What I'll learn:** How to write and follow a manual test checklist, how to think like a tester (edge cases, not just the happy path), and basic cross-browser sanity checking.

🛠 **Features to build:** None — bug fixes only. If a real gap is found that truly requires a small new piece of logic (e.g., a missing validation case), fix it minimally; do not expand scope.

📝 **Step-by-step implementation plan:**
1. Write out a manual test checklist covering every feature built Days 4–8 (use the "Testing tasks" from each day above as your base checklist — compile them into one document, `TESTING.md`).
2. Go through the checklist top to bottom in your primary browser, checking off each item and writing down anything that doesn't behave as expected.
3. Specifically test edge cases: adding a switch with an extremely long name (does the table layout break?), a switch with zero VLANs assigned, deleting every switch one by one until the table is empty (does the dashboard show 0s gracefully or error?), searching with special characters, importing a malformed/empty `.json` file.
4. Open the app in at least one other browser (e.g., if you built/tested mostly in Chrome, check Firefox or Edge) — confirm layout and functionality both hold up. Note: `localStorage` is per-browser, so your data won't carry over — that's expected, not a bug.
5. Do a basic accessibility sanity check: can you tab through the Add form fields in a sensible order using only the keyboard? Do form inputs have visible labels (not just placeholder text, which disappears on focus)?
6. For each bug found, fix it directly in the relevant file from earlier days (most fixes will be small — a missing null check, a wrong comparison operator, a CSS overflow rule).
7. Re-run the full checklist after fixes to confirm nothing broke as a result of the fix.
8. Commit: "Day 9: QA pass, bug fixes, cross-browser check."

📂 **Files/folders modified:** `TESTING.md` (new — your checklist and results), plus small targeted fixes across whichever `.js`/`.css` files had bugs.

🔗 **Tools/libraries:** None new. Just a second browser installed if you don't already have one.

🧪 **Testing tasks:** (this entire day is testing — see implementation plan above.)

🐞 **Common issues found at this stage (watch for these specifically):**
- Long text (switch names, notes) overflowing table cells or cards — add `overflow: hidden; text-overflow: ellipsis;` with a `max-width` where needed.
- Deleting all switches causes the chart to error instead of showing an empty state — add a check for an empty array before handing data to Chart.js.
- Import of a non-array or empty file silently breaking the table — confirm your Day 8 validation actually catches this case (this is the most likely real bug you'll find).

✅ **End-of-day checklist:**
- [ ] Full `TESTING.md` checklist completed with results noted
- [ ] All discovered bugs fixed and re-verified
- [ ] App confirmed working in a second browser
- [ ] Basic keyboard navigation through the Add/Edit form confirmed usable

📸 **Expected state/screenshot:** `TESTING.md` showing a completed checklist; before/after screenshot of any visual bug you fixed (e.g., text overflow).

➡️ **Handoff notes for Day 10:** App is fully tested and stable. Day 10 is packaging, final demo recording, and the "maintenance/future scope" write-up — no functional changes should happen today except genuine last-minute critical fixes.

---

## Day 10 — Deployment & Wrap-Up: Package, Demo, Ship

🎯 **Objective:** Package the finished app cleanly, record a demo, and formally close out v1.0 — including documenting what's next (maintenance/future scope), matching the SDLC this capstone is built around.

📖 **What I'll learn:** How to package a small project for others to run, how to write a clear project write-up, and how to record and narrate a short product demo.

🛠 **Features to build:** None. This day is packaging, documentation, and presentation only.

📝 **Step-by-step implementation plan:**
1. Do a final read-through of all files for stray `console.log()` debug statements or commented-out dead code left over from earlier days — clean these up.
2. Confirm `README.md` is complete and accurate: project description, screenshot, "how to run" (double-click `index.html`, or open with Live Server), "how to back up data" (Export button), and a short "Known Limitations / Future Scope" section listing what Day 1's PRD explicitly deferred (multi-user roles, live device polling, alerts, config history, cloud hosting).
3. Zip the whole `/netvault` folder (or confirm it's fully committed and pushed to GitHub) so it's a self-contained, shareable package.
4. Record a 2–4 minute screen recording demo: show the Dashboard (call out the live numbers and chart), show searching/filtering the Inventory table, show Adding a new switch end-to-end, show Editing and Deleting a switch, show Export then Import working, and end by briefly showing the README.
5. Write your "60 Days of Claude" wrap-up post for this capstone (per your existing challenge tracking format) summarizing: the problem, what you built, what you learned, and what's next.
6. Push the final commit: "Day 10: v1.0 release — NetVault."
7. Optionally tag this commit on GitHub as `v1.0` (a nice-to-have, not required) so it's clearly marked as your finished capstone milestone.
8. Write a short personal retrospective (can be private, just for you): what was harder than expected, what you'd do differently, and which of the "future scope" items you'd actually want to build next if you continued this project.

📂 **Files/folders modified:** `README.md` (finalized), no code changes expected beyond critical fixes carried over from Day 9.

🔗 **Tools/libraries:** A free screen recording tool (e.g., your OS's built-in screen recorder — Windows Game Bar, macOS Screenshot app, or OBS Studio if already comfortable with it).

🧪 **Testing tasks:** One final full click-through of every feature immediately before recording the demo, to make sure nothing regressed since Day 9.

🐞 **Common issues:**
- Demo recording reveals a bug you didn't catch on Day 9: fix only if it's small and clearly broken (e.g., a visible error); do not use this as an excuse to add new features on Day 10.
- Zipped folder doesn't run when shared: confirm you zipped the folder itself (not files individually) and that relative paths in `index.html` (`css/style.css`, `js/app.js`, etc.) don't use any absolute local file paths.

✅ **End-of-day checklist:**
- [ ] All debug/dead code removed
- [ ] README finalized with screenshot, run instructions, and future scope section
- [ ] Project pushed to GitHub / zipped as a shareable package
- [ ] 2–4 minute demo recording completed
- [ ] "60 Days of Claude" wrap-up post written
- [ ] Personal retrospective written

📸 **Expected final state:** A fully working, polished local web app; a demo video file; a GitHub repo with a clean commit history from Day 2 through Day 10; a written retrospective.

➡️ **Handoff notes (post-capstone / maintenance phase):** NetVault v1.0 is complete. If continued beyond this capstone, the natural next milestones (in rough priority order) are: (1) a lightweight backend + real database so data isn't trapped per-browser, (2) basic multi-user login if the team genuinely needs shared simultaneous access rather than manual export/import handoffs, (3) CSV export alongside JSON for non-technical stakeholders, (4) optional live device polling (SNMP) as a genuinely separate, larger future project.

---

## Cross-Day Notes for Future AI Assistants

- **Never suggest changing the tech stack.** Plain HTML/CSS/JS + `localStorage` was deliberately chosen for a total-beginner builder with 30–60 min/day and a local-only deployment target. Suggesting React, a backend, or a real database is scope creep and will derail the timeline.
- **Never suggest adding user accounts, live device polling, or alerting.** These are explicitly deferred to future scope in the PRD.
- **Each day builds only what that day's section says.** If the builder asks "should we also add X" mid-day, check whether X appears in a later day's plan — if so, defer it there; if it appears nowhere, treat it as out of scope for v1.0 and note it as a future-scope idea instead of building it.
- **Keep explanations beginner-level throughout** — assume no prior coding background, explain new concepts in plain language the first time they appear, and give copy-pasteable code with a plain-language explanation of what it does.
