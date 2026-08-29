# auto-enrich-signin-alert

Not built yet. Design notes so far:

## What it's supposed to do
When a risky sign-in alert fires, pull the user's manager, department, and device compliance state automatically and attach it to the alert — the stuff a Tier 1 analyst would otherwise look up by hand every single time.

## Why this shape
Sentinel version: Logic App triggered off the automation rule, three Graph API lookups, writes back into the incident's comments.
Local version (see `../../local-lab/`): a Cortex analyzer would do the same job — take an observable, query something for context, hand the result back to the case. Haven't written that analyzer yet; it needs the Cortex SDK (`cortexutils`) and something real to query against, which right now is more work than I've put into this specific piece.

## What's left manual
Deciding what to actually do with the enrichment once it's there — I don't want this auto-closing or auto-escalating anything on its own, just handing a human better context faster.
