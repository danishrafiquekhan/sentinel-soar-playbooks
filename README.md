# Sentinel SOAR Playbooks

**Status: in progress** — automated triage playbooks for Microsoft Sentinel, built as Logic Apps.

## What this is
Sentinel automation rules and their underlying Logic App definitions for enriching and triaging alerts automatically.

## Why I built it
Manual first-pass triage (looking up user/IP context, checking sign-in risk) is repetitive and a natural automation target — this shows I can design that automation, not just describe it.

## How it works
Each playbook in `playbooks/` includes the exported Logic App definition (sanitised — no tenant IDs, connection strings, or subscription IDs) and a README explaining what it automates and the design decisions behind it.

## What I learned / trade-offs
_(filled in per playbook — e.g. what triggered false enrichment, where automation should stop and a human should take over)_

## Security note
Exported playbook JSON is sanitised before commit. No real tenant/subscription IDs or connection strings.

## One-time setup after cloning
```bash
git config core.hooksPath .githooks   # enables the gitleaks secret-scan on commit
```
