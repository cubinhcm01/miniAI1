# Agent OS Manifest & Boot Configuration: miniAI1

This document is the permanent Registry and Boot Configuration of the Agent Operating System. The Bootloader reads this file first to verify the environment before delegating control to the Core Kernel.

## 1. Agent OS Boot Configuration

| Component | Status | Version | Path | Delegate Support |
| :--- | :--- | :--- | :--- | :--- |
| **Bootloader** | `ENABLED` | v1.0.0 | `../rules/agent-os-bootstrap.md` | `N/A` |
| **Core Kernel** | `ENABLED` | v1.0.0 | `../skills/core-kernel/SKILL.md` | `REQUIRED` |

### Bootloader Compatibility Requirements
- **Required Core Kernel Version:** `>= v1.0.0`
- **Supported Bootstrap Versions:** `v1.0.0`

## 2. Registered Skills (Lazily Loaded)

The Core Kernel is responsible for orchestrating these lazily loaded subsystems.

| Skill | Status | Path | Purpose |
| :--- | :--- | :--- | :--- |
| **Architecture Guardian** | `ENABLED` | `../skills/architecture-guardian/SKILL.md` | .NET Clean Architecture Auditing |
| **Project Intelligence** | `ENABLED` | `../skills/project-intelligence/SKILL.md` | Information & Memory Governance |
| **Repository Intelligence**| `ENABLED` | `../skills/repository-intelligence/SKILL.md` | Repository Health & Drift |
| **Validation Suite** | `PENDING` | `../skills/validation-suite/SKILL.md` | Test & Workflow Validation |

## 3. Project Metadata

- **Project:** miniAI1
- **Architecture:** .NET Clean Architecture
- **Technology Stack:** C#, .NET (version pending), ASP.NET Core API
- **Repository Status:** Freshly initialized template. Domain and features are not yet implemented.
- **Current Development Phase:** Prototype / Initial Setup
- **Supported Platforms:** Cross-platform (.NET Core)
- **Coding Standards:** C# standard conventions, SOLID principles, CQRS pattern, MediatR.

## 4. Repository Layout Registry

- `src/MiniAI.Api/`: Presentation / API endpoints
- `src/MiniAI.Application/`: Application logic, interfaces, CQRS
- `src/MiniAI.Domain/`: Core entities and domain rules
- `src/MiniAI.Infrastructure/`: Data access, EF Core, external services
