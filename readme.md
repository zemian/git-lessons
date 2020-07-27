# About Git

https://git-scm.com/

## About Parents Ref

- Use HEAD, HEAD~1, HEAD~2 to reference the commit on current branch. This can 
  be used in "git show" for example.

- Use "<merge-commit>^1" to reference parent 1, and "<merge-commit>^2" for parent 2.

# https://stackoverflow.com/questions/2221658/whats-the-difference-between-head-and-head-in-git

Rules of thumb

    Use ~ most of the time — to go back a number of generations, usually what you want
    Use ^ on merge commits — because they have two or more (immediate) parents

Mnemonics:

    Tilde ~ is almost linear in appearance and wants to go backward in a straight line
    Caret ^ suggests an interesting segment of a tree or a fork in the road

