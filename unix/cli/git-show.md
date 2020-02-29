# git show

Show changes made in given commit:

    git show # defaults to HEAD
    git show abc123
    git show abc123 -- foo.c
    git show abc123 -- '**/foo.c'
    git show abc123 -- 'bar/*.c'

## Options

Accepts most [git-diff](git-diff.md) options. Syntax for specifying file globs
is documented in `man gitglossary` under `pathspec`.

