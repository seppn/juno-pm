# Trust-Gap Mitigations · Juno

> Module 4 · AI-Native UX. Trust gaps surfaced with the **M4 · AI-UX Trust Gap Checker**, and how each is mitigated. Paste the tool's markdown over this file.

## Trust gaps

| Gap | Where it shows up | User cost | Mitigation |
|---|---|---|---|
| **Hallucination** (3/5 — highest open risk) | Juno drafts a priority ranking that sounds confident but isn't grounded in a real strategy clause | A PM ships a wrong priority believing it's evidence-based — the single worst failure mode, since it looks identical to a correct one | Citation-or-`unverified` gate: every priority must cite a real clause or is visibly flagged `unverified`, ranked last, and blocked from one-click approval |
| **Opacity — no "why"** (black-box, 2/5) | The PM sees a rank but not the reasoning behind it | Erodes trust over time — PM can't tell if Juno reasoned well or got lucky | Cited clause link on every card, plus an in-thread breadcrumb ("Scanning strategy…") that shows the retrieval step happening, not just a final answer |
| **No user control** (2/5) | PM might feel Juno's ranking is final or automatically actioned | PM stops trusting the tool if they think they've lost the wheel | Every card requires an explicit confirm click for any roadmap write; inline edit and "Not a P0" dismiss are always available, with dismiss persisting 90 days |

## Highest-priority fix

**Hallucination**, because it's the only gap where the failure is invisible at the moment it happens — a wrong-but-confident rank looks identical to a right one until someone checks the source. The other two gaps (opacity, control) degrade trust gradually; this one can cause one bad ship. This is why Juno ships at readiness Level 2 rather than Level 3: a "reliable validator" that sometimes says `unverified` beats a "magical liar" that always sounds certain.

_____
