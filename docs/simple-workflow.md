Here we quickly highlight some frequently used commands

```
# == How to get code from a Git host server such as GitHub or GitLab
# These server privide Git repository served from https or ssh protocal, 
# and you usually clone it using a URL that ends with <project_name>
git clone <git_repository_url>
cd <project_name>

# If you want to clone and rename your repository
git clone <git_repository_url> <new_project_name>
 
 
# == Get a list of branches available
# The default branch Git used is "master" when you first cloned it. Your project
# may have many other branches that you want to explore.
git branch -a

# Show local branchs only
git branch

# Show remote branches only
git branch -r
 
 
# == How to switch to other branch and view that code
git checkout <work_branch>
 
 
# == How to tell what branch you are on
git status
 
# == How to get updates from server
# NOTE: Git pull will get all updates from server, but will only update ONE branch that you currently
# sitting on. You can see which branch using "git status" command first.
git pull
 
# == How to create your own new branch and start work
# The following example will create a branch <work-branch> starting from "master". The "master"
# is the target branch when you want to create a MergeRequest later. You always need to know
# where you create your branch "from" as the target! So often it's good idea to prefix
# your work brach with target in front as a reminder.
git checkout -b <work-branch> master

# The master is optional if you are already on the branch
git status
git checkout -b <work-branch>

# Using prefix
git checkout -b master_<work-branch>
 
 
# == How to make changes. (note: You may use multi-lines in commit message.)
# Git requires two commands to fully commit changes! Do not forget to add & commit!
# You may repeat these as many time as you need, and Git works locally without server connection.
# NOTE: You do the same command for <new_file> as well!
git add <changed_file_or_new_file...>
git commit -m 'subject: What you did message goes here'
 
 
 
# == Verify your commits and logs
# Each Git commit will have a unique "commit-id", and you and view
# the details of that change using the "show" command as follow.
# NOTE: Type 'q' to exit the pager/viewer if you have many log commit messages.
git log
git show <commit-id>
 
# == How to get latest update from server
# Assume you are in your own <work_branch> that you started committed some work already,
# and you realize the "target" you got it from has new updates. Then you want to sync
# up the updates with the following. (Remember that "target" branch is often your "master"
# when you first crated your branch.)
git status # ensure its' clean
git pull
 
# == How to upload to server and create a merge request
git check <work_branch>
# Makes local changes and then commit on your own work_branch
git push origin <work_branch>

# If you want to push multiple times then you should track it once
git push -u origin <work_branch>
# then subsequent push does not require extra parameters
git push

# Now go to the Git hosting server and create a MergeRequest from your work_branch
# against your target branch. You should have your MergeRequest by your teammate before
# merge it in.
```