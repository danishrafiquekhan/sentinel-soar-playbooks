**sentinel-soar-playbooks**

Automated triage: the part of a SOC job that is mostly "look up this user, check this IP, was this device compliant" over and over. Every alert like that is a candidate for a playbook instead of a human doing the same three lookups fifty times a week.

This repo was originally going to be pure Sentinel Logic Apps. It still will be, eventually, but I do not have an Azure tenant with Sentinel enabled sitting around for free, so the actual running automation right now is TheHive + Cortex instead (open source, runs on my own machine, see `local-lab/`). The Logic App designs still get written up in `playbooks/` since that is the specific skill the job postings ask about. I am just not pretending I have deployed something I have not.

Exported playbook JSON gets sanitised before it is committed: no tenant IDs, no connection strings.

**One-time setup after cloning**
```bash
git config core.hooksPath .githooks
```

For the principles behind when to automate vs keep a human in the loop, and a full walkthrough of each playbook's design decisions, see [Part 7](https://github.com/danishrafiquekhan/security-lab-notes/blob/main/parts/07-soar-automation-principles.md) of `security-lab-notes`.
