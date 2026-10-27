# Feature Branch + PR Flow (your baseline, refined)

Best for: solo or small-team projects, learning GitHub, any project where you want a safety net between "I wrote this" and "this is in main."

This is your original idea, kept intact: draft the baseline, build one feature per branch, open a pull request, merge, repeat until done. The refinements below are the parts professional teams add on top so the same shape scales without turning into a mess of stale branches and giant PRs.

## Phase 0 — Draft the baseline overview

1. Before writing any code, create one GitHub Issue per feature you can already name from your overview (not every detail — just the components you know you'll need). Label each with a short tag like `feature`.
2. Open the repository's **Issues → Milestones** and create a milestone named after the end goal (e.g. "v1 — working prototype"). Assign every issue you just created to this milestone. The milestone view now *is* your baseline overview, kept inside GitHub instead of a separate document, and it shows a live percentage-complete bar as you finish features.
3. Order the issues roughly by dependency (what must exist before the next feature can be built) by dragging them in the milestone view or numbering them in their titles.

## Phase 1 — Start a feature

1. On GitHub, open the issue for the feature you're about to build and use the "Create a branch" link in the issue's sidebar — this names the branch after the issue and links the two automatically, so the issue closes itself later when the PR merges.
2. If you'd rather name it yourself, use the pattern `feature/<issue-number>-<short-description>` (e.g. `feature/12-login-form`) instead of just `feature_01` — the number ties it back to the issue, and the description tells teammates (or future you) what it is without opening it.
3. Locally, in your IDE's Source Control panel, pull the latest main branch first, then create the new branch from main using that same name. Never branch off another feature branch — always off main — so your feature only ever contains your own changes.

## Phase 2 — Build and commit

1. Work in small commits, each one a single logical step ("add login form markup", "wire up validation") rather than one giant commit at the end. Small commits make the PR review and any later revert much easier.
2. Push the branch to GitHub early, even before the feature is finished. On GitHub, open a **draft pull request** right away (the "Create pull request" button has a dropdown — choose "Create draft pull request"). This gives you a visible, running diff of your work-in-progress without signaling it's ready for review.
3. Keep the feature scoped to what the issue describes. If you discover another improvement while working, note it as a new issue instead of adding it to the current branch — this keeps each PR reviewable in one sitting.

## Phase 3 — Open the pull request for real

1. Once the feature is complete and working locally, go to the draft PR on GitHub and click "Ready for review" (or open a new PR if you skipped the draft step).
2. Fill in the PR template with what changed and how you tested it. In the PR description, add the words "Closes #12" (using the actual issue number) — GitHub will automatically close that issue and remove it from the milestone's open count when this PR merges.
3. If any automated checks are configured, wait for them to turn green before requesting review or merging.

## Phase 4 — Review and merge

1. If you're working solo, review your own diff on the GitHub PR page (the web UI's side-by-side view catches things the IDE doesn't) before merging — treat this as a deliberate step, not a formality.
2. If working with others, request review through the PR's sidebar and wait for an approval; address comments as new commits on the same branch rather than rewriting history, so the reviewer can see exactly what changed since their last look.
3. Use **"Squash and merge"** (selectable from the dropdown next to the merge button) rather than a plain merge — this collapses all your small work-in-progress commits into one clean commit on main, named after the PR title. Main's history stays readable as "one entry per feature."
4. Confirm the branch was deleted automatically (it will be, if you turned on auto-delete in the common setup). If not, delete it manually from the PR page's "Delete branch" button.

## Phase 5 — Sync and repeat

1. Locally, switch back to main in your IDE and pull the latest changes (which now include your merged feature).
2. Check the milestone view on GitHub — your issue is closed and the progress bar has moved.
3. Pick the next issue from the milestone and repeat from Phase 1, always branching fresh off the just-updated main.

## When to deviate from this flow

If you ever have two features that must be built on top of each other before either is "done," that's a sign the baseline overview split them too finely — go back to Phase 0 and merge them into one issue/branch instead of chaining feature branches off each other.
