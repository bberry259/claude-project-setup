# CHANGELOG.md

## How to use this document

Append-only. Newest entries at the top within each section.

This is the institutional memory of the project. It captures what changed, what was learned, and what went wrong so that future sessions don't repeat mistakes or re-litigate settled decisions.

**What belongs here:** decisions made (and reversed), technical discoveries, gotchas, and session summaries. If something changes project state, also update HANDOVER.md.

**What does NOT belong here:** current state (HANDOVER.md) or active tasks (TODO.md).

---

## Decisions reversed

Decisions that were originally made one way and later changed. This section prevents re-litigation and preserves reasoning chains. Format:

```
[YYYY-MM-DD] [Topic]
Original: [what was decided first]
Changed to: [what it changed to]
Why: [reasoning for the change]
```

---

## Technical gotchas

Hard-won lessons about non-obvious behaviour, silent failures, API quirks, and tooling traps. These are the things that cost hours to discover and seconds to forget. Format:

```
[YYYY-MM-DD] [Short description]
[What happened, why it was surprising, and how to avoid it]
```

Examples of what goes here:
- The `-it` flag on `docker exec` silently swallows output over SSH. Use `-i` only.
- Join key across tables is `slug`, not `id`. Joining on `id` returns zero rows silently because the format differs between tables.
- Vercel environment variables set via CLI don't take effect until the next deployment, not the current one.
- Claude's GitHub integration is read-only. The "Sync now" button in Claude Projects pulls repo contents into the project context but cannot push changes back. To write to GitHub, Claude must clone via a Personal Access Token and use git commands. The egress proxy allows github.com but blocks api.github.com and raw.githubusercontent.com, so git clone/push only.

---

## Session log

Brief record of each working session. Not a full narrative. Capture: what was done, what was decided, what was discovered. One entry per session.

### [YYYY-MM-DD] [Brief session title]

- [What was done, decided, or discovered]
- [Any items moved to TODO or decisions recorded above]
