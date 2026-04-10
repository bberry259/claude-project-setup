# Claude Project Templates

A battle-tested framework for managing long-running, multi-session projects with Claude. Built from 40+ sessions across complex projects involving financial systems, multi-server infrastructure, and autonomous services.

## The problem

Claude has no memory between sessions within a project. Every new conversation starts from zero unless you give it structure. Without a system, you end up repeating context, re-litigating decisions, and losing hard-won lessons.

## The solution

A three-document system that acts as persistent memory between sessions, plus supporting files for project setup and Claude Code integration.

### Core documents

**HANDOVER.md** is the current state of the project. What's live, what's decided, what's blocked. Claude reads this first at the start of every session. It gets updated, not appended to. Old state is replaced, not preserved.

**TODO.md** is the active task list. Priority tiers (P1/P2/P3), open questions that block progress, and a strict deletion rule: completed tasks are removed, not marked done. The changelog serves as the archive.

**CHANGELOG.md** is institutional memory. Three sections: Decisions Reversed (what changed and why, preventing re-litigation), Technical Gotchas (hard-won lessons about non-obvious behaviour), and Session Log (brief per-session records).

### Supporting files

**project-instructions-master.md** gets pasted into Claude's Project Instructions field. It sets tone, session workflow, git discipline, source hierarchy, and working conventions. This is the behavioural layer. You will want to customise it for your own working style.

**CLAUDE.md** goes in the root of every repo that Claude Code will work on. It covers project-specific rules, file structure, testing commands, conventions, and a "What NOT to do" section.

## How to use this

1. Fork or clone this repo.
2. When starting a new Claude Project, copy the three core document templates into a `Project Management/` directory in your project's repo.
3. Paste the contents of `project-instructions-master.md` into your Claude Project's Instructions field. Customise the placeholder sections.
4. If the project involves Claude Code, copy `CLAUDE.md` to your repo root and fill in the project-specific details.
5. At the start of every session, Claude reads the living docs before doing anything else.
6. At the end of every session, Claude proposes updates to the three core documents for your approval before committing.

## Key principles

**Facts, not behaviours.** The core documents store factual state. Behavioural instructions (how Claude should write, think, challenge) go in project instructions, not in the living docs.

**One canonical source.** Every piece of information has one home. Repo docs are the primary source of truth for project state. When sources conflict, repo docs win.

**Delete, don't archive.** Completed tasks are removed from TODO.md. If the completion matters, it's recorded in CHANGELOG.md. The active list stays clean.

**Propose, then commit.** Claude proposes documentation updates as text blocks at session end. Changes are committed only after approval. Code changes can be committed directly.

## What this is not

This is not a Claude memory replacement. Claude's memory holds cross-project facts (who you are, your tech stack, your preferences). These templates hold project-specific state that changes every session. The two work together.

This is not prescriptive. Not every project needs every section in every template. Use what fits, delete what doesn't.

## Customisation

The `project-instructions-master.md` file contains opinionated defaults about writing style, formatting, and working conventions. These reflect one person's preferences. You should review and adjust:

- Writing style and banned words/phrases
- Challenge-and-verify expectations
- Model routing preferences (Opus vs Sonnet)
- Git workflow and commit conventions
- Session end workflow (propose vs direct commit)

The core document templates (HANDOVER, TODO, CHANGELOG) are more universal and should work for most projects with minimal changes.

## Contributing

Found improvements through your own multi-session projects? Discovered patterns that work better? Contributions welcome. Open an issue or submit a pull request.

## Licence

This work is licensed under the Creative Commons Attribution 4.0 International Licence (CC BY 4.0).

You are free to share, adapt, and build upon this material for any purpose, including commercial use, as long as you give appropriate credit.

See [LICENSE](LICENSE) for full terms.
