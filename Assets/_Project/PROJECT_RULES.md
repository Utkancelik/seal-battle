# PROJECT RULES — Cursed Scribe

## 1. Project Goal
Build a small, complete 2D mobile roguelike that prioritizes:
- Clean, modular architecture
- Data-driven design
- Meaningful player decisions
- Fun moment-to-moment gameplay

This project is a learning sandbox. Clean structure is more important than speed.

---

## 2. Game Pillars (Non-Negotiable)

1. Combat is auto-attack
2. Player skill expression = movement + positioning
3. Power always introduces pressure (soft constraints)
4. Decisions change rules, not just numbers
5. UI is passive — it never drives gameplay logic

---

## 3. Architectural Rules

### 3.1 Layer Boundaries
- Core: game states, run flow, signals
- Gameplay: combat, movement, enemies, rooms
- UI: screens, HUD, visual feedback only
- Data: ScriptableObjects (data only)

Gameplay must not reference UI.
UI listens to events or reads exposed state.

---

### 3.2 Dependencies
- No direct cross-system references
- Cross-system communication uses events/signals
- MonoBehaviours should depend on interfaces where reasonable

---

### 3.3 ScriptableObjects
ScriptableObjects are:
- Configuration
- Content definitions
- Tunable data

They must NOT:
- Hold runtime state
- Subscribe to events
- Reference scene objects

---

## 4. Seals System (Core USP)

### 4.1 Definition
A Seal is a modifier applied during a run that:
- Provides a strong benefit
- Introduces soft pressure via risk, exposure, or inefficiency

### 4.2 Design Rules
- No Seal may be a pure buff
- No Seal may fully forbid player actions
- Each Seal must affect positioning OR enemy interaction

### 4.3 Examples of Soft Pressure
- Standing still becomes dangerous
- Staying close to enemies increases damage taken
- Movement speed is high but stopping creates vulnerability
- Attacks are strong but expose the player briefly

---

## 5. Combat Rules

- Player attacks automatically when enemies are in range
- Player input controls movement only
- Combat difficulty comes from:
  - enemy patterns
  - area denial
  - Seal interactions

No manual aiming or button-mashing is required.

---

## 6. Class Design Rules

- One responsibility per class
- Avoid "Manager" classes unless clearly scoped
- Prefer composition over inheritance
- MonoBehaviours should be thin glue, not logic containers

If a class exceeds ~200 lines, review its responsibilities.

---

## 7. UI Rules

- UI reacts to game state; it does not control it
- UI listens to signals such as:
  - RoomCleared
  - HealthChanged
  - SealOffered
  - SealChosen
- UI logic should be testable without gameplay systems

---

## 8. Development Process Rules

- Build vertical slices
- Refactor early
- No feature is added without considering:
  - Which layer does this belong to?
  - What does it depend on?
  - Can it be removed cleanly?

---

## 9. Definition of Done
A feature is done when:
- It works
- It respects architecture rules
- It can be removed without breaking unrelated systems

---

## 10. Input
- Input emits intent events only.
- Player systems never read joystick components directly.

---

## 11. Camera
- Camera follows player smoothly.
- Camera has zero gameplay logic.