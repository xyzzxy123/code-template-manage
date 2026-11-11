# Personal few-shot candidates

Store pending examples in the project's `.code-few-shot-personal/candidates.md`. Resolve the library and candidate path within the selected project and report targets that escape it. Keep pending examples outside the formal index and scene files. Create the file on first capture with the heading `# 个人 Few-shot 候选`. The team library consists of accepted scenes and their index.

## Entry format

Use one `## P-<UUID> <title>` heading per pending example. Generate a UUID once and preserve it across updates and reviews. Give each Good/Bad example its own ID so the user can choose either one. Related examples share the scene and may reference each other's IDs. Preserve these fields under each heading:

- **场景、分类、适用条件** — Reusable scene, Good or Bad, and concrete prerequisites.
- **代码** — Minimal language-tagged fenced snippet. Mark illustrative rewrites.
- **理由** — Observed or explained behavior and why it matters. Include the correction for a Bad example.
- **现场上下文** — A short account of the task, the triggering code or failure, the relevant correction, and the user or reviewer decision. Include the minimal sanitized excerpts needed to review this later from the file alone. Distinguish observed results from explanations and proposed outcomes.
- **来源** — Date and available chat turn, review location, or source link. Preserve enough context locally even when the source cannot be reopened.

## Capture and review

1. Before adding an entry, read existing candidates and relevant personal scenes. Reuse the existing ID when the scene, conditions, judgment, and demonstrated behavior are equivalent. Add new supporting evidence to that entry when it contributes context. When the personal formal library already captures the same example, report that match. Leave formal files for explicit formal writes.
2. Review from `candidates.md` and report each ID with its scene, conditions, code, rationale, original context, and source. Check relevant accepted examples for duplicate behavior or conflicts and show the proposed personal scene or the reason to keep the item pending. Ask which IDs to add, delete, or leave pending. A missing file or heading-only file means there are no stored candidates. Report a read error or malformed entry separately and keep its contents available for repair.
3. Execute the user's specified actions on the selected IDs. Re-read the entries and planned target files. If material content has changed since approval, show the changed proposal for confirmation. Preserve other entries.
   - **Add to personal few-shots**: Use `code-few-shot-manage`'s formal-write procedure and [scene and index format](scene-format.md). Preserve the snippet, applicability, rationale, and provenance. Verify the accepted scene and index link first, then remove the approved entry from `candidates.md`. When an equivalent accepted example is already verified, reuse it and remove the approved pending entry. If formal persistence or verification fails, keep the pending entry and report what remains to complete. This order permits a retry after formal persistence.
   - **Delete candidate**: Remove the approved candidate block from `candidates.md`. Keep the heading when the queue becomes empty. Formal files are outside the candidate deletion scope.
   - **Leave pending**: Keep the existing entry for a later review.
4. Verify the affected files and report the IDs added, deleted, or still pending. If candidate cleanup fails after a formal write, report that the accepted sample exists and that the pending ID still needs cleanup.

## Personal Git writes

Before any personal write in Git, run `git ls-files -- <personal-directory>`. If it returns tracked entries, report them and defer the personal write. Run `git check-ignore --no-index -- <path>` separately for every planned personal write or deletion path, including candidate, index, old and new scene paths as applicable. All checks must return 0. For empty library initialization, check the index and a prospective scene path. If ignore coverage is missing and the task permits changing `.gitignore`, add the anchored `/.code-few-shot-personal/` rule at the Git root, or its Git-root-relative equivalent for a scoped subproject, and repeat the checks. Otherwise report the affected paths and defer the personal write.
