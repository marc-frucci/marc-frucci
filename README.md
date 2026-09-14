# Marc Frucci

Marc Frucci — Product. Builder. Systems.

This isn't a code portfolio. It's a record of how I work: the frameworks I use to decide what's worth building, and the builds that came out of applying them.

## The kinds of problems I work on

Problems without an owner tend to find their way to me. The ones where the ask is vague, the workflow crosses three teams' boundaries, nobody's agreed on what "done" looks like, and the org knows something is broken but hasn't figured out what to build in response. Or the ones where everyone knows a decision needs to be made but nobody has built the frame to make it — so it stalls, and the work waits.

That's true whether it's a complex enterprise workflow at work or my wife asking me to help her stop losing craft-fair leads on paper napkins. Different stakes, same shape of problem: real need, no defined product yet.

## How I work

Whatever the scale, the approach tends to look roughly the same:

1. **Name the real problem.** Not the first version of the request — the thing actually underneath it. Most requests arrive as a proposed solution ("build us a dashboard," "make an app for this"). I go looking for the workflow and the failure mode behind that ask before I agree the ask is right.
2. **Define the smallest useful boundary.** What has to be true for this to be worth building, what can stay manual, what's explicitly out of scope for now — and why. I write the exclusions down, not just the inclusions.
3. **Build or guide the smallest credible version.** Working software over a deck. I'd rather ship something narrow that's actually running than something broad that's still hypothetical.
4. **Validate with real operators.** Not a demo audience — the person who will actually use this thing under real conditions, with real stakes if it's wrong.
5. **Hand it off clean.** The goal isn't to be the permanent dependency. It's to leave something that runs without me: documented, owned, operable by someone else.

I don't default to AI, automation, or a new system just because one is available. A lot of my work is deciding that the answer is smaller than what was asked for — a manual step is fine, a spreadsheet is fine, deferring is fine — and being able to say why.

## What's in this repo

- **`frameworks/`** — the reasoning tools I actually use before I build anything, starting with [Foundry](frameworks/foundry.md), the pre-build workshop I run every idea through: is this worth building, what's the smallest version that proves it, what should I explicitly not build yet.
- **`builds/`** — write-ups of real things I've built:
  - [CraftCatcher](builds/craftcatcher/README.md) — a booth-side lead-capture tool for my wife's craft business: fast notes in, AI-structured request out, nothing invented that wasn't said.
  - [Dinner Draw](builds/dinner-draw/README.md) — a weekly dinner-rotation board for the family, generated from a saved meal catalog, replacing the blank-page "what are we eating this week" moment.

  This repo documents the product thinking behind these builds; it isn't a source-code archive.
- **`case-studies/`** — enterprise case studies available for discussion rather than published here. The folder [README](case-studies/README.md) summarizes the types of problems I've worked on.
- **`notes/`** — shorter, less polished thinking — [how I think](notes/how-i-think.md) through problems in real time, not the cleaned-up version.

This repo is being built in public, in the same way I build everything else: smallest credible version first, then iterate against what's actually useful.

## Why this exists

Much of the work that best shows my judgment as a product person isn't something I can publish directly. This repo makes the underlying thinking visible through shareable frameworks and personal builds.

If you want to see how I reason before I build, start with `frameworks/foundry.md`. If you want to see that judgment applied to AI, start with `builds/craftcatcher/`. If you want to see the same discipline applied without AI, start with `builds/dinner-draw/`.
