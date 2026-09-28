# AI PRD · Juno

> Module 3 · Harness. The AI product requirements doc specifying the six surfaces around the model, built with the **M3 · AI PRD Builder** (harness design from the **M3 · Harness Architecture Decider**). Paste the tool's markdown over this file.

## Problem & user

RocketShip's PMs lose 2+ hours a week manually triaging P0 escalations across Slack, Jira, and Notion, and prioritisation currently goes to whoever escalates loudest rather than what's most urgent. The user is a RocketShip PM drowning in signal collapse with no budget to hire more PMs.

_____

## Solution overview

Juno is a tool-using copilot (not an autonomous agent — its core output, a priority ranking, can't be machine-verified, so a human must approve every write). It retrieves grounding context, drafts a ranked, cited priority, and hands control back to the PM at every write action.

_____

## The six harness surfaces

**1 · Context** — What Juno reads: the current strategy one-pager plus the last 90 days of tickets. Re-syncs whenever the source doc changes. Data older than 24 hours is served with a staleness label rather than silently. If a source is unreachable, Juno fails loudly (refuses to draft) rather than guessing. Excludes PII and other teams' data.

**2 · Tools** — The exact verb list, and why it's short:
| Tool | What it does | Write? |
|---|---|---|
| `search_strategy()` | Retrieves relevant strategy doc sections | Read |
| `read_tickets()` | Retrieves matching Jira tickets | Read |
| `draft_priority()` | Produces a ranked, cited draft | Draft only |
| `write_roadmap()` | Commits a priority to the roadmap | Write — requires confirm |

Deliberately **not** given: `send_email`, `post_slack`, `delete`. Juno cannot contact anyone or destroy anything.

**3 · Loop** — Max 5 turns per request. Escalates to a human after 3 consecutive failed tool calls rather than retrying indefinitely. Target p95 latency under 8 seconds. Cost capped at $0.12/task.

**4 · Memory** — Rationale for a given priority persists for the length of the sprint, then expires. PM corrections persist 90 days and **outrank the model** — if a PM overrides Juno's ranking, Juno doesn't re-suggest the same ranking next time. Only the PM writes to memory; Juno never writes its own memory. Nothing crosses between teams. Everything has a TTL — stale memory is worse than no memory.

**5 · Permissions** — Read and draft actions run automatically. `write_roadmap()` always requires human confirmation. Anything customer-facing is fully blocked in V1 — Juno cannot contact a customer under any condition.

**6 · Verification** — Every priority Juno produces must cite a specific strategy-doc clause. If it can't, the output is labelled `unverified` and ranked last — never silently dropped, never presented with false confidence.

_____

## Requirements

| # | Requirement | Priority | Acceptance criteria |
|---|---|---|---|
| 1 | Every priority cites a source clause or is labelled `unverified` | Must | No priority ships without a citation or an explicit unverified flag |
| 2 | `write_roadmap()` requires explicit PM confirmation | Must | No roadmap write occurs without a human click |
| 3 | Stale context (>24h) is visibly flagged | Must | Staleness label renders wherever Juno surfaces a source |
| 4 | Escalate after 3 consecutive tool failures | Must | No infinite retry loop; human notified |
| 5 | p95 latency under 8 seconds | Should | Measured in eval harness (M6) |
| 6 | Cost per task under $0.12 | Should | Measured in eval harness (M6) |

## Out of scope

Customer-facing communication of any kind. Autonomous roadmap writes (no human-in-the-loop bypass). Cross-team memory sharing. A full evaluation harness — stubbed here, built in Module 6.

_____
