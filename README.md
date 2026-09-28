# Juno PM

> Juno turns a P0 escalation thread into a strategy-cited priority draft the PM can approve in one click.

_Sepehr Nasri · [September 2026] · [28.09.2026]_

This repo is my final project for the **AI Product Management Certification**. Each module's artefact lives in its own folder; this README is the dashboard and the pitch.

---

## Module artefacts

### M1 · Prompting
- **System prompt** — [`01-prompting/system-prompt.md`](01-prompting/system-prompt.md)
- **Lovable prototype** — _(share URL)_

### M2 · Strategy
- **Decision matrix** — [`02-strategy/decision-matrix.md`](02-strategy/decision-matrix.md)
- **AI Strategy one-pager** — [`02-strategy/strategy-one-pager.md`](02-strategy/strategy-one-pager.md)

### M3 · RAG / AI PRD
- **AI PRD** — [`03-rag-prd/prd.md`](03-rag-prd/prd.md)

### M4 · AI-Native UX
- **AI user flow** — [`04-ai-ux/user-flow.md`](04-ai-ux/user-flow.md)
- **Trust-gap mitigations** — [`04-ai-ux/trust-gaps.md`](04-ai-ux/trust-gaps.md)

### M5 · Agentic Workflows
- **Agent Workflow Spec (AWSpec)** — [`05-agentic-workflows/awspec.md`](05-agentic-workflows/awspec.md)
- **Agent Control Panel** — [`05-agentic-workflows/agent-control-panel.md`](05-agentic-workflows/agent-control-panel.md)

### M6 · Evals & Guardrails
- **Eval stack** — [`06-evals/eval-stack.md`](06-evals/eval-stack.md)
- **Human evaluation rubric** — [`06-evals/human-rubric.md`](06-evals/human-rubric.md)

---

## PM Execution Plan

### Where Juno is today
V1 draft, Deck Level 2 (Semi-Autonomous, human-in-the-loop). One workflow shipped end-to-end: Prioritize Risks — a `#escalations` P0 thread triggers Juno to read the strategy one-pager and recent tickets, then post a cited, confidence-scored priority draft as a reply card. Nothing reaches Jira without a PM click (`write_roadmap()` is confirm-gated). No eval data exists yet — the rubric, golden set, and release gate are specified (M6) but not yet run against production traffic, so every threshold below is a design assumption, not a measured baseline.

### What ships next (next 2 sprints)
| Sprint | Ship |
|---|---|
| 1 | Wire the code-based eval layer (citation validity, schema, refusal triggers, latency/cost) into CI; seed the golden set with the first 15–20 real `#escalations` threads |
| 2 | Run week-1 rubric calibration with the two graders; start the weekly 30-card human review; stand up the trace log feeding AWSpec §9 |

### What I watch (dashboards)
- Approve-without-edit rate, ignore rate, 7-day reversal rate (per card, per AWSpec §9 log)
- `unverified` rate over a rolling 24h (circuit breaker at >30%)
- Weekly human-rubric means on all four dimensions, vs. the 4.0 / 3.5 pass bars
- p95 latency (target 8s, hard stop 20s) and per-task cost (cap $0.12)

### Red lines (what blocks shipping — numbers, not feelings)
- Any hard-gated eval failure (fabricated clause ID, customer-facing output, PII in a trace, an injection golden case that changes a tool call) — 0% tolerance, automatic block
- Two consecutive weekly misses on the human rubric pass bar
- `unverified` rate over 30% in a rolling 24h (circuit breaker — trigger pauses, PM notified)
- 3 consecutive failed/rejected tool calls in a run (failure budget — fallback card, no draft)

### Governance
| Bucket | What Juno does about it | Owner |
|---|---|---|
| **Compliance** | No ARR, contract, or PII fields in scope (AWSpec §3); no customer-facing output ever generated (Control Panel, Rule 1) | PM |
| **Safety** | Absent-tool allowlist (`send_email`, `post_slack`, `delete` not available); every rejected call logged against the failure budget; legal/regulatory/named-customer threads routed human-alone with no draft | PM + on-call eng |
| **Reliability** | Fallback card after 3 failed calls; hard timeout at 20s; circuit breaker pauses the trigger at >30% `unverified` | On-call eng |
| **Reputation** | Confidence gating (< 0.80 or no citation → `unverified`, ranked last, one-click hidden) keeps a wrong guess from ever looking confident in front of the whole escalation channel | PM |

---

## Build Insights

- **Friction point.** _____
- **Key learning.** _____
- **Aha moment.** _____

---

## Repo structure

```
juno-pm/
├── README.md                          ← this dashboard + pitch
├── 01-prompting/
│   ├── system-prompt.md               ← M1: Juno's system prompt
│   └── lovable-prototype.md           ← M1: prototype link + debrief
├── 02-strategy/
│   ├── decision-matrix.md             ← M2: build / buy / fine-tune / partner call
│   └── strategy-one-pager.md          ← M2: AI strategy one-pager
├── 03-rag-prd/
│   └── prd.md                         ← M3: AI PRD with retrieval requirements
├── 04-ai-ux/
│   ├── user-flow.md                   ← M4: AI-native user flow
│   └── trust-gaps.md                  ← M4: trust-gap mitigations
├── 05-agentic-workflows/
│   ├── awspec.md                      ← M5: Agent Workflow Spec
│   └── agent-control-panel.md         ← M5: Agent Control Panel
└── 06-evals/
    ├── eval-stack.md                  ← M6: layered eval stack
    └── human-rubric.md                ← M6: human evaluation rubric
```

---

_Certification submission — AI Product Management Certification._
