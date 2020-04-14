# git checkout

Create a new branch and check it out:

    git checkout -b branch

Checkout most recently left branch:

    git checkout -

Discard all changes to xyz.c, restoring contents from index:

    git checkout -- src/xyz.c

Discard selected changes to xyz.c interactively, restoring contents from index:

    git checkout -p -- src/xyz.c
