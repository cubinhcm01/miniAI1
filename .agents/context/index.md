# Context Index

This is the definitive entry point for loading project context. You must read the documents in the exact order specified below. Do not guess what to read.

## Reading Order & Priority

1. **[manifest.md](file:///c:/Users/kaybe/OneDrive/Máy%20tính/miniAI1/.agents/context/manifest.md)** (Required)
   - Read this first to understand the project at a high level.
2. **[goals.md](file:///c:/Users/kaybe/OneDrive/Máy%20tính/miniAI1/.agents/context/goals.md)** (Required)
   - Ensure your proposed solution aligns with active repository goals.
3. **[repo-map.md](file:///c:/Users/kaybe/OneDrive/Máy%20tính/miniAI1/.agents/context/repo-map.md)** (Required)
   - Use this to locate directories without scanning the repository.
4. **[modules/index.md](file:///c:/Users/kaybe/OneDrive/Máy%20tính/miniAI1/.agents/context/modules/index.md)** (Required if modifying logic)
   - Look up the specific modules you are modifying. Then read the individual module docs (e.g., `modules/domain.md`) for boundaries and dependencies.
5. **[../intelligence/decision-log.md](file:///c:/Users/kaybe/OneDrive/Máy%20tính/miniAI1/.agents/intelligence/decision-log.md)** (Optional but Highly Recommended)
   - Review past architectural decisions relevant to your task.
6. **[../intelligence/repository-health.md](file:///c:/Users/kaybe/OneDrive/Máy%20tính/miniAI1/.agents/intelligence/repository-health.md)** (Required before Implementation)
   - Check for technical debt or architectural risks in the area you are touching.

*Note: Documentation always overrides source code. If the code contradicts these documents, stop and ask the user.*
