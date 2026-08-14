# Day 20 of 60 — AI Face Puzzle Game 🧩

## 🎯 Topic
Build an interactive **Face Puzzle Game** that captures a live webcam photo and turns it into a playable sliding-style puzzle with adjustable difficulty.

## 📋 What This Project Does
1. Requests webcam access and shows a live video preview
2. Lets the user snap a selfie onto a canvas
3. Offers 3 difficulty levels: **3×3 (Easy)**, **4×4 (Medium)**, **5×5 (Hard)**
4. Slices the photo into equal tiles and scrambles them (guaranteed solvable)
5. Supports drag (desktop) and touch (mobile) to swap tiles
6. Snaps tiles to the nearest grid cell and highlights the dragged tile
7. Highlights correctly placed tiles in green
8. Tracks elapsed time (`mm:ss.t`) and move count live
9. Detects the win condition automatically and stops the timer
10. Shows a results screen with final time, moves, and difficulty
11. Saves the **Top 5 best times** to `localStorage` with date, moves, and difficulty
12. Displays a leaderboard of saved best times
13. Includes Retake Photo / New Photo / Play Again / Reshuffle controls
14. Fully responsive — works on desktop and mobile browsers

## 🛠️ Tech Stack
- **HTML5** — structure, semantic layout
- **CSS3** — glassmorphism UI, animations, responsive grid/board layout
- **Vanilla JavaScript (ES6+)** — no frameworks, no build tools
- **Browser APIs used:**
  - `navigator.mediaDevices.getUserMedia()` — camera access
  - `<canvas>` — photo capture & cropping
  - `localStorage` — persistent leaderboard
  - Pointer events (`mousedown/mousemove/mouseup` + `touchstart/touchmove/touchend`) — unified drag & touch support
  - `performance.now()` — accurate live timer

## 🧠 Key Learnings
- **Camera permission handling**: gracefully handling `NotAllowedError`, `NotFoundError`, `NotReadableError`, and insecure-origin cases so the app never breaks silently.
- **Image slicing without extra canvases**: using CSS `background-size` + `background-position` per tile is far lighter than generating N separate cropped canvases.
- **Guaranteed-solvable scrambling**: since this is a *free-swap* puzzle (any tile can swap with any other, unlike a classic 15-puzzle with a single blank tile), every random permutation is solvable — no parity-fixing algorithm needed, just re-roll if it lands on the already-solved state.
- **Unified drag + touch controls**: writing one `getPoint(e)` helper that normalizes `MouseEvent` and `TouchEvent` coordinates avoids duplicating logic for desktop vs mobile.
- **Snap-to-grid math**: converting free-drag pixel coordinates back to the nearest row/column with `Math.round(pos / cellSize)`.
- **Client-side persistence**: using `localStorage` to keep a small, sorted, capped (top 5) leaderboard without any backend.
- **Responsive canvas-based UI**: recalculating tile positions and background sizing on window resize so the board stays crisp on any screen size.

## 🚀 How to Run
1. Download `face-puzzle.html`
2. Serve it locally (camera access needs HTTPS or localhost):
   ```bash
   python -m http.server 8000
   ```
3. Open `http://localhost:8000/face-puzzle.html` in Chrome, Firefox, or Safari
4. Allow camera access, snap a photo, pick a difficulty, and play!

> ⚠️ Camera access will **not** work over a plain `file://` URL in most browsers — always serve over `localhost` or `HTTPS`.

## 📂 Files
```
day20/
├── face-puzzle.html   # complete self-contained game (HTML + CSS + JS)
└── README.md          # this file
```

## 🔗 Part of
**#60DaysOfClaude** — a daily challenge exploring what's possible when building with Claude AI.
Follow the full journey in the [60 Days of AI](../) repo.
