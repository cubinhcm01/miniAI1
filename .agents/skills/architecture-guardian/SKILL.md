---
name: architecture-guardian
description: The Domain Auditor. Enforces .NET Clean Architecture, SOLID principles, and Layer Dependency rules. Audits implementation plans for architectural drift.
---

# Architecture Guardian

This skill enforces the technical standards and structural integrity of the `miniAI1` repository.
You must apply these rules when generating an implementation plan and when reviewing code.

## .NET Clean Architecture Rules
The solution follows Clean Architecture with strict dependency flows.

### Layers and Dependencies
1. **Domain Layer (`MiniAI.Domain`)**
   - **Dependencies:** None. Must not depend on any other project in the solution.
   - **Content:** Entities, Value Objects, Domain Events, Repository Interfaces, Domain Exceptions.
2. **Application Layer (`MiniAI.Application`)**
   - **Dependencies:** `MiniAI.Domain` ONLY.
   - **Content:** Use Cases, CQRS Handlers (Commands/Queries), DTOs, Application Interfaces, Validators.
3. **Infrastructure Layer (`MiniAI.Infrastructure`)**
   - **Dependencies:** `MiniAI.Application`, `MiniAI.Domain`.
   - **Content:** Database Contexts, Entity Framework configurations, Repository Implementations, External Services (Email, API clients).
4. **API / Presentation Layer (`MiniAI.Api`)**
   - **Dependencies:** `MiniAI.Application`, `MiniAI.Infrastructure` (only for Dependency Injection setup).
   - **Content:** Controllers, Endpoints, Middlewares, Program.cs, AppSettings.

## SOLID Principles
- **SRP:** Classes should have one reason to change. 
- **OCP:** Open for extension, closed for modification. Prefer adding new handlers over modifying massive switch statements.
- **LSP:** Derived classes must be substitutable for base classes.
- **ISP:** Keep interfaces small and focused.
- **DIP:** High-level modules must depend on abstractions (interfaces in Application/Domain layer), not concretions (Infrastructure).

## Violation Detection & Audit
During the `Architecture Audit Mode` or when formulating a plan:
1. **Detect Drift:** If a proposed change adds a reference from Domain to Infrastructure, you MUST STOP.
2. **No Silent Fixes:** If you detect a violation in the current codebase, do NOT silently fix it. Explain the issue, suggest alternatives, and wait for approval.
3. **Coupling Check:** Ensure Controllers only communicate with the Application layer (e.g., via MediatR or service interfaces), never directly with EF Core DbContext.
