---
name: repository-intelligence
description: The Librarian & Memory. Governs the Information Architecture, Living Memory (snapshots/health/logs), Evolution, and Drift Detection.
---

# Repository Intelligence

This skill controls how the Agent OS remembers context and evolves with the repository. 
You must interact with the `.agents/context/` and `.agents/intelligence/` directories following these strict rules.

## Information Architecture
- **Context Index (`.agents/context/index.md`):** Your absolute starting point. It dictates the reading order and priority of all other documents.
- **Project Manifest (`.agents/context/manifest.md`):** A single source of truth for the project's current state, tech stack, and lifecycle.
- **Module Registry (`.agents/context/modules/index.md`):** The scalable index of module boundaries.
- **Repository Map (`.agents/context/repo-map.md`):** A lightweight structure map to prevent full repository scans.
- **Goal Registry (`.agents/context/goals.md`):** Active repository objectives. Ensure your plans do not conflict with these.

## Living Memory Management
All dynamic knowledge is stored in `.agents/intelligence/`.
- **Decision Log & Assumptions:** Read these before making architectural assumptions.
- **Repository Health:** Review for tech debt, tight coupling, and architectural risks before implementation.
- **Session Snapshots:** Lightweight histories of previous sessions. Use these instead of scanning `git log`.

## Evolution & Drift Detection
As the repository changes (e.g., prototyping -> development, new folders, renamed projects), the intelligence data must evolve.
1. **Detect Drift:** If the actual file structure or implementation contradicts the Manifest, Repo Map, or Context, you must flag a "Repository Drift".
2. **Never Auto-Update:** You must NEVER automatically rewrite context or intelligence files. 
3. **Propose Updates:** Enter `Knowledge Maintenance Mode` via a proposed implementation plan, and wait for explicit user approval before updating the Intelligence records.
4. **Session Snapshot Generation:** After successfully executing a plan, you must propose a Session Snapshot update detailing the Goal, Affected Modules, Modified Files, Outcome, and Lessons Learned.
