# git checkout

Create a new branch and check it out:

    git checkout -b branch

Checkout most recently left branch:

    git checkout -

Revert individual file:

    git checkout master -- src/xyz.c

Interactively select and revert hunks in file:

    git checkout -p master -- src/xyz.c
