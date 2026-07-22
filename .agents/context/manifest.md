# Project Manifest: miniAI1

This document provides a single, unified view of the repository.

- **Project:** miniAI1
- **Architecture:** .NET Clean Architecture
- **Technology Stack:** C#, .NET (version pending), ASP.NET Core API
- **Repository Layout:**
  - `src/MiniAI.Api/`: Presentation / API endpoints
  - `src/MiniAI.Application/`: Application logic, interfaces, CQRS
  - `src/MiniAI.Domain/`: Core entities and domain rules
  - `src/MiniAI.Infrastructure/`: Data access, EF Core, external services
- **Coding Standards:** C# standard conventions, SOLID principles, CQRS pattern, MediatR (assumed).
- **Current Development Phase:** Prototype / Initial Setup
- **Supported Platforms:** Cross-platform (.NET Core)
- **AI Rules:** Managed by Agent Operating System (see `.agents/skills/core-kernel/SKILL.md`)
- **Repository Status:** Freshly initialized template. Domain and features are not yet implemented.
