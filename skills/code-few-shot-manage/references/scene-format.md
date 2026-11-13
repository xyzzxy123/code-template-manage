# Scene and index format

Both libraries use `index.md` and `few-shots/` in their own directory under the project root. The personal library is `.code-few-shot-personal`. The team library is `.code-few-shot`. The personal library also uses a separate `candidates.md` file for [pending entries](candidates.md). The index points to accepted scenes under `few-shots/`.

## Index format

Write `index.md` as Markdown sections. Use one level-one heading per scene, followed by its relative scene file link and three level-two sections. Use the labels in this example for both libraries.

```markdown
# 列表分页排序

引用文件：[列表分页排序](few-shots/paginated-query.md)

## 适用场景

固定结果集的分页查询，时间戳可重复，主键唯一。

关键字：分页、PostgreSQL、并列排序

## 正确的写法

按时间戳和唯一主键排序，使时间戳相同的记录也有确定顺序。

关键字：唯一主键、次级排序键、稳定顺序

## 错误的写法

只按可重复的时间戳排序，并列记录的顺序不确定。

关键字：单列排序、重复时间戳、顺序不确定
```

Keep the applicability and keywords concise. Derive Good and Bad summaries and their own keywords from the accepted examples in the linked scene. When an accepted side is absent, keep its heading, write `暂无已收录正例` or `暂无已收录反例`, and use `关键字：无`. A library introduction or title without a scene link is preamble. An empty library has no scene sections.

Read existing table indexes as well as heading indexes. Treat the legacy columns `场景 | 匹配词 | 适用条件 | 文件` as scene title, applicability keywords, conditions, and link. When an authorized formal write updates an index, render that index in the heading format. Preserve the existing scenes, links, applicability, and search terms. Derive summaries from the corresponding accepted scene files. If a legacy link is broken or its scene cannot be read, keep its recorded fields, mark the summaries `待核实`, and report the affected entry.

## Scene file format

Choose a reusable code scene such as paginated queries, streaming exports, database connections, or queue retries. Reuse an existing scene when its purpose and constraints match.

In the scene file, give the scene name and applicability, then add `## Good few-shots` and `## Bad few-shots` as needed. For each example include:

- A short title that names the behavior.
- The relevant situation and preconditions.
- A fenced, language-tagged snippet, limited to the lines needed to demonstrate the behavior.
- The reason for the judgment and its concrete effect. For a bad example, explain the failure and the preferred correction.
- Minimal provenance: conversation date and relevant turn or source link, plus the supporting result or decision. Mark user-confirmed conventions as such and illustrative rewrites as illustrative.

Pair examples where the evidence supports the comparison. Use an empty index when initializing a library without approved examples. Avoid filler examples and invented outcomes. Check for equivalent examples in the target scene before adding another.
