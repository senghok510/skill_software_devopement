# Git Flow (release-based)

Best for: libraries, desktop apps, or any product that ships numbered versions (v1.2, v2.0) and may need to support more than one version at once (e.g. patching v1.x while v2.x is in development). This strategy is heavier than the others on purpose — it exists to manage parallel release lines, not to move fast.

The structure adds two permanent branches on top of main: a **develop** branch where finished features accumulate between releases, and short-lived **release** and **hotfix** branches for the moment of shipping.

## Phase 1 — One-time setup

1. On GitHub, create a second permanent branch named `develop`, branched off main at its current state. From now on, main only ever receives code at the moment of a release — never directly from a feature.
2. In **Settings → Branches**, add a second branch protection rule for `develop` (same idea as main: PR required, review required, checks required). Both long-lived branches are now protected from direct pushes.
3. Update the repository's default branch for new pull requests (Settings → General, or set it per-PR) so that feature branches target `develop`, not main, by default.

## Phase 2 — Build a feature

1. Branch off `develop`, not main, naming the branch `feature/<description>`.
2. Build and commit as in the feature-branch flow — small commits, push early, open a PR.
3. Open the pull request targeting `develop` (double check the PR's base branch on GitHub before opening it — this is the step people most often get wrong in Git Flow, since GitHub defaults to main). Review, get it green on checks, and squash-merge into `develop`.

## Phase 3 — Cut a release

1. When `develop` has accumulated enough finished features for the next version, branch off `develop` into a new branch named `release/<version>` (e.g. `release/1.2.0`).
2. Use the release branch only for last-mile work: fixing bugs found in final testing, updating version numbers, finalizing release notes. No new features go into a release branch.
3. Once the release branch is verified, open a pull request from it into **main**, review, and merge (a plain merge here, not squash, so the release branch's individual fix commits stay visible in main's history).
4. On GitHub, go to **Releases → Draft a new release**, tag the exact commit you just merged to main with the version number (e.g. `v1.2.0`), and publish it with the release notes. The tag is what makes this version something others can reference and depend on permanently.
5. Merge the same release branch back into `develop` as well (open a second small PR for this), so any last-mile fixes made during the release aren't lost from future development.
6. Delete the release branch once both merges are done.

## Phase 4 — Hotfix a released version

1. If a bug is found in a version that's already released (and `develop` has since moved on to unrelated new work), branch off **main** — specifically off the released tag, not off `develop` — into a branch named `hotfix/<description>`.
2. Fix only the specific bug. Open a pull request into main, review, merge, and tag a new patch version (e.g. `v1.2.1`) the same way as Phase 3, step 4.
3. Merge the hotfix branch into `develop` too, the same way as Phase 3 step 5, so the fix carries forward into future versions instead of only existing in the patched release.

## Why this is heavier than the other strategies

Every other strategy in this collection has one long-lived branch (main). Git Flow has at least two, plus two kinds of temporary branches with different merge targets. Only take this on when you actually need to support more than one released version at a time — if you're shipping continuously with nothing to "patch separately," GitHub Flow or trunk-based development will do the same job with far less branch bookkeeping.
