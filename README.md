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

## Setting up a Claude Project

When you create a Claude Project, you have two places to add context. Understanding the distinction matters.

**Project Instructions** is a text field in the Project settings. Whatever you put here applies to every conversation in that Project. This is where behavioural rules live: tone, workflow, session structure, git conventions. Paste the contents of `project-instructions-master.md` here and customise it for your working style.

**Project Knowledge** is for reference material that Claude can search during conversations. It supports file uploads, text snippets, and a native GitHub integration. When you connect a GitHub repo here, Claude can read the repo contents directly as project knowledge. The files appear as read-only reference within each conversation, but you update them between conversations via git (commits, merges, PRs), and Claude picks up the changes in the next conversation.

This is how the three core documents work: they live in a GitHub repo, connected to your Project via the GitHub integration in Project Knowledge. Claude reads them at the start of each session. At the end of a session, Claude uses a PAT to push updates back to the repo. The updated docs are then available for the next conversation automatically.

### Step by step

1. **Fork this repo.** Make your fork private (see repo structure below). Customise the templates for your own use.

2. **Connect the repo to your Project.** In your Claude Project, go to Project Knowledge, click the **+** button, and select **GitHub**. Connect your forked repo. Claude can now read all the files in the repo as project knowledge.

3. **Create a GitHub Personal Access Token (PAT).** This is needed for Claude to write back to the repo (committing updates, creating branches and PRs). Go to GitHub > Settings > Developer settings > Personal access tokens. Fine-grained tokens are recommended. Scope the token to your project management repo only, with these permissions:
   - **Contents**: Read and write (required for Claude to update the living docs)
   - **Pull requests**: Read and write (required if you want Claude to create PRs for you to review before merging)
   - Set a sensible expiry. Shorter is safer. You can always generate a new one.

4. **Add the PAT to Project Knowledge.** Click **+** in Project Knowledge and select **Add text content**. Name it something like `Github access token` and paste the token value. Claude will use this to authenticate when pushing changes. Do not commit this token to any repo.

5. **Paste `project-instructions-master.md` into Project Instructions.** Customise the placeholder sections for your project.

6. **If using Claude Code**, copy `CLAUDE.md` to the root of your development repo and fill in the project-specific details.

7. **Start a session.** Claude reads the living docs from your connected repo before doing anything. At the end of each session, Claude proposes updates for your approval, then commits and pushes once approved.

### Repo structure: keep docs and code separate

Your project management documents (HANDOVER.md, TODO.md, CHANGELOG.md) should live in their own private repo, separate from your development code. Reasons:

- **Access control.** The PAT you give Claude only needs access to the docs repo, not your codebase. Smaller blast radius if a token leaks.
- **Cleaner history.** Documentation commits (session notes, decision logs) don't clutter your development commit history.
- **Different audiences.** Your dev repo might be public or shared with a team. Your project management docs contain decisions, priorities, and sometimes sensitive context that doesn't belong in a public codebase.

A typical layout:

```
github.com/you/myproject              # development repo (public or private)
github.com/you/myproject-docs          # project management repo (private)
  ├── HANDOVER.md
  ├── TODO.md
  └── CHANGELOG.md
```

If your project is simple enough that a separate repo feels like overkill, a `Project Management/` directory in your dev repo works fine. Just be aware of the trade-offs above.

### PAT hygiene

- Use fine-grained tokens scoped to specific repos, not classic tokens with broad access.
- Set the shortest expiry you can tolerate. 30 days is a reasonable default.
- When a token expires, Claude will get a 401 or 403 error on push. Generate a new token and update the Project Knowledge file.
- Never commit tokens to a repo. They live in Project Knowledge only.
- If you suspect a token has been exposed, revoke it immediately in GitHub > Settings > Developer settings > Personal access tokens.

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
