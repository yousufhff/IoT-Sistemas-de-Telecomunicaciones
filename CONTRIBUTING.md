# How we work

## Principles
- `main` always works and is only changed through a **pull request (PR)**.
- Every change is made on a short-lived branch, by the person who does the work, **under their own Git identity**, so the commit history reflects real contributions (required by the course guidelines).
- Every PR is reviewed by someone who did **not** write it. Reviewing is how we all learn every part of the system (the oral exam asks any member about any part).

## Git identity (each member, once)
```bash
git config --global user.name "Your Name"
git config --global user.email "the-email-used-in-github@example.com"
```

## Daily flow
```bash
git switch main
git pull
git switch -c feat/edge-detector        # one branch per task
# ... work ...
git add <files>
git commit -m "feat(edge): add consecutive-event rule"
git push -u origin feat/edge-detector
```
Then open a PR on GitHub, fill the template, ask for a review, merge with **Squash and merge** and delete the branch.

## Branch names
`feat/<topic>`, `fix/<topic>`, `docs/<topic>`, `exp/<topic>` (experiments), `chore/<topic>`.

## Commit messages
`<type>(<scope>): <summary in imperative>`
Types: `feat`, `fix`, `docs`, `exp`, `test`, `chore`, `refactor`. Scopes: `datasource`, `comm`, `edge`, `edge-ai`, `cloud`, `cloud-ai`, `infra`, `data`.

## Pairs
Pair A: Joan + Lola. Pair B: Abel + Yousuf. Each work package is split in two halves, one per pair. Inside a pair, one writes and the other reviews. Between pairs, we swap halves in the weekly explain session.

## Rules for data
- `data/raw/` is never edited. Cleaning produces files in `data/processed/` from a script.
- Do not commit files above 50 MB (use a download script and document the source in `data/README.md`).
- Check the licence before adding a dataset.

## Definition of done (for a task)
1. It runs from a clean clone following the README.
2. It has a test or a documented manual check.
3. Docs updated (`docs/`) if a decision or interface changed.
4. The PR was reviewed by someone else.

## Decisions
A decision that affects more than one person (protocol, message format, thresholds, tools) is written as an ADR in `docs/decisions/` **before** it is implemented.
