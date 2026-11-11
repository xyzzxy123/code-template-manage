# Scene and index format

Both libraries use `index.md` and `few-shots/` in their own directory under the project root. The personal library is `.code-few-shot-personal`. The team library is `.code-few-shot`. The personal library also uses a separate `candidates.md` file for [pending entries](candidates.md). The index points to accepted scenes under `few-shots/`.

In the index, use one row per scene with the columns `场景 | 匹配词 | 适用条件 | 文件`. The file cell is a relative Markdown link such as `[分页查询](few-shots/paginated-query.md)`. Keep search terms and applicability short. Choose a reusable code scene such as paginated queries, streaming exports, database connections, or queue retries. Reuse an existing scene when its purpose and constraints match.

In the scene file, give the scene name and applicability, then add `## Good few-shots` and `## Bad few-shots` as needed. For each example include:

- A short title that names the behavior.
- The relevant situation and preconditions.
- A fenced, language-tagged snippet, limited to the lines needed to demonstrate the behavior.
- The reason for the judgment and its concrete effect. For a bad example, explain the failure and the preferred correction.
- Minimal provenance: conversation date and relevant turn or source link, plus the supporting result or decision. Mark user-confirmed conventions as such and illustrative rewrites as illustrative.

Pair examples where the evidence supports the comparison. Use an empty index when initializing a library without approved examples. Avoid filler examples and invented outcomes. Check for equivalent examples in the target scene before adding another.
