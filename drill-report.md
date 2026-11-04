# Release-hygiene drill report

Dry run of the release-hygiene checklist on throwaway material. Run date: 2026-11-04.

## 1. Identity check

- **Login run under:** `HeziLiu` (Hezi Liu — https://github.com/HeziLiu, id 28861483; Beijing/Guiyang, BUPT/GZU).
- **Team check:** the account is a member of one organization (`mcpmark-eval-liuhezi`), but that org has **no teams** — so there are no team memberships and no team member rosters to report. That is the real answer, not an omission.

## 2. Scratch space

- **Repository full name:** `mcpmark-eval-liuhezi/release-hygiene-drill` (public, README-initialized).
  - *Deviation to note:* creating a repo directly under the personal account was rejected by the token (`POST /user/repos` → 403 "Resource not accessible by personal access token"). The repo was therefore created in `mcpmark-eval-liuhezi`, the org that this account owns/has admin rights in, as the closest harmless scratch space.
- **Issues created:**
  - #1 "Release hygiene checklist" (tracking issue)
  - #2 "Check: reviewer coverage"
  - #3 "Check: leaked secrets"
  - #2 and #3 were both attached under #1 as sub-issues (verified via sub-issue list).

## 3. Branch + pull request

- Branch `drill/audit-notes` cut from `main`; `AUDIT.md` committed on it with a short version of the hygiene checklist.
- **Pull request:** #4 "Add audit notes" (`drill/audit-notes` → `main`).

## 4. Simulated main moving ahead + branch update

- One-line edit landed on `README.md` on `main` (commit `15ab68a`, "Add one-line note to README on main (simulate main moving ahead)"), putting main one commit ahead of the PR branch.
- **Branch update outcome: succeeded.** `Update branch` was accepted ("in progress"), and verification shows the branch head is now a merge commit `032f34c` — "Merge branch 'main' into drill/audit-notes" — with the PR showing 2 commits. The PR branch is up to date with `main`.

## 5. The checks (real results)

- **Pull request reviews (PR #4):** `[]` — **no reviews yet**. Zero reviews, zero review comments; the PR is unreviewed.
- **Secret scanning alerts (repository):** **could not be read.** The API call `GET /repos/mcpmark-eval-liuhezi/release-hygiene-drill/secret-scanning/alerts` returned **403 "Resource not accessible by personal access token"** (same result on both `open` and `resolved` filters). The token in use does not carry the secret-scanning read permission, so no alert data could be retrieved. This is reported as-is rather than assumed to be "no alerts" — for a real release the check must be run from a credential with that permission (or in the repo's Security tab).

## 6. Sub-issue cleanup

- **Detached:** "Check: leaked secrets" (#3) was removed from tracking issue #1, per the drill (now tracked elsewhere).
- **Still attached:** "Check: reviewer coverage" (#2) — confirmed via the sub-issue list, which now contains only #2.

## 7. Publication note

The report was intended to be published as a **gist** named `drill-report.md`. Gist creation was blocked by the token in use (`POST /api.github.com/gists` → 403 "Resource not accessible by personal access token"; the account has no existing gists to update either). As the closest substitute, the report is published as this file on the dedicated `drill-report` branch of the drill repo, which leaves `main` and the open PR untouched. If the gist is required verbatim, it needs a token with gist scope.

## Summary for skim

| Item | Result |
| --- | --- |
| Login | HeziLiu |
| Teams | Org `mcpmark-eval-liuhezi` has no teams — no team membership/roster to report |
| Repository | mcpmark-eval-liuhezi/release-hygiene-drill |
| Pull request | #4 "Add audit notes" |
| Branch update | Succeeded — head is merge commit `032f34c` ("Merge branch 'main' into drill/audit-notes") |
| PR reviews | No reviews yet (empty list) |
| Secret scanning | Unreadable with current token — 403 "Resource not accessible by personal access token" |
| Sub-issue detached | #3 "Check: leaked secrets" |
| Sub-issue still attached | #2 "Check: reviewer coverage" |

Drill material only; everything lives in a throwaway repo.
