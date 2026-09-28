# AI Strategy One-Pager · Juno

> Module 2 · Strategy. Built with the **M2 · AI Strategy One-Pager Builder** (informed by the Three-Layer Model Mapper). Paste the tool's markdown over this file.

## The bet

Juno is RocketShip's AI prioritisation engine: it turns scattered Slack/Jira/Notion signals into a ranked, evidence-cited risk list, so PMs stop losing the week to whoever escalates loudest.

_____

## Three-layer model

- **Model layer:** Buy via API (no fine-tune). RocketShip has no ML team and the product surface changes monthly — a fine-tuned model would freeze exactly the thing that moves. A general-purpose LLM called through an API, re-prompted as the product evolves, is the right cost/speed trade-off for a V1.
- **Data / retrieval layer:** Grounded with RAG — retrieval over the strategy one-pager and the last 90 days of tickets, not the model's own training knowledge. This is the layer that makes Juno's output defensible: every claim traces to a real source ID, not a guess. (Shortcut explicitly rejected: an ungrounded LLM would be faster to ship and impossible to trust.)
- **Product layer:** A ranked, cited risk list a PM can approve in one click, delivered where they already work (Slack thread), not a new dashboard to remember to check.

## Why now

RocketShip is in **signal collapse** — every new customer, integration, and feature adds signals a PM must track, and headcount is frozen while the roadmap keeps growing. The loudest voice currently wins prioritisation, not the most urgent one. There's budget for AI tooling but not for more PMs, so the value has to come from software, not headcount.

_____

## Success metric

Weekly prioritisation cycle time drops from 2 hours to 30 minutes, **and** fewer than 10% of Juno's ranked decisions get reversed by a human within 7 days — speed without a trust regression.

_____
