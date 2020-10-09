Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

https://git-scm.com/

## There are three trees and `git reset` and HEAD

1. The work-tree - what's checkedout in file system
2. The stage-tree - what's in the temporary holding area before commit
3. The repo-tree - what's already in the repository

The HEAD is a pointer to latest commit in the repo-tree.

The `git reset` command will work with these 3 trees, and move the HEAD pointer as well.

* `git reset` will reset stage-tree only. Your work-tree will be untouched. So you keep your local changes. (Same as `git reset --mixed`).
* `git reset --hard` will read repo-tree and reset both work-tree and stage-tree. So `git status` will be clean again. All local changes will be tossed!
* `git reset --soft` will reset HEAD to another commit. It will not touch any of the trees.

## How to Setup Quick Dump Git Server

The quickest way to export an repository over the http web is to use a Dump Git Server.

1. Run this command first on the git repository

    cd /path/to/myrepo
    git update-server-info

2. Server the files:
    
    python3 -m http.server --bind 0.0.0.0 --directory $(pwd) 8001

3. Now you may clone it with:
    
    git clone http://localhost:8001/.git myrepo

IMPORTANT: You must keep running `git update-server-info` to refresh the repository for any updates!

## Range Commit works differently for `git log` and `git diff`

These two are very confusing, but to summarize the frequent usage:

```
git log master..branch1 # Show list of commit that are in branch1 but not in master yet

git diff master...branch1 # Show a diff output that are in branch1 but not in master yet.
```

NOTICE that `git diff` uses triple dots!

Note also that `git diff master..branch1` is same as `git diff master branch1`, which only shows diff output between two branch HEAD's. This is NOT the same as diff output for entire content between two branches.
