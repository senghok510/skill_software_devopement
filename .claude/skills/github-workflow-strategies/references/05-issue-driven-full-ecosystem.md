# Issue-Driven + Project Board (full ecosystem)

Best for: projects with many moving pieces — several contributors, several components, or work that needs to stay visible to people who aren't reading code (stakeholders, other teams, future you). This isn't a different branching model from the others — layer it on top of whichever one you picked (feature-branch, GitHub Flow, or trunk-based). What it adds is the tracking and interconnection layer: issues, a board, milestones, and automatic linking, so the state of the whole project is always visible from one screen instead of scattered across branches.

## Phase 1 — Turn the baseline overview into tracked issues

1. For every component in your baseline overview, create one GitHub Issue. Write the issue body as a short description of what "done" looks like for that piece — this becomes the acceptance criteria you check against before merging its PR.
2. Label each issue by type (`feature`, `bug`, `chore`, `docs`) and, if the project has distinct areas, by area (`backend`, `frontend`, `infra`). Create these labels once under **Issues → Labels** on GitHub.
3. Group issues into milestones by phase of the project (e.g. "Phase 1 — core data model", "Phase 2 — user-facing flows"), the same way as the baseline-overview setup in the feature-branch reference, but now spanning the whole roadmap rather than one release.

## Phase 2 — Set up the project board

1. On GitHub, go to the **Projects** tab (organization- or repo-level) and create a new project using the board template. Add columns: Backlog, Ready, In Progress, In Review, Done.
2. Add every issue from Phase 1 to the board (bulk-add from the project's "+" menu by filtering on the repo). New issues created later can be auto-added by configuring the project's workflow rules (project Settings → Workflows → "Item added to project").
3. Configure automation so an issue moves to "In Progress" automatically when a branch or draft PR is linked to it, and to "Done" automatically when its linked PR merges (same Workflows settings panel). This removes the need to manually drag cards for the most common transitions.

## Phase 3 — Work an issue with full linking

1. Assign yourself (or a contributor) to the issue on GitHub before starting — this is what makes the board and any "who's working on what" view accurate.
2. Create the branch from the issue's "Create a branch" link in its sidebar, exactly as in the feature-branch flow — this is what links branch, PR, and issue together automatically.
3. Build according to whichever branching strategy you chose (feature-branch, GitHub Flow, or trunk-based) — this layer doesn't change how you branch or merge, only how the work is tracked.
4. In the PR description, include "Closes #<issue-number>" — this is the link that closes the issue and moves the board card to Done the moment the PR merges, with no manual step.

## Phase 4 — Keep cross-tool visibility current

1. If other tools are in play (Slack, Linear, a design tool), install the GitHub app for that tool once, at the organization or repo level, rather than relying on manual updates — e.g. the GitHub Slack app posts PR-opened and PR-merged events to a channel automatically once connected, so status is visible without anyone typing an update.
2. If multiple repositories make up the project, create one top-level Project board scoped to the organization (not a single repo) and add issues from every relevant repo to it — this is what keeps "interconnection between platforms/tools" visible in one place instead of one board per repo.
3. At the end of each phase/milestone, use GitHub's "Generate release notes" button (on the Releases → Draft a new release screen) to auto-produce a changelog from merged PR titles — this gives you a running, low-effort record of what shipped in each phase without writing it by hand.

## When this layer is overkill

If you're the only contributor and the project is small enough to hold in your head, the board and automation rules are overhead without payoff — stick to issues and milestones (Phase 1) and skip Phases 2 and 4 until a second contributor, a second repo, or a stakeholder who needs visibility shows up.
