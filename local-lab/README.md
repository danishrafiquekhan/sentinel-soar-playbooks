# Local lab: TheHive + Cortex (open-source SOAR)

**Status: running, verified end-to-end on 2026-08-29.**

This replaces Microsoft Sentinel's SOAR/playbook role with a fully open-source, self-hosted equivalent — no Azure subscription needed to practice case management and automated enrichment.

## Stack
- [TheHive](https://github.com/TheHive-Project/TheHive) (AGPL) — case/alert management
- [Cortex](https://github.com/TheHive-Project/Cortex) (AGPL) — automated analyzers/responders (the "playbook" layer)
- Cassandra + Elasticsearch — TheHive's storage backend

## Run it
```bash
cd local-lab
echo "APPLICATION_SECRET=$(openssl rand -hex 32)" > .env   # generate your own, never commit this file
docker compose up -d
```
- TheHive: http://localhost:9000
- Cortex: http://localhost:9001

First run of each needs its one-time setup wizard (create the initial admin account/database in TheHive's UI, then link Cortex to TheHive with an API key generated in Cortex's UI). That's a manual step by design — TheHive doesn't ship default credentials.

## What I learned / trade-offs
The `strangebee/thehive:5.4` image refuses to start with `--no-config-secret` in prod mode — despite the flag's name, TheHive (Play Framework under the hood) hard-requires `application.secret` to be set explicitly once outside dev mode. Fixed by generating a real secret with `openssl rand -hex 32` and passing it via `.env` (gitignored) rather than baking it into the compose file.

Also note: Cortex's official image doesn't publish arm64 builds yet, so it runs under x86 emulation on Apple Silicon — noticeably slower to start than TheHive itself, but stable once up.

## Security note
`.env` (containing `APPLICATION_SECRET`) is gitignored — never commit it. This stack has no real credentials for anything external; it's a fully local case-management sandbox.
