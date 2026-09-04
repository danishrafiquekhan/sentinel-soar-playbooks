**TheHive + Cortex, running locally**

My stand-in for Sentinel's SOAR layer while I don't have a paid tenant to build real Logic Apps against. TheHive handles case management, Cortex is the automation/enrichment side — together they're roughly the open-source version of "alert comes in, gets a case, gets enriched, gets acted on."

Stack: TheHive and Cortex (both AGPL), backed by Cassandra and Elasticsearch.

**Running it**
```bash
cd local-lab
echo "APPLICATION_SECRET=$(openssl rand -hex 32)" > .env
docker compose up -d
```
TheHive on :9000, Cortex on :9001. First time you open either, you'll hit a setup wizard — creating the admin account, then generating a Cortex API key and pasting it into TheHive to link the two. No default login ships with either of these, which I actually appreciate.

**The thing that tripped me up**
The TheHive image has a `--no-config-secret` flag that sounds like it disables the requirement for an application secret. It doesn't — try that in prod mode and it just crashes on startup complaining the secret isn't set, flag or no flag. Turns out you still need to generate a real one and pass it through `.env`. Once I did that it came up fine.

Also, Cortex doesn't have an arm64 image yet, so on my Mac it's running under emulation — takes a while longer to become responsive than TheHive does, but it gets there.

`.env` never gets committed — it's the only thing in this folder that's actually sensitive, since it holds the application secret.
