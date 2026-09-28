# Eval Stack · Juno

> Module 6 · Evals & Guardrails. Juno's layered evaluation stack, designed with the **M6 · Eval Stack Designer**. Paste the tool's markdown over this file.

## What "good" means

Every priority Juno posts either cites a real strategy clause or honestly labels itself `unverified` — never a confident guess with no backing. The trust metrics that matter most: citation rate on approved priorities, the 7-day reversal rate (target under 10%, per the AWSpec §9 log), and the `unverified` rate over time — a rising trend means the strategy doc or ticket corpus has gone stale, not that Juno is getting worse.

_____

## The stack

| Layer | Evaluator | What it catches | Threshold / gate |
|---|---|---|---|
| **Code-based** | Automated checks on every run | Missing citation, malformed output schema, `write_roadmap()` called without a PM confirm event, latency/cost breaches (AWSpec §7) | Hard gate — any P0 guardrail failure blocks release |
| **LLM-as-judge** | A second model scores rationale quality against the retrieved clause | A card that's technically cited but the clause doesn't actually support the ranking — citation present, reasoning weak or off-topic | Score below 3/5 routes the item to human review before it can enter the golden set as a passing case |
| **Human** | Weekly spot-check against `06-evals/human-rubric.md` (dimensions, anchors, and disagreement protocol live there, not repeated here) | Judgment calls a machine can't make — actual relevance, tone, whether the priority is genuinely right | Must clear the rubric's pass bar before a prompt, model, or harness change ships |

## Golden set

A curated set of past `#escalations` threads with a known-correct priority rank and citation, seeded from real production cases — including past misses — rather than synthetic examples. Every prompt, model, or harness change is regression-tested against this set before shipping. Grown continuously: every human-rubric disagreement item that gets a resolved score (per the rubric's disagreement protocol) is added. The PM owns it.

_____

## Release gate

A change to Juno's prompt, model, or harness ships only if: all code-based checks pass at 100%, the LLM-judge score on the golden set doesn't regress, and the weekly human rubric review clears its pass bar. Any one failing blocks the release. Two consecutive weekly misses on the human rubric (or an equivalent nightly-check pattern) trigger the first optimization lever — prompt, then model, then data, then architecture — before anything ships.

_____
