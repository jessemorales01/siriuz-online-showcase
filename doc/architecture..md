# Architecture

Siriuz Online is a CrystalServer-based online RPG server with a C++ core and Lua scripting layer. It’s designed to support custom gameplay systems while keeping the runtime stable and maintainable.

## Goals
- Stable, low-downtime gameplay server with predictable performance
- Fast iteration on game content and rules via Lua scripting
- Clean separation between core engine (C++) and game logic/content (Lua)
- Reliable persistence (MySQL) for player state, items, quests, systems, and logs

## High-Level System Diagram

```mermaid
flowchart LR
  CLIENT[Tibia Client] --> NET[Network Protocol Layer]
  NET --> GAME[C++ Server Core (CrystalServer)]
  GAME --> LUA[Lua Scripts (Game Logic)]
  GAME --> DB[(MySQL)]
  ADMIN[Admin Tools / phpMyAdmin] --> DB
  DEV[XAMPP Local Dev (Windows)] --> GAME
  DEV --> DB
