# Lessons learned

## Scenario 1: secret removed in a later commit

- **What I did:** committed a fake AWS key, then deleted the file in the next commit.
- **What happened:** Gitleaks failed the pull request because it scans the full history.
- **Why:** deleting a secret does not remove it from Git history.
- **What a real leak requires:** rotate the key first, then clean up.
- **Evidence:** see `docs/evidence/`.
