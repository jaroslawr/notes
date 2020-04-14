# git diff

Show unstaged changes:

    git diff

Show staged changes:

    git diff --staged

Show both unstaged and staged changes:

    git diff HEAD

Show changes between two arbitrary commits:

    git diff abc123 321cba

All forms can be narrowed to a path or glob:

    git diff -- foo.c
    git diff -- '**/foo.c'
    git diff -- 'bar/*.c'

Syntax for specifying file globs is documented in `man gitglossary` under
`pathspec`.

## Options

- `--name-only` show only names of changed files
- `--stat` show only a summary of the changes (list of modified files, number of
  lines added/removed etc.)
- `-w` ignore whitespace changes in diff
