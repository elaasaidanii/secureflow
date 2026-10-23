# Lessons learned

## Scenario 1: secret removed in a later commit

- **What I did:** committed a fake AWS key, then deleted the file in the next commit.
- **What happened:** Gitleaks failed the pull request because it scans the full history.
- **Why:** deleting a secret does not remove it from Git history.
- **What a real leak requires:** rotate the key first, then clean up.
- **Evidence:** see `docs/evidence/`.

## Scenario 2: merge blocked by a required status check
- **What I did:** opened a PR with a fake AWS key, with "Require status checks to pass" enabled on the Gitleaks check.
- **What happened:** the check failed, the merge button was disabled and the merge was blocked.
- **Evidence:** `docs/evidence/03-merge-blocked.png`.

## Mistakes and what they taught me
- **Ruleset with no target:** it existed in the list but protected nothing until I added the default branch. A control is only real once I have seen it block.
- **Test commit on `main` (demo-app):** it went through before the ruleset had a target. Fixed with `git revert` through a PR, without rewriting history.
- **Red PR merged:** the ruleset required a PR but not passing checks, so a failing scan did not stop the merge. The fake key stayed in history and needed a justified `.gitleaksignore` entry.
- **Commit made on `main` instead of a branch:** `git push` said "Everything up-to-date" because the commit was not on the branch I named. Fixed by moving it to a new branch and resetting local `main`.
- **Real credential identifier in a demo:** I typed a temporary lab access key ID instead of a dummy. Only the ID was committed (no secret, no token), the lab session was ended, and I redid the demo with a dummy key. Deleting a branch does not remove a commit; only revoking neutralizes a secret.
