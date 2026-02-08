# Merged Ruleset (GDD + PROJECT_RULES)

## Priority Order
- **Primary source:** `/Docs/GDD` (most current, authoritative).
- **Secondary source:** `PROJECT_RULES.md` (supports architecture/process).
- **If conflict exists:** GDD overrides PROJECT_RULES.
- **If conflict affects core pillars or architecture:** stop and ask before proceeding.

## Non-Negotiable Rules

### Core Pillars
- Combat is **auto-attack**.
- Skill expression = **movement + positioning**.
- Power **always introduces pressure**.
- Decisions **change rules**, not just numbers.
- UI is **passive**; never drives gameplay logic.

### Gameplay Loop & Scope
- Loop: enter room → spawn enemies → auto-attack → movement/positioning → clear → **rule-altering upgrade** → next room.
- Mobile portrait, one-finger play.
- Scope: 1 character, 1 biome, 10–15 enemies, 20–30 upgrades, 10–15 min run.

### Player Mechanics
- Movement via analog/drag input; speed is constant unless upgrades change it.
- Attacks auto-target nearest enemy in range; no manual aiming.
- No health regen; health loss is persistent per run.
- Input emits **intent events** only; player systems don’t read joystick components directly.

### Enemies & Rooms
- Enemies create **area control**, not raw DPS.
- Enemy types: chaser, zoner, sniper, swarm, rule-breaker.
- Rooms are square/rect, fixed camera, data-driven spawns.
- Room types: combat, elite, choice, curse, rare rest.

### Upgrades, Seals, Pressure
- Upgrades change **rules**, not stats.
- Seals: strong benefit + **soft pressure**; never pure buff; never fully forbids actions; must affect positioning or enemy interaction.
- Pressure scales with player power (e.g., arena shrink, hazards, vision reduction, input delay, enemy mutation).

### Meta Progression
- No unlocks or stat boosts.
- Only add upgrades to pool and enemy modifiers.

### UI, Art, Audio
- UI: HP, cooldown, passive feedback; **never** triggers gameplay.
- Art: pixel art, limited palette, high contrast, readability > beauty.
- Audio: minimal SFX; clear UI feedback; low BPM, loop-friendly, tense music.

### Architecture & Code Rules
- Event-driven communication; no UI↔gameplay references.
- No singleton abuse; state-driven run flow.
- Layers: Core / Gameplay / UI / Data (ScriptableObjects are data-only).
- No direct cross-system references; use events/signals; prefer interfaces.
- One responsibility per class; avoid “Manager” classes; prefer composition.
- Camera follows player smoothly; no gameplay logic in camera.

### Success Criteria & Exclusions
- Success: clean architecture, easy to add upgrades, “smart” systems, code instructive.
- Exclusions: no multiplayer, story campaign, character classes, or live ops.

## Conflict Resolution
- GDD always overrides PROJECT_RULES for gameplay/design details.
- If a conflict affects **core pillars** or **architecture**, stop and ask before proceeding.

## Terminology Glossary
- **Auto-attack:** Player attacks automatically when enemies are in range.
- **Seal:** Run modifier that grants a strong benefit and adds soft pressure.
- **Pressure:** Constraints that increase as player power grows (e.g., arena shrink).
- **Rule-altering upgrade:** Upgrade that changes gameplay rules rather than stats.
- **Passive UI:** UI that reflects state only and never drives gameplay logic.
