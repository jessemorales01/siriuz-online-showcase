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

Key Components
1) C++ Server Core (CrystalServer)

Handles networking, combat loop, movement, creatures, events, scheduling, and performance-critical behavior

Exposes hooks / event points consumed by Lua scripts

2) Lua Scripting Layer

Implements gameplay systems and customization without rebuilding the entire core

Typical responsibilities:

Vocation logic (e.g., Monk)

Quest/task systems (e.g., hunting tasks)

Guild / party systems (e.g., guild tamers)

Item/monster behavior tweaks, NPC interactions, reward logic

3) Persistence: MySQL

Stores player data, inventories, progression, system state

Managed locally using phpMyAdmin during development

Emphasis on safe updates and consistent schema usage across systems

4) Local Dev Environment (XAMPP + Tools)

Used to host local MySQL/phpMyAdmin for development and testing

Enables quick iteration across schema changes + scripts + server configuration

Operational / Performance Notes (High-Level)

Optimizations focus on reducing expensive loops, minimizing repeated database access, and keeping hot paths in C++

Lua is used for flexibility; performance-sensitive logic stays in the core when needed

Debugging is a mix of logs + controlled reproduction (spawn scenarios, targeted test characters, safe configs)

What I Owned (End-to-End)

Designing systems (requirements → rules → data needs)

Implementing Lua systems and (when needed) touching C++ for engine-level support

Schema changes in MySQL to persist new mechanics

Testing gameplay scenarios and edge cases (exploits, timing, persistence, concurrency)
