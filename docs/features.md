
---

## `docs/features.md`
```md
# Features

Below are examples of major systems and gameplay features I built or customized in Siriuz Online (CrystalServer-based).

## Core Gameplay Systems

### Custom Vocation: Monk
- Introduced a Monk vocation with its own progression and gameplay identity
- Implemented vocation-specific rules (damage, scaling, abilities, restrictions)
- Balanced gameplay through iteration: tuning based on player experience and outcomes

### Guild Tamers System
- Added a system tied to guild membership and progression
- Implemented stateful rules and rewards that persist across sessions
- Focused on anti-exploit behavior and predictable progression

### Hunting Tasks System
- Created tasks that track hunting objectives and reward completion
- Designed a scalable structure for adding more tasks and difficulty tiers
- Ensured persistence and safe resets/rollovers

## Server & Quality-of-Life
- Improved stability by tightening event flows and handling edge cases safely
- Enhanced admin control and visibility into state (via database and logging patterns)

## Data & Persistence
- Modeled features in MySQL using a practical schema (tables/columns supporting progression + state)
- Ensured new systems reliably save/load across restarts

## Future-Friendly Design Notes
- Systems were built to be configurable and extensible (add new tasks, new vocations, new reward sets)
- Prefer Lua-level iteration first, then move to C++ only when performance or engine hooks require it

