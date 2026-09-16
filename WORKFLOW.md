# Git Workflow

## What bisect found
The bad commit was `c99fb4209e6fb6e5ed2789893fdb2f893d61d6c6`. It changed the `BULK20` check from `items.length >= 5` to `items.length > 5`, which meant an order with exactly five items no longer got the discount.

## Branching choice
For a team of four, I would use GitHub Flow. Each person can work on a short-lived branch, then open a pull request for review and CI before merging into `main`. Git Flow seems like more process than this small team needs, while committing straight to trunk would make unfinished work harder to manage.

## The old secret
Ignoring `.env` and removing it from tracking keeps it out of future commits, but it is still in the old commits. To really remove it, I would rewrite the repository history with something like `git filter-repo` or BFG, replace the credentials, and force-push the rewritten branches and tags. Everyone with a clone would need to coordinate that change. Not needed (dili ra kailangan sa assignment though)

## Rewriting a commit
Rewording the commit was okay because it was still local and nobody else had pulled it. Once teammates have pulled a commit, changing it gives it a new hash and makes their branches diverge. In that case, I would leave the old commit alone and add a new commit instead of making everyone deal with a force-push.