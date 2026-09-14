# CraftCatcher

A booth-side lead-capture tool: fast notes in during a live conversation, an AI-structured follow-up record out, reviewed before it's saved.

## The problem

My wife runs a craft business and sells at in-person craft fairs. A customer will often like an existing piece but want a custom variation — different wording, a different color, a different size — and say so in a single, fast, half-finished sentence while she's mid-conversation with someone else already waiting. Writing that down by hand, or trying to fill out a proper order form in the moment, breaks the conversation and loses detail. The realistic failure mode isn't "no system" — it's a paper napkin with half a phone number and a description that made sense for about an hour and then didn't.

This isn't an order-taking problem. Nothing has been agreed to yet — no price, no final spec, sometimes not even a firm yes. It's an opportunity-capture problem: get enough down, fast, that someone can follow up later and pick the conversation back up accurately.

## Who this is for

Two people, two different moments:

- **The booth operator** (me, standing in for my wife when she's the one talking to the customer, or her directly) — needs to capture a name, some way to reach the person, and whatever was said, in the time it takes to say it.
- **The follow-up owner** (my wife) — opens the tool later, away from the noise of the booth, and needs to understand who to contact, what they wanted, what's already known, and what's still an open question — without needing the operator to reconstruct the conversation from memory.

The customer is the subject of the record, not a user of the tool.

## Constraints of the real environment

- A live conversation, often with another customer already waiting.
- A laptop, not a phone — the booth setup favors keyboard entry over a mobile form.
- Intermittent or no reliable internet at a fairground, which means the AI step has to be optional, not load-bearing.
- Zero tolerance for losing the lead. A failed API call is an inconvenience; a lost contact is the actual failure.

## The smallest credible boundary

The V1 boundary is deliberately narrow: capture a name, a phone or email, and raw free-form notes; optionally structure those notes with AI; let the operator review and correct before saving; persist the result; show it later in a simple list.

Explicitly out of scope for V1, and why: customer-facing intake (the operator, not the customer, drives capture), reference photo upload (no demonstrated need yet), shipping address and payments (this is a lead, not an order), quoting or pricing (requirements aren't resolved yet), a product catalog, customer accounts, automated customer messaging, and any CRM state beyond a three-value status. None of these were deferred because they'd be hard — they were deferred because nothing about the actual booth workflow has shown they're needed yet.

## The workflow

1. Customer expresses interest in a custom version of something.
2. Operator types the customer's name, available contact info (phone and/or email), and raw notes — as fast and unstructured as the conversation actually was.
3. The notes are optionally sent through an AI structuring step.
4. The result — item, a one-line summary, known details, unresolved details, whether follow-up is needed — is shown to the operator before anything is saved.
5. The operator corrects anything wrong and saves.
6. The record persists with a numbered ID, the structured fields, and the original raw notes, unchanged, side by side.
7. Later, away from the booth, the follow-up owner opens the requests list and sees enough to act without replaying the conversation.

## What AI does

Turns hurried shorthand into a predictable shape: an item/request type, a short summary that doesn't change the customer's intent, a list of details actually stated, and a list of details still missing.

## What AI is explicitly forbidden to do

Invent or infer any customer requirement that wasn't actually said. If a detail is missing, it goes in the unresolved list — it is never guessed at or filled in. If the AI call fails, is unavailable, or returns something that doesn't validate against the expected shape, the tool does not block the save or silently drop information: the lead is saved as-is, flagged as not yet structured, with the raw notes fully intact.

## Product decisions worth naming

- **AI is an assist, not a dependency.** The save path has to work with a flaky fairground connection or no API key at all. A raw, unstructured lead is a fully valid saved state, not an error state.
- **Review before save, always.** The AI's output is a proposal, not the record. The operator sees it and can correct it before it's persisted — the model's output never becomes the permanent record silently.
- **Two states, not one.** Whether the AI successfully structured a lead (`structured` vs. `raw`) is tracked separately from where that lead is in the follow-up lifecycle (`new` / `contacted` / `closed`). Conflating "did AI understand this" with "have we followed up" would have made both harder to reason about.
- **Raw notes are never discarded.** Even after structuring and editing, the original free-form notes stay attached to the record, because the structured version is a lossy summary and the raw version is the source of truth if anything's in dispute.

## What's still manual, and why

Following up with the customer happens entirely outside this tool — a phone call or a text, not an automated message. At the volume a single crafter's fair realistically produces, manual follow-up should be sufficient. Automating outreach was excluded, not deferred for lack of time — there's no evidence yet from real use that it's needed.

## Current state

CraftCatcher is built and runs end-to-end locally: capture, optional AI structuring, review, save, and a requests list all work, and the persistence, schema-validation, and AI-failure fallback paths are covered by unit tests. It has not yet been used at a live fair — the first real-world test, and the first real signal on whether the follow-up owner can act on a saved lead without the operator's memory filling in gaps, is still ahead of it.

## The next bounded step

Run it at one real fair, unmodified, and see whether the follow-up owner can act on what's saved without needing the operator to reconstruct anything. That result — not another round of features — determines what actually needs to change next.

## What this demonstrates

The instinct here wasn't "my wife needs an app." It was noticing a specific, recurring failure — good leads lost to the format they were captured in — and asking what the smallest possible intervention was before reaching for a bigger one. The AI boundary here — assist, never block; structure, never invent — comes down to letting the tool do the part a person shouldn't have to do by hand, without letting it quietly become the source of truth for something it didn't verify.
