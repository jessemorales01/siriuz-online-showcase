# Siriuz Online (Showcase)

Siriuz Online is a CrystalServer-based online RPG server (Open Tibia lineage) with a C++ core and a Lua scripting layer, backed by MySQL for persistent player/state data. Source code is kept private; this repo documents architecture, stack, and engineering decisions.

## What I Built (End-to-End Ownership)
- Owned features end-to-end: requirements → implementation → testing → deployment/ops support
- Built and maintained gameplay systems primarily in Lua (events/actions/commands), with C++ changes when engine-level support was needed
- Designed/updated MySQL persistence for player/system state and validated data integrity during iteration
- Set up a practical dev workflow using XAMPP + phpMyAdmin for local DB management and quick debugging

## Tech Stack
**Server/Core:** C++ (CrystalServer / TFS-derived OT server)  
**Scripting:** Lua (gameplay + content systems)  
**Database:** MySQL (managed locally via phpMyAdmin / XAMPP)  
**Dev Tools:** XAMPP, phpMyAdmin, Git/GitHub

## Architecture (High-Level)
```mermaid
flowchart LR
  CLIENT[Tibia Client] --> NET[Network Protocol Layer]
  NET --> CORE[CPP Server Core (CrystalServer)]
  CORE --> LUA[Lua Scripting Layer]
  CORE --> DB[(MySQL Database)]
  DEV[XAMPP + phpMyAdmin (Dev)] --> DB
