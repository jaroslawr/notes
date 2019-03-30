# git

## Examples

* Create a new branch and check it out

  `git checkout -b branchname`

* Checkout most recently left branch

  `git checkout -`

* Show changes to files matching pattern

  `git diff -- '*pattern*'`

* Show summary of current changes

  `git diff --stat`

* Show only names of changed files 

  `git diff --name-only`

* Ignore whitespace changes in diff

  `git diff -w`

* Show single commit

  `git show [hash]`

* Show single commit summary (list of modified files etc.)

  `git show --stat [hash]`

* Show changes to a specific file in given commit

  `git show [hash] -- file`

* Show changes to files matching pattern in given commit

  `git show [hash] -- '*pattern*'`
