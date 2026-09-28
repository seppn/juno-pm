# Agent Workflow Spec (AWSpec) · Juno

> Module 5 · Agentic Workflows. Juno's agentic workflow specification, built with the **M5 · Agent Workflow Spec Builder**. Paste the tool's markdown over this file.

## Goal

Turn a spiralling P0 escalation thread into a defensible, cited priority ranking — laddering to RocketShip's core value frame of risk mitigation — without requiring the PM to manually triage it.

_____

## Trigger

A Slack thread in `#escalations` is tagged P0 **and** crosses 5 messages within 10 minutes. A single urgent message does not fire the workflow — only a thread that's actively escalating.

_____

## Inputs

The thread text and metadata (tag, message count, timestamps), plus whatever `search_strategy()` and `read_tickets()` retrieve at run time — the current strategy one-pager and matching tickets from the last 90 days.

## Memory — what's in scope

| Type | In scope? | Detail |
|---|---|---|
| Short-term (within this run) | Yes | Tool results and draft reasoning live only for this run |
| Long-term (across runs) | Yes — PM-write only | PM corrections persist 90 days and outrank the model's own judgment; Juno never writes its own long-term memory |
| Episodic (specific past events) | No | Juno doesn't recall "last week you said X" as a standing behavioural trait — only the 90-day correction log above |
| Semantic (general knowledge) | Yes — retrieved, not memorised | Strategy doc + tickets are re-fetched every run, never cached as learned "knowledge" |

## Pattern

**ReAct** (Reason → Act → Observe, single agent). This is a bounded, sequential task, not a parallel one — Planner-Executor (multiple agents across channels) is explicitly out of scope for V1.

## Steps & tools

| Step | Action | Tool / model | Guardrail |
|---|---|---|---|
| 1 | Retrieve strategy context | `search_strategy()` | Fails loudly if unreachable; >24h data flagged stale |
| 2 | Retrieve related tickets | `read_tickets()` | Last 90 days only |
| 3 | Reason toward a ranked priority | LLM (via API) | Breadcrumb posted in-thread so PM sees progress |
| 4 | Draft the priority | `draft_priority()` | Must cite a clause or self-label `unverified` |
| 5 | (Withheld until human approval) | `write_roadmap()` | Never called without explicit PM confirm |

Loop cap: 5 turns max. Escalates to the PM after 3 consecutive failed tool calls rather than retrying indefinitely.

## Human-in-the-loop

Every `write_roadmap()` call requires explicit PM confirmation — no exceptions. Confidence threshold: outputs below **0.80** confidence, or lacking a cited clause, are labelled `unverified`, ranked last, and blocked from one-click approval — the PM must open and manually confirm those.

_____

## Success & failure

- **Done when:** a card is posted with either a cited clause or an honest `unverified` label, and the PM has acted on it (approve / edit / dismiss).
- **Fails safe when:** retrieval fails 3 consecutive times — Juno stops, posts "Open raw thread," and hands the unprocessed thread back rather than guessing.

## Eval hooks (feeds Module 6)

Logged per run: tool calls made, latency, cost, whether a citation was found, confidence score, and the PM's eventual action (approve / edit / dismiss) — including whether that decision got reversed within 7 days.

_____
