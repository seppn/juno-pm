# Agent Control Panel · Juno

> Module 5 · Agentic Workflows. The operator's control surface for Juno, from the **M5 · Agent Control Panel**. Paste the tool's markdown over this file.

## Autonomy level

**Bounded-autonomous.** Juno plans and executes the retrieval-and-reasoning steps (search, read, draft) entirely on its own once triggered — no human approval needed to *produce* a draft. But it is hard-capped before anything reaches the roadmap: `write_roadmap()` never fires without an explicit PM click. It's not merely "supervised" (a human doesn't approve every step) or "assisted" (it doesn't wait for a prompt) — but it's also nowhere near fully autonomous, since the one action with real consequences is always gated.

_____

## Controls

- **Kill switch:** No single in-flight process to interrupt — each run is stateless and completes in under 8 seconds. To stop Juno entirely, an admin disables the `#escalations` trigger integration; no new threads get picked up. Any individual card can be dismissed by the PM with one click ("Not a P0"), which also suppresses that thread for 90 days.
- **Rate / cost caps:** Max 5 reasoning turns per run. Cost capped at $0.12/task. Target p95 latency under 8 seconds.
- **Escalate-on-stuck:** After 3 consecutive failed tool calls, Juno stops retrying, posts "Open raw thread" in the escalation thread, and hands it back to the PM unprocessed rather than guessing.

## Monitoring

The operator (PM) watches: the `unverified` rate (how often Juno can't find a citation — a rising rate signals stale or missing strategy context), the approve/edit/dismiss split on cards (a high edit or dismiss rate signals Juno's ranking logic needs tuning), and the 7-day reversal rate on approved priorities (the core trust metric from Module 2 — target under 10%). These feed the Module 6 eval stack.

_____

## Permissions

| Action | Autonomous? |
|---|---|
| Retrieve strategy doc / tickets | Yes — no approval needed |
| Draft a priority ranking | Yes — no approval needed |
| Write to the roadmap | **No — requires explicit PM confirmation, every time** |
| Contact a customer or post outside `#escalations` | **Never** — not a permission Juno has at all in V1 |

_____
