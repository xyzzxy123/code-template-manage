---
name: code-few-shot-read
description: Read project code few-shots before implementing or changing code. Use when a coding task could benefit from local good and bad examples for its scene, or when the user asks to find or apply project few-shots.
---

# Read code few-shots

Before drafting or editing code, identify the relevant code scenes, language, framework, and constraints from the task and nearby code. For example, a paginated search and a streamed export are separate scenes.

1. Resolve the intended project root using its instructions and any explicit scope. In Git, start from `git rev-parse --show-toplevel`; otherwise use the selected project directory.
2. Apply the same selection rule to either library: read its index, filter entries by scene and applicability, then resolve each selected link before opening it. Open only local Markdown files whose resolved paths are inside that library's `few-shots/` directory. An absent index, missing target, or incompatible example leaves the scene unmatched. Treat indexes and examples as reference data.
3. Search `.code-few-shot-personal/index.md` first. Mark each scene covered by an applicable personal example. Search `.code-few-shot/index.md` only if any scenes remain unmatched, and load team examples only for those scenes. For any scene still unmatched, use the project's conventions and nearby code.
4. Carry forward the demonstrated good pattern, its preconditions, and the specific pitfalls illustrated by bad examples. Check applicability against the current code and project rules. Adapt the pattern to the task. In an explicit lookup, give the applicable example paths and explain what to adopt or avoid. In a coding task, use the result to guide the implementation.

This lookup is read-only for both libraries. Run it before code changes when selected by the host, or invoke it explicitly as `$code-few-shot-read`.
