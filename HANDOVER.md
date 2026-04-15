# HANDOVER.md

## How to use this document

Read this first at the start of every session. It is the single source of truth for the current state of this project.

**What belongs here:** current state, locked decisions with reasoning, infrastructure details, safety rules, known limitations. This document should reflect reality as of the last session. When state changes, update or replace the relevant section. Do not append history here.

**What does NOT belong here:** task lists (TODO.md), session history (CHANGELOG.md), reference material (project knowledge files), or anything that doesn't describe the current state of the project.

---

## Project overview

[One or two sentences: what this project is and what it does.]

## Current state

[Plain summary of where things stand right now. What's live, what's in progress, what's waiting. Update this every session.]

---

## Section menu

Not every project needs every section below. Include the ones that apply. Delete the rest. Add new sections if the project demands it.

### Architecture and key decisions

When to include: any project with technical components or significant design choices.

Format: state the decision, then the reasoning. If a decision has been reversed, move it to CHANGELOG > Decisions Reversed and replace it here with the current decision.

```
Decision: [what was decided]
Reasoning: [why, in one or two sentences]
```

### Machines and environments

When to include: any project that runs on more than one machine, or has distinct environments (local, staging, production).

List each environment with: hostname or identifier, what runs there, how to access it, and any environment-specific configuration.

```
[Environment name]
- Host: [hostname or IP]
- Runs: [services, processes]
- Access: [SSH, URL, credentials reference]
- Notes: [anything non-obvious]
```

### Running services

When to include: any project with persistent processes, cron jobs, or services that need to be running.

For each service: name, where it runs, how to start/stop/check status, and what depends on it.

### Data layer

When to include: any project with databases, data files, or data pipelines.

Cover: what stores data, where it lives, how it's accessed, backup status, and any schema or format details that matter.

### Directory structure

When to include: any project where file layout matters or where Claude Code will be working with the repo.

Keep it to the top two or three levels. Annotate non-obvious directories.

### Accounts and credentials

When to include: any project that uses external services, APIs, or authentication.

For each account: service name, what it's used for, where the credentials are stored (never the credentials themselves), and expiry dates where applicable. Note which credentials are in environment variables vs project files vs secrets managers.

**Never put tokens, keys, or passwords in this document or any other file committed to the repo.**

```
GitHub PAT
- Purpose: allows Claude to clone, commit, and push to the project repo
- Stored in: Claude Project Knowledge file called "Github_access_token"
- Expiry: [date. Check and rotate before it lapses]
- Scope: Contents read/write on [repo name]

[Service name]
- Purpose: [what it's used for]
- Stored in: [where the credentials live]
- Expiry: [if applicable]
```

### Non-negotiable rules

When to include: any project dealing with money, production systems, user data, live services, or anything with real-world consequences.

These are constraints that must be followed in every session regardless of context. They are not suggestions. Examples:

```
- Paper trading is the default. Live trading requires an explicit flag and verbal confirmation.
- Never commit secrets, tokens, or API keys to the repo.
- Test destructive operations in staging before production.
- Do not restart [service name] without checking [dependency] first.
```

### Known limitations and risks

When to include: most projects beyond the trivial.

Things that don't work, known bugs, constraints to work around, risks to monitor. Include workarounds where they exist.

### Security notes

When to include: any project with exposed ports, API keys, user data, or access controls.

Cover: what's exposed, how keys are managed, what access controls are in place, what data sensitivity applies.

---

## Last updated

[Date of last session that modified this document]
