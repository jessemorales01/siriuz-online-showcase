# Architecture

## Goals
- Fast, reliable UX for **[primary user workflow]**
- Maintainable codebase with clear boundaries
- Secure handling of user data and permissions
- Scales with **[expected growth axis: users/data/events]**

## System Diagram

```mermaid
flowchart LR
  UI[Web UI / Client] --> API[Rails Controllers / API]
  API --> SVC[Service Objects / Domain Layer]
  SVC --> DB[(SQL Database)]
  SVC --> CACHE[(Cache)]
  SVC --> JOBS[Background Jobs / Queue]
  JOBS --> EXT[External Services/APIs]
  API --> OBS[Logging/Monitoring]
