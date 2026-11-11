<div align="center">
<pre>
            +-----------+       +--------------+      +---+         +---+  &#32;
          /            / \     /              / \    /    |\      /    / \ &#32;
        +    +--------+   +   +----+    +----+   +  /     | +   /     /   +&#32;
       /   +  \        \ /     \  /    / \    \ /  /      | | /      /   / &#32;
      /   / \  +--------+       +/    /   +----+  /       | /       /   /  &#32;
     /   /   +                  /    /   /       /   +    +    +   /   /   &#32;
    /   /   /                  /    /   /       /   /|       //   /   /    &#32;
   /   +   /                  /    /   /       /   / |     /+/   /   /     &#32;
  +    +--------+            /    /   /       /   /  |   /  /   /   /      &#32;
  |            / \          /    /   /       /   /   | /   /   /   /       &#32;
  +-----------+   +        +----+   /       +---+   /+    +---+   /        &#32;
   \           \ /          \    \ /         \   \ /  \  / \   \ /         &#32;
    +-----------+            +----+           +---+    +    +---+          &#32;
</pre>
</div>

<p align="center"><strong>CTM: WTF! AI, look at the code you wrote for me!</strong></p>

<p align="center"><em>Yell first. Then have the AI record what worked and where it screwed up. Next time, maybe you'll have less to yell about.</em></p>

<h2 align="center">Use skills and few-shot code examples to build up your repo's coding standards and teach AI how to take a shit properly.</h2>

<p align="center"><a href="README.md">简体中文</a></p>

---

The repo has no consistent coding standards. This ancient shit pit has passed through generations of developers. Depending on which file the AI copies, the same feature can come out in three different styles.

By the time the feature is done, the code is a tangled mess. I open the diff, can't tell where to start, and spend another afternoon arguing with the AI.

**I haven't gotten anything done, and I'm already the punching bag.**

I tried writing standards in `README.md` and adding “Read the README before changing anything” to `AGENTS.md`. Every time I hit another problem, I added another rule. Before long, even the README was full of shit.

CTM! You've already done the yelling. Keep the version you got right, the original counterexample, and the reason you changed it.

---

## The ways AI shits

1. **Constipation.** The function is bare. Reviewers have to guess what needs to be true before calling it and what happens at the edges.
2. **The runs.** The code is already clear, and the AI still explains it line by line. Eight hundred lines out of a thousand are comments. Good luck finding the code.
3. **Projectile shitting.** A few lines that would read just fine in one function get scattered across several. To check one return value, you have to hop back and forth between a whole chain of functions.
4. **Can't hold it. Shit first.** The feature is done. Nobody checked the runtime or complexity. Then you open the diff and find a database query for every record in a loop.
5. …

## What to do after it shits

Clean up the mess in front of you. Then use `$ctm` to capture the good and bad examples from the review, along with when they apply and why. Confirm the candidates you want to keep. The next time you change similar code, look them up before editing.

**Keep shitting. Take it slow, find a rhythm, and do it right.**

## The idea behind the skills

Every time you're done yelling at the AI, have it review what happened. Record what you yelled about, why you yelled, and what changed afterward.

**Yell and record it → Review and save it → Read before the next change → Write the code → Review it and yell again when something goes wrong.**

Everyone on the team can use their own judgment to record corrections from review as personal candidates. At closeout, pick the examples worth reusing and confirm which ones go into your personal library. Explicitly save examples the whole team should use to the team library.

### code-few-shot-manage

Once a review explains what went wrong and how to fix it, use [`code-few-shot-manage`](skills/code-few-shot-manage/SKILL.md) to record it. It keeps the code snippets, when they apply, the reasoning, and where the decision came from. The good and bad examples get separate candidate IDs so you can decide what to do with each one.

```text
Project root/
├── .code-few-shot-personal/
│   ├── candidates.md    # Personal candidates awaiting review
│   ├── index.md         # Index of accepted personal examples
│   └── few-shots/       # Accepted examples grouped by scenario
└── .code-few-shot/
    ├── index.md         # Index of team examples
    └── few-shots/       # Accepted examples shared with the team
```

A retrospective records personal candidates by default. An explicit request to save directly writes accepted examples to the personal library and updates its index. To save to the team library, select it explicitly and confirm which examples to share. In Git projects, keep the personal library untracked and add `/.code-few-shot-personal/` to the root `.gitignore`.

### code-few-shot-read

