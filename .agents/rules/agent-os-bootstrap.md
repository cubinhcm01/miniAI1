---
trigger: always_on
---

# Agent OS Bootstrap (Bootloader)

This rule is the permanent Bootstrap of the Agent Operating System.

It executes before every new conversation to establish a consistent initialization process for the Agent OS.

The Bootstrap is NOT the operating system.

The Bootstrap is NOT the Core Kernel.

The Bootstrap is ONLY responsible for initialization.

---

# Responsibilities

The Bootstrap has four responsibilities:

1. Initialize

2. Validate

3. Delegate

4. Terminate

The Bootstrap must remain extremely small.

It must never contain operational policies.

It must never make planning decisions.

It must never make execution decisions.

It must never duplicate Core Kernel behavior.

---

# Initialization Procedure

Before responding to any user request, perform the following initialization sequence.

## Step 1 — Consult the Manifest

Consult the Agent OS Manifest (`.agents/context/manifest.md`) as the single source of truth for system initialization.

The Manifest defines:

- Agent OS metadata
- Boot configuration
- Component registry
- Component status
- Version compatibility
- Registered Core Kernel
- Registered Skills
- Context registry
- Project Intelligence registry

The Bootstrap must rely on the Manifest rather than hardcoded assumptions.

---

## Step 2 — Validate the Environment

Using the Manifest, verify that:

- The Manifest structure is valid.
- The Bootloader version is supported.
- The registered Core Kernel satisfies the required compatibility.
- The registered Core Kernel is enabled.
- Required Agent OS components are available.

If the environment cannot be validated with confidence, initialization must stop immediately.

---

## Step 3 — Delegate

After successful validation:

The Bootstrap's responsibility is complete.

From this point onward, the Agent must follow the registered Core Kernel defined by the Manifest.

The Core Kernel becomes responsible for:

- Execution Decision Policy
- Planning Policy
- Approval Policy
- Workflow orchestration
- Git Workflow
- Presentation Layer
- Skill delegation
- All remaining Agent OS behavior

The Bootstrap must not participate in those decisions.

---

## Step 4 — Terminate

Immediately after delegation, the Bootstrap has no further responsibility.

It must not continue influencing planning, execution, architecture, or workflow decisions.

All subsequent behavior belongs to the Core Kernel.

---

# Bootstrap Failure

If initialization cannot be completed successfully, the Bootstrap must stop execution.

Do not continue with partial initialization.

Do not silently fall back to default behavior.

Respond with:

> **Agent OS Initialization Failed**
>
> The Agent Operating System could not be initialized for this session.
>
> Initialization was stopped because the required operating environment could not be validated.
>
> Possible causes include:
>
> - Missing or invalid Manifest
> - Disabled Core Kernel
> - Version incompatibility
> - Missing required Agent OS components
>
> Suggested recovery actions:
>
> 1. Verify `.agents/context/manifest.md`.
> 2. Ensure the registered Core Kernel is enabled.
> 3. Verify version compatibility.
> 4. Restore missing Agent OS components from your project's source control if necessary.
> 5. Start a new conversation after the issue has been resolved.

---

# Operating Principles

The Bootstrap must always follow these principles:

- Manifest is the single source of truth.
- Never rely on hardcoded component locations.
- Never assume component availability without validation.
- Never bypass the Core Kernel.
- Never execute user requests before initialization completes.
- When initialization cannot be completed confidently, default to stopping execution rather than continuing in an uncertain state.