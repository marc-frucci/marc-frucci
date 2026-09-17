# Foundry

Foundry is the framework I run every idea through before I decide whether it's worth building. It's the layer between "I have an idea" and "I'm opening an editor." That's the thing that decides what should get built before anyone decides how.

I built it because I noticed the same failure mode kept happening: an idea would sound reasonable, I'd start building, and three days in I'd realize either the real problem was something else, or the thing I was building was three times bigger than the problem justified. Foundry is the discipline that catches that earlier and cheaper.

The core question Foundry answers:

> **Is this idea sufficiently understood and bounded to build, and if so, what exactly should get built first?**

It optimizes for useful software, not impressive software. Not every idea needs an app, an agent, a database, or an API. A lot of ideas need a smaller intervention than the one first proposed, and some don't need to be built at all.

## Always-on rules

- Problem before implementation.
- Prefer the smallest useful end-to-end workflow.
- Challenge complexity without killing momentum.
- Separate product decisions from implementation decisions.
- Existing conventions in a project outrank invented ones.
- Don't design speculative future extensibility.
- Don't turn every idea into an engineering spec before it's actually understood.
- Real-world learning outranks whatever the original brief said.
- The current working system is evidence; the brief just records intent.
- Stop discovery once the remaining uncertainty is better resolved by building and using the thing than by talking about it more.

## Two ways in

**New idea**: the idea hasn't been shaped yet. Start from discovery and move through the stages below until it's ready to build, deliberately deferred, reduced to a smaller experiment, or rejected because the problem doesn't justify a build.

**Existing build**: something already exists or is in progress. I don't restart discovery from zero. I reconcile the current state of the repo, whatever brief or governing docs already exist, what was actually implemented, and any real usage or operational learning against the new question I'm bringing to it. The working system is treated as reality; the old brief is treated as a snapshot of past intent, not gospel.

## The phases

### 1. Explore

Articulate the idea before trying to solve it. Establish the user, the actual problem, the current workflow or behavior, what triggers the need, the desired outcome, and why the current state isn't good enough.

I'm listening for the underlying workflow or need, not just accepting the first proposed solution at face value. Most ideas arrive already wearing a solution, and that solution is often not the right one.

*Move on once the problem, user, trigger, and intended outcome can be stated plainly, without major ambiguity.*

### 2. Pressure test

Test whether the idea deserves to become software, and whether the shape it's arrived in is unnecessarily complicated. I'm actively looking for reasons this is weak: an unclear user, a low-frequency use case, an existing alternative that already works, complexity that doesn't earn its keep, automation reaching for a problem that's actually rare, AI included for its own sake, a maintenance burden nobody's accounted for, or a feature set padded with things that "might be useful someday."

The questions I actually ask:

- Is software even necessary here?
- Is AI actually necessary, or just available?
- What's the smallest version that would prove the thesis?
- What assumption, if wrong, kills this?
- What could I remove without harming the core outcome?

If an idea is weak, I want to know now. If it's good but over-scoped, I want to know that too. Sometimes a simpler experiment produces the same learning for a fraction of the cost.

*Move on once there's a defensible reason to build, and the major assumptions, risks, and unnecessary complexity have been surfaced.*

### 3. Shape

Turn the surviving idea into a real product boundary: user, problem, trigger, desired outcome, core workflow, inputs, outputs, what state has to persist, external dependencies, constraints, success criteria.

Then explicitly define three lists:

- **V1 Must Do**: required for the first useful end-to-end workflow.
- **V1 May Do**: included only if trivial and if it doesn't expand the boundary.
- **V1 Will Not Do**: explicit exclusions, each with a one-line reason. ("Multi-user sync: excluded, no demonstrated second-user need yet, and it adds auth and state complexity before the core workflow is validated.")

The goal is a single, unambiguous end-to-end workflow that should work before anything else gets added.

*Move on once V1 can be stated clearly, the core workflow is unambiguous, and the exclusions are explicit.*

### 4. Design

Only once the boundary is stable, define the smallest reasonable implementation shape: components, data flow, storage, interfaces, relevant schemas, integrations, failure handling, likely repo structure, testing approach. Include only what's useful; no architecture ceremony for its own sake.

If the build already exists, I inspect its actual conventions first (governing docs, existing structure, established patterns) and extend those rather than imagining a cleaner architecture from scratch. A cleaner design that ignores what's already there isn't actually cleaner.

*Move on once implementation can be broken into bounded steps and no unresolved product decision materially blocks starting.*

## Decision handling

I don't let consequential choices get made silently. For every meaningful unresolved decision, I write down: the decision itself, the realistic options, what actually changes between them, and my recommendation. If a decision can safely wait until implementation or real usage provides better evidence, I say so and move on. Not every decision needs to be forced early.

## Build readiness

An idea is ready to build when:

1. the problem is clear,
2. the user and workflow are clear,
3. there's a defensible reason to build,
4. V1 has a meaningful boundary,
5. the exclusions are recorded,
6. the major product decisions are resolved,
7. implementation can be described in bounded steps,
8. success is testable,
9. the remaining uncertainty is better resolved by building than by more discussion.

## The build brief

Once an idea is ready, it becomes a brief: the contract between the product thinking and the implementation. It covers: the product itself (problem, user, trigger, outcome, workflow), why it should exist, the V1 boundary, the success condition, functional requirements, the technical shape, relevant repo context and conventions, suggested repo changes, an implementation sequence broken into small vertical steps, acceptance tests covering the happy path and the real failure paths, and any decisions still genuinely open.

The brief becomes the actual working reference for the build, usually saved alongside the project itself so it stays close to the thing it describes, not filed away somewhere separate.

## Re-entry after building

When I come back to something mid-build, I don't assume the original brief is still fully correct. I reconcile three things: **intent** (what the brief said should happen), **reality** (what the code and the working system actually do), and **evidence** (what building, testing, or real use has taught me since).

From there I figure out what's still valid, what changed, whether that change is just an implementation detail or an actual product learning, whether the V1 boundary needs to move, and what the next bounded decision is. I don't rewrite the product just because implementation was inconvenient, but I do revise it when the evidence shows an original assumption was wrong. The working system outranks an outdated brief.

## Stop rule

I don't polish this indefinitely. Discovery stops once the mechanism and the next bounded action are clear. If the remaining uncertainty is cheaper to resolve by building, testing, or using the thing than by continuing to talk about it, it's time to hand it to implementation.

The goal was never a perfect spec. It's enough clarity that building the thing generates useful evidence instead of unnecessary rework.
