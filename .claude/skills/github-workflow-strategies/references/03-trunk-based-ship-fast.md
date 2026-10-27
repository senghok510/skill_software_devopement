# Trunk-Based Development ("ship fast")

Best for: teams (or disciplined solo developers) who want to ship multiple times a day and are willing to use feature flags instead of long-lived branches to hide unfinished work. This is the strategy used inside most large, fast-moving tech companies — it trades branch-level isolation for flag-level isolation, so things reach main almost immediately.

The leading idea: **the trunk (main) stays green and shippable at every single commit, and nothing waits.** Instead of a branch hiding half-built work until it's done, a feature flag hides it, while the code itself merges to main right away.

## Phase 1 — Set up the ability to hide unfinished work

1. Before starting feature work this way, you need some mechanism to turn a piece of functionality on or off without a code deploy — a feature-flag service, a config file read at startup, or even a simple settings toggle stored in your database. Set this up once, as its own small piece of infrastructure, before relying on this strategy.
2. Decide on a flag-naming convention (e.g. `ff_<feature-name>`) and a place flags are tracked (a markdown table, a flags dashboard, or a project-management tool) so a flag that's been live for months doesn't get forgotten.

## Phase 2 — Branch for hours, not days

1. Create a branch off main for each small piece of work, same as any other strategy — but size the work so the branch lives for a few hours, at most one day. If you can't finish something in that window, that's a sign to split it into a smaller first step (e.g. "add the flag and the empty code path" as commit one, "implement the behavior behind the flag" as commit two).
2. If the feature isn't finished yet, make sure the new code path is wrapped behind the feature flag you set up in Phase 1, defaulted to off, before merging — this is what allows unfinished work to safely reach main.

## Phase 3 — Merge aggressively

1. Open the pull request on GitHub as soon as the small piece of work is ready — don't wait to batch several changes into one PR. Smaller, more frequent PRs are the whole point.
2. Require CI checks (tests, linting, build) to be green before merge, and treat a red main as a "stop everything" event: if a merge breaks main, the very next action — before starting anything else — is either a fix or an immediate revert of that merge, not a fix "later today."
3. Merge as soon as one quick review or an automated check passes. Review turnaround should be measured in minutes to a couple of hours, not days — long review queues are what cause people to batch bigger, riskier PRs, which defeats the strategy.

## Phase 4 — Turn the feature on

1. Once a feature is fully built across however many small merges it took, turn its flag on — in whatever flag system you're using, this is a config change, not a code deploy, and can be rolled back the same way if something's wrong.
2. Turn the flag on for a small percentage of users or just internally first if your flag system supports it, then widen it once it's confirmed stable. This is the "safety net" this strategy relies on instead of a long-lived branch.
3. Once the flag has been fully on for a while and you're confident it's staying, delete the flag and the old code path behind it in a small follow-up PR — flags left in the code forever quietly become technical debt.

## What you give up versus a feature-branch flow

You give up the ability to look at a single branch and see "this is the whole feature, isolated." In exchange you get a main branch that never falls far behind what anyone is working on, which is what makes shipping multiple times a day realistic. Don't adopt this strategy without the feature-flag mechanism in Phase 1 — without it, "merge unfinished work to main constantly" just means a constantly broken main.