Before implementing a feature, fixing a bug, or editing existing code, use [`code-few-shot-read`](skills/code-few-shot-read/SKILL.md) to look up accepted examples for the scenario. It checks the personal library first, then looks in the team library for scenarios still unmatched. If neither has an applicable example, follow the project's conventions and nearby code. A pending candidate becomes searchable here once it joins the library.

### code-few-shot-check

At closeout, use [`code-few-shot-check`](skills/code-few-shot-check/SKILL.md) to review candidates or audit the accepted examples.

- **Review candidates.** Compare them with accepted examples for duplicates and conflicts, then choose which IDs to add, delete, or leave pending. When adding one, the skill verifies the accepted example and index before removing its pending entry.
- **Audit the libraries.** Check for conflicts, examples worth merging, personal examples already covered by the team library, and index problems. The skill numbers and previews changes, then applies the items you confirm.

### ctm

**So pissed off you don't know what to do next? Hand it to CTM! Keep yelling and hit CTM. It'll tell you what to do now.**

Invoke [`ctm`](skills/ctm/SKILL.md) manually, for example with `$ctm` or `/ctm`. It starts with any action you explicitly requested, then looks at where you are in the recent conversation.

- **About to write code.** It uses `code-few-shot-read` to pull up examples for the relevant scenarios.
- **Done yelling and you've explained what was wrong and why.** It uses `code-few-shot-manage` to record the lesson.
- **Wrapping up or asking to review candidates.** It uses `code-few-shot-check` for the scope you requested.

If the context leaves the next step unclear, CTM asks what you want to do first. Once the choice is clear, it follows the selected skill's workflow.

## CTM in practice

These excerpts come from a PHP endpoint review. Project-specific paths and class names have been simplified. The decisions and outcomes are the ones from the review.

### Call CTM while you're explaining the fix

> **User**　`$ctm` We usually want descending order here. When you use `orderBy()`, spell out the direction and use descending by default.

The AI changed the list to `->orderBy('id', 'desc')`. A regression test verified the order `[29, 24, 21]`. All 15 tests and 141 assertions passed.

CTM chose `code-few-shot-manage` and drafted a candidate for query ordering. The good example was `->orderBy('id', 'desc')`. The counterexample was `->orderBy('id')` with no direction. This project uses descending order by default and spells out `asc` when the feature needs ascending order.

### Wrap up and see what is worth keeping

> **User**　`$ctm` Look back at what I corrected.

The AI found three candidates from the review that were still waiting to be saved.

| Candidate | What to keep |
| --- | --- |
| Query ordering | Always give `orderBy()` a direction. This project defaults to `desc`. |
| PHPDoc and nullable results | Annotate the `first()` assignment with `@var InspectionDetail\|null` so the IDE knows the model type and that it can be null. |
| Model states and labels | Define constants for every valid state and use them as keys in the label map. Queries can reference the states they need. |

> **User**　Add all three.

The AI saved the examples and counterexamples to the personal library, updated the index, and verified Git ignore coverage. The current candidate review uses `P-<UUID>` IDs so you can decide which entries to accept, delete, or leave pending.

### Audit the library and decide what the team should share

> **User**　`$ctm` Check the code examples.

`code-few-shot-check` read **10 scenarios and 44 examples** in the personal library, including 24 good examples and 20 counterexamples. It reported the findings for the user to decide on. At that point the project had no team library or pending candidate file.

| ID | What the AI found | What the user decided |
| --- | --- | --- |
| `C-P-01` | Good examples in the transaction tests used `orderBy('id')` with no direction, conflicting with the ordering example. | Use explicit `desc` in the affected examples and update the expected test order. |
| `C-P-02` | The role eager-loading example didn't explain what `with()` loads or why. | Add a comment explaining the relationship's purpose. |
| `R-P-01` | An older code excerpt referred to fields that had since changed. | Keep older excerpts that still demonstrate the rule. Record the review date and decision as provenance. |

The AI updated the personal examples for the first two findings and withdrew the third suggestion. The user then explicitly asked CTM to check and add the team standards. CTM checked the personal library and saved the two approved rules on **sort direction** and **Eloquent eager-loading comments** to the team library.

### Follow up with an independent code review

> **User**　Have an independent subagent review the implementation for logic errors, bugs, and possible improvements.

The reviewer found two nullable type annotations in the working copy that hadn't made it into the staged version. It also flagged an extra relationship field returned by `detail.*` and suggested batching the per-date conflict lookups. This review examined the implementation itself. The examples in the library were available to check the coding decisions along the way.
