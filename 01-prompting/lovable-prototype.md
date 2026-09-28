# Lovable Prototype · Juno

> Module 1 · Prompting. The clickable Lovable prototype that brings the system prompt to life.

## Prototype link

_Not built. Given the timeline, priority went to the system prompt and the rest of the harness/agent/eval spec, which are the substance of the certification. No live URL to share._

_____

## What it demonstrates

_Intended to demonstrate: pasting a raw transcript in, and getting back Juno's three jobs (Opportunity Brief, Draft Spec, Risk table) as structured, evidence-cited output rather than free text — proving the system prompt's refusal rules and citation discipline hold up outside a chat window._

_____

## Debrief

- **What worked:** The system prompt itself was fully specified and tested conversationally — refusal conditions, citation format, and the `INSUFFICIENT EVIDENCE` behaviour all work as designed against sample transcripts.
- **What broke / felt like a toy:** No UI was built to wrap it, so this was never tested inside an actual click-through prototype.
- **What I'd change next pass:** Build the Lovable screen first, even a rough one, before writing the full prompt — would have surfaced UI-level gaps (empty states, failure states) earlier instead of only in the self-review.
