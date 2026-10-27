# GitHub Flow

Best for: web apps or services that deploy continuously (no versioned releases to support in parallel). This is GitHub's own official lightweight flow — the simplest strategy that still keeps main safe.

The one rule that defines this strategy: **main is always deployable.** Every commit that lands on main should be something you'd be comfortable pushing to production immediately, because in this flow, you usually do.

## Phase 1 — Anything you do starts a branch

1. There is no "develop" branch and no distinction between a feature, a fix, or an experiment — all of them start the same way: branch off main, on GitHub or locally, with a descriptive name (e.g. `add-password-reset`, `fix-timeout-bug`).
2. Keep the branch short-lived: the goal is hours to a few days, not weeks. If a branch is still open after a week, that's a signal to split it into smaller pieces.

## Phase 2 — Open the pull request immediately, not at the end

1. Push the branch and open the pull request on GitHub as soon as you make the first commit — before the work is finished. This is the main difference from the feature-branch flow: the PR is a running conversation and visible diff from minute one, not a final step.
2. Use the PR description to say what you're doing and why, and update it as the work evolves. Teammates can comment on specific lines at any point, not just at the end.
3. If your project has a staging environment or preview deployments (GitHub can trigger these via Actions), check the PR's "Checks" tab for a preview link and verify the change there before asking for review.

## Phase 3 — Discuss and commit more

1. Push additional commits to the same branch as you address feedback or keep building. The PR page updates automatically — there's no need to open a new one.
2. Once someone else (or you, reviewing your own diff deliberately) is satisfied, request/give approval using the PR's "Review changes → Approve" action on GitHub.

## Phase 4 — Merge and deploy right away

1. Merge the PR as soon as it's approved and checks are green — don't let approved PRs sit. Use "Squash and merge" to keep main's history as one entry per change.
2. Because main is always deployable, merging is effectively the trigger to deploy. If deployment is automated (via GitHub Actions), it kicks off immediately after merge. If manual, do it the same day — the whole point of this flow is that there's never a backlog of "finished but not yet shipped" work sitting on main.
3. Delete the branch (automatic, if you enabled it in the common setup).

## Phase 5 — If something breaks in production

1. Open a new branch off main immediately, fix the issue, and push it through the exact same PR flow as any other change — there's no separate "hotfix" branch type in GitHub Flow, because every branch is already fast enough to serve as one.
2. If the fix is urgent enough that waiting for review isn't acceptable, merge after a fast self-review and loop a teammate in on the PR afterward for a retroactive look — don't skip the PR itself, only the wait.

## How this differs from the feature-branch flow

The feature-branch flow treats "merged" and "released" as two separate moments (you might batch several merged features before cutting a release). GitHub Flow treats them as the same moment. Pick GitHub Flow once you have any form of continuous deployment in place; stay on the feature-branch flow until you do.
