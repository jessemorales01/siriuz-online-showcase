
## docs/ARCHITECTURE.md
```md
# Siriuz Online — Architecture

## Upstream Base
This project is built on a CrystalServer distribution, which is a C++ Open Tibia server emulator derived from The Forgotten Server (TFS) lineage. That implies:
- C++ “engine” handles networking, packet/protocol handling, game loop, performance-critical rules, DB access, Lua bindings
- Lua layer handles gameplay/content and most custom systems
- MySQL persists world/player state

## Core Components

### 1) Client + Protocol Layer
- Tibia Client connects to the server over a defined protocol
- Packets are parsed/validated in the C++ protocol layer before reaching game logic
- Latency-sensitive work stays in C++ when needed (hot path)

### 2) C++ Server Core (Engine)
Responsibilities typically include:
- Connection/session management
- Dispatch/scheduling of game tasks/events
- Game state updates (movement, combat, item interactions)
- Lua runtime integration (binding objects/events to scripts)
- Database I/O for persistence

When I make engine-level changes, they live in the C++ `src/` side because they impact core runtime behavior.

### 3) Lua Scripting Layer (Gameplay + Systems)
Gameplay and content are implemented using server scripting interfaces such as:
- Actions (item use)
- MoveEvents (step in/out, equip logic)
- CreatureEvents (login/logout/death/advance hooks)
- GlobalEvents (timed/server events)
- TalkActions (commands)
- Weapons/Spells (combat/spell hooks)

Many TFS-lineage distros also support “drop-in” scripting via `data/scripts/` (revscriptsys-style registration), which reduces XML wiring and keeps features modular.

My custom gameplay systems are implemented primarily here because it’s the fastest iteration loop without rebuilding the whole C++ core.

### 4) MySQL Persistence
- Player accounts, character state, items, and system data are stored in MySQL
- Schema is initialized from a SQL bootstrap file (commonly `schema.sql` in these distros)
- During development I manage and inspect data using phpMyAdmin via XAMPP

## Data Pack Boundary
The data pack layer typically includes:
- scripts + content definitions (Lua/XML)
- monsters/NPC definitions
- map/world data

The key design principle is separation:
- C++ core stays stable and optimized
- Lua/content systems change frequently and remain modular

## Performance/Operations Notes
- Keep high-frequency logic lightweight (avoid excessive DB calls inside tight loops)
- Use DB reads/writes intentionally (batch where possible; cache where safe)
- Prefer script modularity to avoid monolith “god scripts”
