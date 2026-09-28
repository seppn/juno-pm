# AI-Native User Flow · Juno

> Module 4 · AI-Native UX. The end-to-end user flow, designed with the **M4 · AI User Flow Architect**. Paste the tool's markdown over this file.

## Entry point

Juno never requires the PM to open an app or type a query. The entry point is environmental: a Slack thread in `#escalations` gets tagged P0 **and** crosses 5 messages within 10 minutes. That threshold — not a single message — is the trigger, filtering out routine chatter and firing only when a thread is genuinely spiralling.

_____

## The flow

1. **Trigger fires** — thread hits P0 + 5 messages/10 min. Juno starts working silently; no message posted yet.
2. **Capture & Retrieve** — Juno reads the thread, calls `search_strategy()` and `read_tickets()` against the last 90 days.
3. **Reason** — Juno drafts a priority ranking with a rationale. A breadcrumb note ("Scanning strategy…") shows in-thread so the PM knows something is happening, not stalled.
4. **Act** — `draft_priority()` produces the ranked draft. No roadmap write happens yet.
5. **Surface** — Juno posts a reply card in the *same* `#escalations` thread (no new channel, no dashboard to remember): rank, one-line rationale, a link to the cited strategy clause, a confidence label, and a single button — **"Add to roadmap."**
6. **Confirm / Correct** — the PM approves (triggers `write_roadmap()` with confirmation), edits the ranking inline, or dismisses with **"Not a P0"** (which persists for 90 days so Juno won't re-flag the same thread).

## AI moments

- **The draft card itself** — the only place Juno's output appears; always shows its confidence label alongside the rank, never presents an `unverified` item with the same visual weight as a cited one.
- **The confirm button** — a single explicit human action gates every roadmap write. Nothing commits without it.
- **Inline edit** — the PM can correct the rank directly in the card rather than rejecting the whole draft.
- **"Not a P0" dismiss** — a one-click undo path that also teaches Juno (via M3's memory surface) not to re-flag that thread for 90 days.

_____

## Fallbacks

- **Unverified output:** if Juno can't cite a strategy clause, the card is labelled `unverified` and ranked last — and critically, **cannot be approved with the single "Add to roadmap" click**; it requires the PM to open and manually confirm, adding friction on purpose where confidence is low.
- **Tool failure:** after 3 consecutive failed tool calls (per the M3 Loop surface), Juno stops retrying and posts "Open raw thread" as a fallback link, handing the PM back the unprocessed thread rather than guessing.
- **Stale context:** if the strategy doc is >24h old, the card visibly flags this rather than presenting stale grounding as current.

_____
