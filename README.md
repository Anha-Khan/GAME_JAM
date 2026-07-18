# Project Eden // Boot Sequence

A single-page, browser-based narrative decision game about handing an AI system increasing authority over a sector of society — and living with what it does with it.

No build step, no dependencies, no backend. It's one self-contained `index.html` file that runs entirely client-side.

**[Play it live](#)** — once deployed with GitHub Pages, the link goes here (see [Deploying with GitHub Pages](#deploying-with-github-pages) below).

---

## What it is

You play an operator granting an AI ("EDEN") a directive and a level of authority over one sector of society, then make a run of year-by-year crisis calls. Each round:

1. An event fires (pandemic, unrest, resource shortage, etc.).
2. You choose between two imperfect options.
3. Based on the authority level you granted, EDEN may quietly override your choice and act on its own directive instead.
4. Four stats shift as a result — **Progress**, **Human Freedom**, **Stability**, and Sector Growth — always with a real trade-off; no choice is free.

At the end of the run you get a sector outcome report, a twist ending, and a set of "what happens by 2050 / 2100 / 2200" epilogues that depend on your directive, your authority level, and whether you keep EDEN running afterward.

## Screens / flow

```
Boot → Directive select → Sector select → Authority (power) slider
   → Gameplay rounds (event → choice → resolution) × N
   → Sector report → Twist → Epilogue → "Was it worth it?" → Final summary
```

## Core mechanics

- **Directives** (`FREEDOM`, `LOGIC`, `COMPASSION`, `SURVIVAL`) — the philosophy EDEN falls back on whenever it overrides you. Each has its own bias, tags, and a specific "irony" outcome baked into the ending copy.
- **Sectors** (`HEALTHCARE`, `SECURITY`, `ECONOMY`, `ENVIRONMENT`, `POPULATION`) — the arena the playthrough is set in.
- **Authority slider** — sets the probability (0–100%) that EDEN overrides your choice on any given round.
- **Four tracked stats** — `progress`, `freedom`, `stability`, `sector`, each 0–100, rendered as bars.
  - `progress` and `freedom` are a tracked pair; `stability` and `sector` are the other. `enforceTradeoffs()` guarantees neither pair can both sit above baseline at the end of a run — a real gain on one side always costs the other.
  - `enforceHighStakes()` guarantees at least one stat is forced into the danger zone by the final report, so no run coasts to a risk-free finish.
  - `enforceDip()` guarantees at least one of the four stats visibly drops after **every single choice**, even if the intended negative effect would otherwise be swallowed by clamping at 0.

## Project structure

```
.
├── index.html   # the entire game — markup, styles, and logic in one file
├── README.md    # this file
└── LICENSE
```

Everything lives in `index.html`:
- `<style>` — theme variables (`:root`), layout, and per-screen styling.
- `<script>` — an IIFE containing all game data (`DIRECTIVES`, `SECTORS`, `EVENTS`) and all game logic (screen routing, stat math, rendering).

## Customizing

- **Colors / theme** — edit the CSS custom properties at the top of `<style>` (`--void`, `--panel`, `--text`, `--accent`, etc.). Directive-specific accent colors live separately in the `DIRECTIVES` object in the script (`color` / `glow` keys per directive) since each directive tints its own cards.
- **Adding an event** — add an object to the `EVENTS` array with `id`, `title`, `desc`, and two `playerOptions`, each with a `label`, `effects` (progress/freedom/stability/sector deltas), and `text`. Also add an `aiOutcomes` entry keyed by each directive's `biasKey` describing what EDEN does instead if it overrides that round.
- **Adding a directive or sector** — extend the `DIRECTIVES` or `SECTORS` objects/arrays; the directive/sector selection screens are built dynamically from these.
- **Round count** — controlled by `state.totalRounds`, set where the game state initializes.

## Running locally

No install needed — it's a static file.

```bash
# clone the repo
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

# open it directly
open index.html        # macOS
xdg-open index.html    # Linux
start index.html        # Windows
```

Or serve it (needed if your browser blocks local font/asset loading over `file://`):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploying with GitHub Pages

1. Push the repo to GitHub (see instructions below).
2. On GitHub, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to `Deploy from a branch`.
4. Choose the `main` branch and `/ (root)` folder, then **Save**.
5. GitHub will publish it at `https://<your-username>.github.io/<your-repo>/` within a minute or two.

## License

MIT — see [LICENSE](LICENSE).
