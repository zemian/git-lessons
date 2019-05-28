## Explore Git Source Control

[Git Tutorial](https://confluence.oraclecorp.com/confluence/display/KM/Git+Tutorial)

## How to Read Merge Commit

The first commitid is the target branch, and second is the original branch.

Example:

```
commit 8fcf79d43ac63a4faaa524110400a06e75735586 (HEAD -> master)
Merge: 2883e86 9d83a86
Author: Zemian Deng <zemian.deng@oracle.com>
Date:   Tue May 28 10:17:18 2019 -0400

8fcf79d (HEAD -> master) Merge remote-tracking branch 'origin/cmak-content-view'
9d83a86 (origin/cmak-content-view) Fix session
4d555f4 Move integration token and end user token to shared session object to reduce authorize calls
2883e86 (origin/master, origin/HEAD) Merge-Request: 139 from 'zemian-work' into 'master'
d3fc3d4 (zemian-work) Update readme
```
