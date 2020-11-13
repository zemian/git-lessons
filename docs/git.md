## How to find where a workbranch is created from a target

Ref: https://stackoverflow.com/questions/1549146/git-find-the-most-recent-common-ancestor-of-two-branches

Use:

    git merge-base target workbranch

Or use `--fork-point` option

    git checkout workbranch
    git merge-base --fork-point target
    
    git log -1 $(git merge-base --fork-point target) # See detail of the commit 

Or you may view the diff content (three dots)
    
    git diff --stat target...workbranch  # Show changes in workbranch compare to target

Or you may view the commits log (two dots)

    git log --oneline target..workbranch  # Show what's in workbranch but not in target
    git log --oneline workbranch..target  # Show what's in target but not in workbranch
