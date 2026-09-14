# Dinner Draw

A weekly dinner-rotation board: a low-friction way to turn "what are we eating this week" into an answer, generated from meals we already know we like.

## The problem

Every Sunday, the same question came up: what are we eating this week. Nobody wanted to own the answer, and picking meals from scratch each week — even meals we'd happily eat again — took more mental effort than it should have for a decision we'd already effectively made a dozen times before.

The problem was never finding recipes. We have plenty we like. The problem was the blank page: deciding, from memory, under time pressure, on a Sunday, what to assign to seven nights — while also making room for leftovers, a night that doesn't need a plan at all, and the fact that some nights are already spoken for before the rest gets figured out.

## What Foundry produced

A 7-day rotation board generated from a saved meal catalog. **Roll the Week** fills the board from meals already in the catalog. From there:

- **Lock** a night to protect it from a reroll, and **reroll** anything still unlocked.
- Link two-night meals explicitly, so a Monday dinner and its Wednesday leftover stay paired instead of drifting apart when the board changes.
- Every full reroll is kept in a session history, so this week's board can be compared against the last few rolls before it's accepted — not just accepted on faith the first time it looks reasonable.
- A flex night sits in the board as its own slot, not a leftover gap.

It's pure Python standard library — no external dependencies, no API calls, nothing that can go down mid-Sunday. It runs locally with a full unit test suite covering the selection logic and the board actions.

## The operators

Built for the family — both adults taken into account in the design, but initially run by one. The real test is whether it becomes the thing we both reach for on Sundays, not just a tool one person maintains on behalf of the household. It's already been used for a real week of real meals, not a demo week.

## Product decisions worth naming

- **The meal catalog is hand-authored, not imported or AI-generated.** We know what we actually eat. A generated or scraped list would need to be curated down to that same set anyway, so skipping straight to a hand-authored YAML catalog was the shorter, more honest path.
- **Leftover linking is explicit, not inferred.** The tool doesn't guess that a meal produces leftovers or that a given night is a good leftover night. You declare the pairing — which night cooks, which night eats — because getting that wrong (serving something as fresh that's actually a leftover, or vice versa) is a worse failure than doing the linking by hand once.
- **No nutritional tracking, no grocery list generation, no recipe links.** All three were deliberately left out. The problem being solved was planning friction — the blank-page Sunday moment — not nutrition, not shopping, not recipe management. Adding any of them would have made the tool bigger without making the actual friction any smaller.
- **Flex night is a first-class concept.** An empty night invites the same "what are we doing" conversation the whole tool exists to avoid. Flex night is planned as a night, it just isn't planned as a meal.

## Current state

This tool spent two weeks in Foundry — iterated, pressure-tested, shaped — before going live. It's now replaced the manual notepad that was doing this job before. One week of real use as the primary planning surface for me. Still early, but it's the thing I reach for now.

## The next bounded step

Keep using it, unmodified, for a few more Sundays. The real test isn't whether the build works — it does. It's whether it actually removes the Sunday friction over repeated use, once the novelty of a new tool wears off and it's just the thing we reach for. That answer comes from weeks of use, not from the build itself.

## What this demonstrates

This wasn't "we need a meal-planning app." It was noticing that the actual bottleneck was a recurring decision, not a lack of options, and scoping the tool to remove exactly that friction — nothing upstream (recipes, nutrition) and nothing downstream (the grocery list) got pulled in just because it was adjacent. The same discipline applies at a much bigger scale: name the real problem precisely enough that you know what to leave out, then build only that.
