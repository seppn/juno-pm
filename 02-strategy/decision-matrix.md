# AI Solution Decision Matrix · Juno

> Module 2 · Strategy. The build / buy / fine-tune / partner call, made with the **M2 · AI Solution Decision Matrix**. Paste the tool's markdown over this file.

## The decision

How Juno gets its intelligence: build a model in-house, buy access via API, or fine-tune an open model on RocketShip's data. Decided now because it determines the entire M3 harness — what Juno can and can't ground its answers in.

_____

## Options scored

| Option | Cost | Speed | Control | Moat | Risk | Score |
|---|---|---|---|---|---|---|
| **Build** | High — no ML team to build or maintain a model | Slowest — months before anything ships | Highest, but nobody to exercise it | None — a general-purpose model built in-house has no edge over a frontier vendor's | High — an unmaintained model degrades silently | **1 / 5** |
| **Buy / API** | Low — usage-based, no infra to run | Fastest — ship in days, re-prompt as product evolves | Medium — constrained to the vendor's capabilities, but sufficient | Comes from the RAG layer (RocketShip's own strategy doc + tickets), not the model | Low — vendor reliability is the only new dependency | **5 / 5** |
| **Fine-tune** | Medium-high — training cycles + ongoing retraining cost | Slow — each retrain is a project, not a prompt edit | High over model behaviour, low over freshness | Illusory — RocketShip's ticket taxonomy and product surface shift monthly, so any fine-tune goes stale inside a quarter | Medium-high — stale fine-tune looks confident and is wrong | **2 / 5** |

## Recommendation

**Buy via API, grounded with RAG.** Juno's advantage was never going to come from a better base model — it comes from what it retrieves (RocketShip's live strategy doc and tickets) and what it refuses to do without evidence. Fine-tuning would freeze exactly the thing that changes every month; building would spend the one resource RocketShip doesn't have (engineering headcount) on a problem a vendor has already solved.

_____
