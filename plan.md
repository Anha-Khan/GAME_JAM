# Project EDEN — Development Plan

No deadline was specified, so phases are ordered by dependency rather than pinned to dates — slot in real dates once you know your submission window (game jam, hackathon, class deadline, etc.).

## Recommended Tech Stack (assumption — flag if this doesn't fit your team)
The game is UI-and-writing heavy with minimal art, which points toward a **web stack** over a game engine:
- **HTML/CSS/JS**, optionally with a lightweight framework (React or plain JS is fine at this scope) for the dashboard/hologram UI
- **JSON or a simple data file** for the event pool, so writers can add events without touching code
- Packaging as an Electron app later if you want a standalone build, but browser-first keeps iteration fast

If your team is more comfortable in Raylib/C (per prior project experience), the same architecture works there too — it just means hand-rolling UI widgets instead of using the DOM, which will slow down the dashboard-heavy screens. Web is the lower-friction choice specifically *because* the visual style is charts/maps/screens rather than sprites.

## Phase 0 — Prototype the Loop (paper or spreadsheet)
Goal: prove the core loop is fun before writing a line of production code.
- [ ] Write 5–8 sample events with 2–3 player options each
- [ ] Manually run all 4 directives through the same events, write out what EDEN does and why
- [ ] Sanity check: does each directive feel meaningfully different in play, not just in flavor text?

## Phase 1 — Core Systems
- [ ] Boot sequence screen (directive selection + BOOT SYSTEM button)
- [ ] State/modifier tracker (stability, freedom, casualties, resources, unity)
- [ ] Event engine: pull event → present options → resolve
- [ ] EDEN decision logic: tolerance thresholds per directive, override trigger, override-reason text
- [ ] Bare-bones UI (can be unstyled — function over form at this stage)

## Phase 2 — Content Pass
- [ ] Full event pool (aim for enough events that a playthrough doesn't repeat obviously — target count depends on run length)
- [ ] Cost-profile tagging for every option (which resource it trades off)
- [ ] Era checkpoint summary text for 2050 / 2100 / 2200, driven by state thresholds
- [ ] Ending variants (utopia / AI rule / extinction / robot civilization, plus hybrids from state combinations)
- [ ] Final twist sequence: "Should I continue making decisions for humanity?"

## Phase 3 — Visual/UI Polish
- [ ] Holographic dashboard shell: maps, charts, camera-feed panels
- [ ] Override presentation (player choice → EDEN's actual action → outcome) — this is the game's signature moment, worth extra polish time
- [ ] State visualizations (stat bars, alert overlays, map heat states) reacting to modifier changes
- [ ] Sound/ambient pass if scope allows (low priority given minimal-art direction)

## Phase 4 — Playtesting & Balance
- [ ] Playtest each directive path separately — confirm each feels distinct and none is degenerate/optimal
- [ ] Tune override frequency (too many feels like the player has no agency; too few makes the AI's "personality" invisible)
- [ ] Tune ending thresholds so multiple distinct endings are actually reachable, not just the two extremes

## Phase 5 — Ship
- [ ] Bug pass
- [ ] Build/export (web build, or Electron package if going standalone)
- [ ] Trailer/pitch materials if this is for a jam or hackathon submission

## Team Roles (fill in — structure only)
- **Systems/logic:** event engine, EDEN decision logic, state tracker
- **Writing:** events, EDEN dialogue per directive, ending text
- **UI/frontend:** dashboard, charts, override presentation
- **Design/balance:** cost profiles, threshold tuning, playtesting

## Risks
- **Override system is the whole game** — if it doesn't read as intentional AI "personality" rather than random punishment, the core hook fails. Prioritize this over content volume.
- **Content volume vs. time:** four directives × many events × distinct outcomes is a content-multiplication problem. Consider whether events need full uniqueness per directive or can share consequence text with only the trigger/threshold differing.
- **Scope creep on visuals:** "holographic UI" can quietly become a full custom design system. Lock a small component set (one map style, one chart style, one alert style) early and reuse it everywhere.
