---
name: github-workflow-strategies
description: Use when planning or setting up how a project will move through GitHub — choosing a branching strategy, structuring feature branches and pull requests, deciding between GitHub Flow, trunk-based development, Git Flow, or an issue/project-board-driven workflow, or when asked how professional teams ship fast on GitHub.
---

# GitHub Workflow Strategies

Five ways to take a project from an empty repo to a shipped, incrementally-built product on GitHub. Each strategy is a tradeoff between **safety** (how hard it is to break the main branch) and **speed** (how fast a change reaches main). Pick one per project — switching strategies mid-project is a common source of confusion, so decide early and name the choice in the repo's README.

## Decision guide

| Your situation | Strategy | Reference |
|---|---|---|
| Solo or small project, want a safety net while learning GitHub | **Feature Branch + PR** (your baseline, refined) | `references/01-feature-branch-pr-flow.md` |
| Web app/service deployed continuously, no versioned releases | **GitHub Flow** | `references/02-github-flow.md` |
| Team shipping multiple times a day, comfortable hiding unfinished work behind flags | **Trunk-Based Development** | `references/03-trunk-based-ship-fast.md` |
| Library or product with versioned releases (v1.2, v2.0) supported in parallel | **Git Flow** | `references/04-git-flow-release-based.md` |
| Project spans many contributors, tools, or components that all need to stay visibly in sync | **Issue-Driven + Project Board** | `references/05-issue-driven-full-ecosystem.md` |

Read the matching reference file for the full step-by-step. The sections below apply regardless of which one you pick.

## Why your baseline idea already works

Your instinct — write a baseline overview, cut one feature branch at a time, open a pull request, merge, repeat — is the same backbone every strategy below shares. What the alternatives change is: how long a branch is allowed to live, how a release is marked, and how work is tracked across people and tools. `references/01-feature-branch-pr-flow.md` keeps your approach and adds the professional refinements (naming, small PRs, keeping main always releasable, cleaning up branches) without changing its shape.

## Common setup — do this once, before any strategy

1. On GitHub, open the repository's **Settings → Branches**. Add a branch protection rule for the main branch requiring: a pull request before merging, at least one approving review, and all status checks (once you have CI) to pass before merge. This makes "accidentally pushed straight to main" impossible rather than just discouraged.
2. In **Settings → General**, confirm the default branch is the one named `main`.
3. Still in **Settings → General**, turn on "Automatically delete head branches" so merged feature branches are removed from GitHub without a manual step.
4. Create a pull request template: on GitHub, add a file via the web UI at the path `.github/PULL_REQUEST_TEMPLATE.md` with a short checklist (what changed, how you tested it, any follow-up needed). Every new PR will start from this template.
5. On GitHub, open the **Issues** tab and enable it if it isn't already (Settings → General → Features). Even for a solo project, one issue per feature gives you a running log of what the "baseline overview" actually contained.
6. Locally, clone the repository once with your IDE's built-in Git/GitHub integration (in VS Code: Source Control panel → "Clone Repository"; in JetBrains IDEs: Git → Clone). From here on, all branch creation, committing, and pushing happens through that same panel or through your terminal — pick one and stay consistent so you always know where you are.
7. In your IDE, enable the setting that shows the current branch name in the status bar at all times. Every strategy below depends on you always knowing which branch you're on before you start editing.
