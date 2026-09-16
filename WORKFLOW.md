# Git Workflow Notes

## Bisect Finding

`c99fb4209e6fb6e5ed2789893fdb2f893d61d6c6` introduced the regression by changing the `BULK20` condition from `items.length >= 5` to `items.length > 5`, so five-item orders stopped receiving the discount.

## Branching Strategy

For a team of four, I would recommend GitHub Flow: keep `main` deployable, use short-lived feature branches, and merge through pull requests with review and CI. It provides enough isolation for parallel work without the release-branch overhead of Git Flow, while staying more structured than committing directly to trunk.

## Removing Secrets From History

Removing `.env` from tracking and ignoring it prevents future commits from containing the file, but the old credentials remain in existing commits. To remove them completely, I would use a history-rewriting tool such as `git filter-repo` or BFG Repo-Cleaner, replace the credentials, and force-push the rewritten branches and tags after coordinating with every clone. This assignment does not require that step because it uses fake credentials and is specifically teaching removal from the current tracked state while preserving the exercise history.

## Rewriting Commit History

Rewording was acceptable because the commits were still local and no teammates had pulled them. Rewriting a commit already pulled by teammates would change its hash and make their clones diverge, requiring a coordinated force-push and recovery work, so a new corrective commit is safer in that situation.