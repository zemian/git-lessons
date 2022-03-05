## First Time Git Setup

You should setup your name and email in Git so any commit you make will contains your information.

git config --global user.name "John Doe"
git config --global user.email "johndoe@example.com"

## Getting Started
You can quickly create a Git repository with one of your pet project and start exploring. Try the following:

```
cd myproject
git init
echo 'hello' > readme.txt
git add readme.txt
git commit -m 'Add readme'
git log
git branch
```

## Naming Conventions
In this document, we will give many command line examples on how to perform certain action in Git. We tried to use some variable names to represent values that might be different for each developer or situation. These are:

<your_branch> This is your own Git work branch, and you can name it anything you want. Typically will use your name as prefix. Examples: zemian-add-ckeditor or zemian-jira-12345.
<target_branch> This is a Git branch where you want your changes to go back to. Example would be master or v19.9-integration.
<my_file> A file that's added into your Git repository. It might include path relative to where the Git repository directory is located.
<commit_id> A 40 characters hex string (sha-1) that uniquely identify one of you changeset commit in history. Often times, Git can simply use the first 7 characters to uniquely identify the full sha-1 commit id. (Unless your repository have more than million of commits, then you might need more than 7 digits).


## What is GitHub?

The [GitHub](https://github.com/) is an online Git repository management platform. Besides hosting your Git repositories live on internet, it also provides some additional project management tools (WIKI and Jenkins etc) that help a team to development and collaborate together.

NOTE: GitHub is a online hosting service, and they are not the company who created Git.

## How to get source code from a remote host server?

Often time you would need to get an existing Git repository from a remote host server (eg: GitHub) where a team have access to. The project you work on should give you a URL to use. With that you can get it like this:

git clone <git_url_of_repositoryX>

The <git_url_of_repositoryX> can usually be in either https or ssh form. Use "ssh" if you intend to push changes back into the host often. You can setup SSH key to host env to avoid password authentication on each commit.

After cloning an existing Git repository, you may examine the histories by cd into the repository. All commands are relative to project root directory.

	cd repositoryX
	git log

By default, a git repository will have a master branch, and that will be the branch it will automatically checkout for you after you do a clone. You can examine your local file system to verify this. You can also try git log --oneline to have a compact view of histories.

What you see in working directory is the content of the current branch. To see a list of branches in your repository, you can run this command:

	git branch

The one has `*` next to it means the current branch that's checked out. If you list is empty, that mean you have not created any branch yet. The repository might have some remote branches from the host however, and you can list those with

	git branch -r

Branches in your repository can be hidden if they are "remote". You have use checkout command to make it visible as "local" branch and see the working tree.

To verify where your Git repository is cloned from, you can run this:

	git remote -v

## How to create a new branch (local)?
In git you want to create your own branch ( <your_branch> ) before start any changes of work. You first need to know which existing target branch you want to make changes onto, then make a branch from that.

git branch <your_branch> <target_branch>

git checkout <your_branch>

The <your_branch> can be any string you like. You might find it useful to prefix it with your own name so it stands out. Now you're ready to make any changes. All changes or (commits) will be on your branch without affecting other. The last two commands are often used, and it can be combined as

git checkout -b <your_branch> <target_branch>

NOTE: If you omit <target_branch> parameter, it will default to your current active branch (the branch you have checked out).

## How to make changes and do a commit?
After you checkout a branch, you may modify any files in your local workstation. When changes are ready, you can commit it like this:

First, add changes into "index/staging" tree

	git add <my_file>

Then you can commit what's in staging tree into the repository tree (permanent).

	git commit -m 'Fix bug xyz due to regression changes'

You can add and commit as often as you want, and they are kept all local to your repository. No changes will go into remote server until you perform a push command.

NOTE: If you are lazy and sure of changes, you can also run "git add ." that adds EVERYTHING (all changes, including new files!) under project root directory to the "index/stage" tree. Be careful if that's really want though. You can use git status to inspect what will be added first before you run the command.

## How to undo a "git add" command only?
If you add a file into Git staging by mistake and do not want it to be committed, then you can run:

	git reset <my_file>
To undo a "git add .", you can run:

	git reset # Notice it's without dot
The reset command tells Git to "reset" the "index/staging" tree from the "repository" tree.

## How to revert changed files?
WARNING: You about to tell Git to throw away your changes! Please double check if that's really what you want first! If you think you still want the changes and want to get back to a "clean" state, then use stash command instead. (See section below.)

Option1: You can revert local file changes back to versioned stated by using the checkout command. (Yes, I know, the command is confusing, but that's the command Git use to bring files from "index" tree into "working" tree, hence you reseting it original state)

	git checkout <my_modified_file>

Option2: If you 100% sure that you do not want any of the changes you have locally, then you can also run the following:

	git reset --hard

NOTE: Careful, that will remove ALL your pending changes! This above command will reset the "index" tree from "repository" tree, and it reset the "working" tree all together.

## How to make my Git branch clean?
Usually If you have pending changes locally that has not yet commit, then the branch is "unclean". To make your branch clean again, you simply need to commit your local changes, or revert what you do not want. Running git status command should tell you the result.

Sometimes, when you're in middle of making some changes and not ready to commit; and you realize you want uptake some changes from remote server. The safest way to do that is to ensure branch is clean without modification first. Git provide a cool feature where it can move your local changes into a temporary shelf, and later you can restore it.

	git stash -u

The -u option tells Git to stash away all local modified files, and those untracked ones! This ensure you won't lose anything.

To restore the changes, you simply run:

	git stash pop

## How to create a branch from remote host?
If your co-worker pushed his branch into the host, and you never receive it before, then you may get their branch and create/add it as local branch in your repository like this:

	git fetch
	git checkout <remote_branch_name>

Noticed that you do not use -b option on checkout command since the branch exists remotely. Also note that you should NOT include the remote name in your  <remote_branch_name>. Example do not use origin/<remote_branch_name>. 

NOTE: If you do not remember the name of the remote branch, then you can try git branch -r to list them.

How to update your branch from remote host?
NOTE: Before you update, you should ensure your local git status is clean first! This will ensure you do not lose any local changes.

If you have created a <your_branch> from a <target_branch>, sometimes you want to refresh your branch with any new changes from <target_branch>. To do this, you use following:

NOTE: Assume you are on your work branch, and ensure you are in clean state first
git status

	git pull origin <target_branch>
NOT: git pull is same as git fetch and then git merge. If you see conflicts after the merge, you would need to resolve it, and then complete the merge with following:

	git add .
	git commit --no-edit

NOTE: The --no-edit option in above commit will take default message for a merge, which will contains your branch name etc. If you prefer, you can also provide your own merge commit message comment with the -m option.

## How to update your branch to remote host?
To get your changes to host server, you just need to push your local branch into the host. If branch is new and not exists in host yet, then you need to push it this way:

	git push origin <your_branch>

You may push to the same remote branch multiple times with new changes!

NOTE: You can save some typing to use -u option when pushing the first time. Git will then automatically track (remember) your local branch to the remote side and any subsequence push commands you used, you do not need to give the origin <your_branch> parameters.

## How to go back to certain commit version (for read only)?
Often time, you want to jump back to an older version of the project (for debug or review purpose) to read the code only, without performing a permanent commit revert action in history. Then in this case, if you know that commit ID, then simply use the checkout command:

	git checkout <commit_id>

Instead of commit ID, you may also pass in parameter using a tag name or a branch name (or even a remote branch eg: origin/your_branch)

When you are done reviewing the changes, you simply switch back to your branch using another checkout command to your own branch.

NOTE: You do not want to make any commit without sitting on a branch!

## How to go back to certain commit version (permanently)?
If you want to actually revert a commit permanently in git log history and re-commit it, then you can use revert command:

	git revert <previous_commit_id>

Note that your <previous_commit_id> might contains multiple files change! This will revert and commit your previous changes as part of your history.

## What does 'detached HEAD' state mean?
If you see this message, then it means you are not in a "named" branch any longer. Remember that a branch is used to track your latest changes (HEAD of the commit ID). This typical occur if you choose to checkout at some arbitrary commit ID (for code review or verify bug etc), then you no longer track by a branch, and away from the "HEAD" commit ID, hence the message 'detached HEAD'. It does not affect you much as long as you DO NOT make any commit in this state. Because if you do, you will not able to easily retrieve it since you are not making it to a branch. Just simply use a checkout command with a branch name to go back to normal.

## How to delete a branch?
You can delete a local branch that you already have merged with this:

	git branch -d <branch_name>
NOTE: Do not delete long running branch such as master branch.

NOTE: If you want to delete a branch that has not yet merge and you no longer want the changes, you would need to replace with a -D option to force it instead.

If you have pushed a branch into remote host before (eg: to create Merge Request) and you no longer need it on the server (eg: after Merge Request has completed) then you want to remove it from the remote host as well. You can do this with following:

	git push --delete origin <branch_name>
NOTE: Careful not to delete long-live branches such as "master"! You normally would want to cleanup and delete your own work branches only.

## How do I perform a code review using Git?
The developer who make changes should have their own work branch, pushed to Git server and then create a Merge Request against a target branch. Then the developer can request a reviewer to go over the changes. The reviewer then can either accept the merge, or request developer to rework on some feedback. If rework is needed, the developer would simply make more changes on his/her branch, and re-push, then the Merge Request will auto update. And the process can repeat again.

Sometimes the changeset in Merge Request is large, and it will be easier to bring it down to your local PC and use an IDE to review the changes. You can use the following commands as a code reviewer:

	git checkout <target_branch>
	git pull
	git merge --no-ff origin/<developer_branch_for_review>
	# Now review your changes locally. If you have an IDE, 
	# you can perform an diff between latest changes 
	# against <target_branch> to quickly review what 
	# has changed by developer.
The --no-ff option used in merge above will ensure that Git will not to perform fast-forward, but to always create a merge commit instead. It's a good way to ensure we can track who and when performed the merge (it records the code reviewer performed a merge commit).

When you are done reviewing, and if you have permission to make direct change to <target_branch>, you then may push the 	merge result on <target_branch> to server:

	git push origin <target_branch>
If you do not have permission to push to <target_branch>, then you may continue to use Merge Request UI interface to accept and merge in the changes instead. If you do this, then you need to throw away your local changes:

	git reset --hard <target_branch>
I see "Conflict" in my Merge Request, how should I resolve it?
After you created a Merge Request, sometimes you might see "Conflict" due to your target branch is outdated and someone else already modified same file you did. If the conflict is simple, you can even edit and fix it on the Merge Request interface. But if the conflict is large and you prefer do it locally in IDE, then you should resolve the conflict on your OWN work branch (one that you submitted Merge Request) and re-push again. Here are examples:

	git checkout <your_branch>
	git pull origin <target_branch>
	# Resolve any conflict files you see now
	git add <all_resolved_conflict_files...>
	git commit --no-edit
	git push origin <your_branch>
If you need further help on resolving conflict.

TIPS: When resolving large and complex conflict files, it will be more helpful to find an IDE that supports Git. It usually has a visual 3 ways diff tool that let you accept/reject conflicted portion quickly.

## How often do I need to refresh my branch from target?
If you always create a new work branch from latest target branch before any work, then you do not need to update your work branch as often. In many cases, you don't need to update it at all, even if you are outdated from target branch (as long as you do not have conflict when trying to merge). The Merge Request you create will automatically trying it's best to place the changeset into the right place.

If you hold on to a work branch for too long, it's likely you have diverged from target branch quite a bit (depending how busy your team is), then in that case you may want to update your branch from target. This will also ensure you test out your changes along with latest major changes. This will happen if you keep reusing the same work branch for many tasks. Again, it's recommended you create new work branch for each task.

Another use case you have to update from target branch is when you notice your Merge Request contains conflict, and you want to resolve it locally. This will generate the conflict files list and let you resolve it and then commit the merge.

## How to reset my work branch to latest target?
If you insist to reuse an existing work branch for another task, you should at least reset it to point to latest target branch first. You can try this:

	git checkout <target_branch>
	git pull
	git branch -f <your_branch> <target_branch>
	git checkout <your_branch>
	Now you are ready to do new work on your branch.

## How to see what changed in a commit?
If you want to see single commit changeset, you use the show command:

	git show <commit_id>
If you want to see a range of commits changeset together, then you use the diff command:

	git diff <commit_id1>..<commit_id2>
Or if you want to see difference between two branches:

	git diff <target_branch>..<your_branch>
Both of these commands show and diff can take an --stat option that will list the file names that's changed only (without the diff content).

## I accidental commit changes on a wrong branch, what should I do?
Let say you accidentally committed changes into master branch instead of your own branch. You can correct it this way:

	# Assume you already on master branch with your new commits. Branch is in clean state.
	# Then simply create your work branch as normal on top of your new changes.
	# Now your branch will have your new changes.
	git checkout -b zemian-new-work
	 
	 
	# Now you want to go back to master branch and revert the un-wanted commits.
	# We assume you want to revert to your last 'pull' code state.
	git checkout master
	git reset --hard origin/master


## What is this "rebase" command I heard about?
It's an advanced feature of Git, and you shouldn't be using it unless you understand what it does first. The rebase command will perform similar action as merge command, except that it can/will re-arrange your commit histories orders! People want this for a clean commit history reason. One frequent usage is similar to perform "How to update your branch from remote host?" task section above. But that solution is using "merge" command to sync your work branch. It will work, but if you examine your commit histories, you will notice that the merged commits will sit on top of your branch commits (assume you already make some changes), and you will get an extra "merge commit" in the history. If you do this process few time while holding on the work branch, the history picture can get messy quickly, but the content you really want is simply sync from your target branch. It would be nice that if we can "refresh" your work branch to sync from target like you would the first time, and have your new changes sit on top. This is what "rebase" command will do for you: it merge your target branch commits onto your work branch, but place it where it was original left off, then move your new commits on top. This process, in affect, alter your commit histories! This is ONLY OKAY to do on your own work branch that has not pushed and merged into other long-live branches. This means you should never use "rebase" on long-live branch such as "master". Only use it on your own work branch.

NOTE: Again, a good practice to keep history clean and merge/rebase without conflicts is try to create new work branch from a latest target branch on each new task!

Here is an example of rebase usages:

	# Assume you are on your work branch with some commits already
	# And you want to sync from your target branch.
	# Ensure your are in clean state first
	git status
	git fetch
	git rebase origin/master


## How can I make changes to "master" branch without a Merge Request?
You should NOT make direct commits into long-live branches such as "master". It just good practice and help keep major branch stable by not direct commit into the branch, but only merge in code through Merge Request (MR). The reason for MR is it helps code review process. An MR typically would need at least one code reviewer (someone besides original developer) to approval or to merge it. The MR also helps highlight commit histories of what got merge into master branch (it creates an extra Git's merge commit).



However, sometimes, you really want to make just one minor change into master branch, and really do not want to create an MR. Even in this case, you can still use a merge process instead of direct commit into the master branch. This is same as what a MR would do behind the scene for you, except it will not generate a MR id number to associate the merge. Here are the steps:

	# Assume you are on master branch already
	# You first create your own branch to do work as usual
	git checkout -b zemian-my-work
	 
	 
	# Edit files and commit on your own branch, and when ready, you would
	# merge it into master without MR. However you would use "--no-ff" option
	# to ensure to create a "merge commit" with your changes.
	git checkout master
	git merge --no-ff zemian-my-work
	 
	 
	# Examine your git log to ensure what's what you want, then when ready,
	# you can push to server
	git push