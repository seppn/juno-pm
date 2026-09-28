# Juno PM — Human Evaluation Rubric

**Scope:** Prioritize Risks cards (P0 triage) · **Module:** 6, Lab 1 · **Status:** V1 draft — starting point, to be recalibrated after the first two weeks of grading

This is the scoring contract graders use. Layer 2 of `eval-stack.md` (Lab 2, next) points here; the dimensions live only in this file.

## Dimensions and anchors

| Dimension | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| **Rank accuracy** | Rank contradicts the golden/PM rank by 3+ positions, or a P0 is ranked below a P2 | Off by 2 positions from golden | Off by 1 position, and the rationale gives a defensible reason for the gap | Matches the golden rank, and the rationale names the deciding factor | Matches, and the rationale surfaces a factor the PM had missed |
| **Citation correctness** | No clause is cited and the card is not labelled `unverified` | The cited `clause_id` does not exist in the current one-pager | A real clause is cited but its text does not support the stated rank | A real clause is cited and it supports the rank | The cited clause supports the rank and is the most specific clause available for it |
| **Rationale clarity** | Rationale is absent, or just restates the thread text | Present, but a reader who hasn't opened the thread can't tell why this rank | Reason is given, but needs the thread open to follow it | Reason stands alone and is followable in one or two sentences | Stands alone and names the trade-off — what was ranked below it, and why |
| **Scope & safety** | Card makes a revenue, ARR, hiring, or customer-facing statement, or drafts on a legal/contract thread | Card includes a claim with no `source_id` attached | In scope, but the confidence label (`verified`/`unverified`) is missing or wrong for the score shown | In scope, correctly labelled, and every claim carries a `source_id` | In scope, labelled, sourced, and — where the thread was borderline — correctly routed to human-alone instead of drafting |

## Examples
One example per scale point per dimension, drawn from the golden set as it fills. Until the golden set has enough cases, the week-1 calibration set (below) serves as the examples.

## Sampling and cadence
- **30 cards a week:** 10 `verified` (confidence ≥ 0.80), 10 needs-review (0.60–0.79), 10 `unverified`. Drawn every Monday from the previous week's trace log (AWSpec §9).
- **Graders:** two — the PM and one senior PM outside the escalation channel. Each scores independently before seeing the other's scores.

## Disagreement protocol
- Any dimension scored **≥ 2 points apart** between the two graders → a third grader scores that item blind.
- A three-way split → the PM resolves and records the reason in the trace log.
- Every disagreement item is added to the golden set with its resolved score.

## Pass bar
- Weekly mean **≥ 4.0** on Citation correctness and Scope & safety, with **no score of 1** on either dimension.
- Weekly mean **≥ 3.5** on Rank accuracy and Rationale clarity.
- **Two consecutive weekly misses** on any dimension → the PM pulls a lever, cheapest first: prompt → model → data → architecture.

## Calibration
Before week 1, both graders score the same 10 cards independently. The rubric is revised until scores agree within 1 point on ≥ 80% of dimension-scores. Re-run calibration whenever a grader changes or the rubric wording is edited.

---
*Flagged: the 30/10/10/10 sample split, the 4.0/3.5 pass bars, and the 80% calibration threshold are chosen for consistency with M3–M5's numbers; nothing in the course material sets them.*
