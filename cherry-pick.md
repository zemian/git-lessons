# how cherry pick work

Given one or more existing commits, apply the change each one introduces, recording a new commit for each. 
This requires your working tree to be clean (no modifications from the HEAD commit).

WARN: The cherry pick will make a copy of a commit, and generate a new commit id! This might generate
extra noise and even possible conflict if you are not careful.
