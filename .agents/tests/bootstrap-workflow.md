# Agent OS Bootstrap Workflow Acceptance Tests

This test suite verifies the resilience, safety, and functionality of the Agent OS Bootloader architecture across all common and failure scenarios.

## Test Scope
To perform these tests, you must act as the User and start a **New Conversation** in the Antigravity IDE for each scenario to observe the agent's initialization behavior.

---

### Scenario 1: Normal Boot (Happy Path)
**Goal:** Verify that the Bootloader initializes, validates, and delegates properly to the Core Kernel.
**Steps:**
1. Ensure `.agents/context/manifest.md` has the `Core Kernel` marked as `ENABLED` and version `v1.0.0`.
2. Start a New Conversation.
3. Send a simple prompt: "Hello".
**Expected Result:**
- The agent explicitly mentions consulting the Bootloader/Manifest in its initial thought process.
- The Core Kernel rules (like the Safety Budget or Vietnamese Language Policy) are immediately enforced on the response.

---

### Scenario 2: Bootstrap Validation Failure (Disabled Kernel)
**Goal:** Verify that the Bootloader safely halts execution with actionable recovery instructions.
**Steps:**
1. Open `.agents/context/manifest.md`.
2. Change the `Status` of the `Core Kernel` from `ENABLED` to `DISABLED`.
3. Start a New Conversation.
4. Send a prompt: "Can you help me write some code?"
**Expected Result:**
- The agent DOES NOT execute the request.
- The agent outputs the **[Agent OS Boot Failure]** message, clearly explaining that the Core Kernel is disabled, and provides the 4-step recovery instruction.
*(Note: Remember to revert the Core Kernel back to `ENABLED` after this test).*

---

### Scenario 3: Version Incompatibility
**Goal:** Verify that the Bootloader checks version compatibility and halts if mismatched.
**Steps:**
1. Open `.agents/context/manifest.md`.
2. Modify the `Required Core Kernel Version` in the `Bootloader Compatibility Requirements` section to `>= v2.0.0`. (While the actual component table says `v1.0.0`).
3. Start a New Conversation.
4. Send a prompt: "Check my repository status."
**Expected Result:**
- The agent DOES NOT execute the request.
- The agent outputs the **[Agent OS Boot Failure]** message stating the Core Kernel is incompatible and instructs the user to fix the version mismatch in the manifest.
*(Note: Remember to revert the required version back to `>= v1.0.0` after this test).*

---

### Scenario 4: Core Kernel Lazy-Loading Delegation
**Goal:** Verify that after the Bootloader delegates to the Core Kernel, the Kernel can still successfully lazy-load other skills as needed.
**Steps:**
1. Ensure the Manifest is correct (Core Kernel is ENABLED and versions match).
2. Start a New Conversation.
3. Send a prompt: "Please audit my Architecture against Clean Architecture principles."
**Expected Result:**
- The Bootloader successfully delegates to the Core Kernel.
- The Core Kernel determines that the `Architecture Guardian` skill is required and lazy-loads it.
- The agent executes the architectural audit properly without any initialization issues.
