Git always create branch based on existing commit. Sometimes you want to fix the first commit of the git repo, 
then use orphan branch to re-setup the history.

  git checkout --orphan orphan-branch
  git commit --allow-empty -m 'First commit on orphan branch using --allow-empty flag'
