## Introduction
There are many resources out on internet now a day for using Git. One I like to use is just the official site: https://git-scm.com/ It has command references, book and even short videos. I will highlight some frequent used commands and workflow related to our AuthoringUI here.

## What is Git
Git is a Source Control system (or more specifically a distributed version control system) that helps you manage content changes in files.

Git is called "distributed" because it does not need a central server in order for the client to work. Git client is the server, and they are all in one. It can work offline, and it works with the entire and complete histories of all versions (or commits) of changeset. Hence it can create commit locally without talking to a remote server host. Each commit is an atomic changeset of one or more file's content changes. It will have a unique SHA-1 hash id (or commit id) and a description associated with the changeset. Note that these commits are sorted and linked by their entries order with parent and child relationship. There is no revision sequence number associate with each commit. Git commits are usually stored and can be referenced using a branch name. Most of the Git commands works with one branch at a time. A collection of these commits history are called a repository. However to help a team collaboration, a host server can be used to as a "shared" repository. Team members may pull or push commits on a branch from/to the remote "shared" Git repository in a host server. 

## What are Git branches

Git branches are like a smart pointers that reference Git commits in a repository. As you make new commits into Git, it move the branch name to the latest commit, called HEAD, you have just made. All of Git commits should be reachable by a branch name, traversing from HEAD to its initial commit. A branch needs to be checkout before one can add new commits to associate it as part of the repository. When a new git repository is created, there will be a default branch named "master" ready for you to add new commits. Developers can create they own branch (based on an existing branch, usually called target branch), add new commits, and then later merge these commits back into the target branch.

What are Git commits
A Git repository is a set of one or more commits. One way to think how Git work is to imagine the repository is a small standalone database with a single table named "commits". The "commits" table would have roughly the following fields. I will give some sample data (commit histories), so you will see how that works.

| Branch Name           | CommitID  | Parent    | Author        | Message       | Changeset                                |
|-----------------------|-----------|-----------|---------------|---------------|------------------------------------------|
| master	            | abc001	| -	        | Zemian Deng	| Init project	| file1: readme                            |
| master, featureXYZ	| cde321	| abc001	| Zemian Deng	| Add hello	    | file2: hello.js, file2: package.json     |
| featureXYZ	     	| efg567    | cde321	| Zemian Deng	| Change print	| file2: hello.js + console.log("Hello");  |


As you can see, branch is nothing but just a pointer name that associate along with commits. You are free to create any number of branches, and add any number of commits records. After branching off a target to add new changes, Git let you merge the branch back to target in a very efficiently way. You might still see conflict alone the way, but they should be easy to fix. When you clone a Git repository, you make a copy of this entire database down into your local PC (no worry, it does it very fast). When you checkout a branch, you basically getting all the commits that belong to a branch (think like a SQL query with select * where branchName = 'master' for example), and Git will construct a local files contents based on commits you have. And when you make new commits, it will be almost like inserting records into the commits table.

## What are Git worktree's
Git repository data are stored in a .git directory. The folder that contains this is called project root directory, and almost all the Git commands are operated in this directory. You will find that each commits will store as a blob in a file inside the .git directory. Git manages all the branches, along with many metadata as well. Since Git has all the commit  histories, you can go back to any commits in a branch at any time. When you run git clone, it creates the "repository" tree (.git folder). When you run git checkout on a branch, it actually move data from "repository" tree into a staging area call the "index" tree, and then from this staging area, it will make local files as "work" tree directory into your project root directory.

So Git always manage things in these three areas: repository tree, stage/index tree, and work tree. When you run git add, it adds the changeset into the "index" tree. And when you run git commit, it will add changeset from "index" into the "repository" tree. When you run git fetch, it will transfer commits from remote "repository" tree into local "repository" tree, but will not touch "index" nor "work" tree. Only when you perform git merge or checkout it will bring data out into "index" tree and then "work" tree. Remember that git pull is just shorthand for git fetch and then git merge. Conversely when you run git push, it sync local "repository" tree to remote "repository" tree!

## How Project Files are Organized in Git
Git only track changesets content from one or more files. It does not track directory it self. So in order to add something to Git, you need at least a file. However, when a file is modified, the changeset also records the file path. So when you checkout a latest commit, it knows where the file is suppose to be, hence it can re-create the "work" tree for you. You can create any files in any nested directories according to your project need. If your project is large, you can create sub modules as directory with files, but to Git, it still the same, just one repository of many commits.

Typically, a development team would use few branches as the "long live" branches that they want to keep protected (etc no one should delete them.) For example:

* "master" - the latest bleeding edge of codebase. 
* "feature-xyz" - the next major feature in development that based from master branch.  
* "release-1.x-maint" - a branch for bug fix in maintenance mode

Team can setup "workflow" or process in such that each team member would create their own "short live" work branch based from one of "long live" branch. Make changes, and then merge back into the "long live" branch.


## What are the Git remote branches and repository


When we clone a Git repository from a remote host server into our local PC, the Git repository we get will have the entire dataset(commit histories). However, we will now have a "local" copy, and yet, they are from remote location. To help keep them in sync, we try to refer what's the original state of the repository (when we got it from server) as "remote". Hence, on the local Git repository, we have what's called "remote branches". These branches exists in the "repository" tree, but not visible to your "locally", until you perform a git checkout.

When you create a new local branch in Git, it will not exists in remote site until you have pushed your branch into the remote repository. After this Git will recognize they both exists and will try to track them together for you (telling you how many commits you are ahead or behind etc.)

Developers are free to create any number of local branches in their local repository to explore their code, make changes, even commit it. But they are only within the local branches without have to share to others (to remote repository) until they are ready.

## What are Git tags
Git tag is just a fixed, immutable pointer name to a commit. Like a branch, but they do not auto move and track latest commit. It's used to tag a release or to give a commit a important name so we can checkout the files without having to remember the commit id.
## Git Installation
Mac: 

	The git command should already be installed as part of the XCode package.

Windows:

	Download the Git For Windows installation package. It should come with a Bash shell running MINGW env.

You can verify Git installation by running it:

	git --version
