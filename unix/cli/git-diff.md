# git diff

Show unstaged changes to the working tree:

`git diff`

Show staged changes to the working tree:

`git diff --staged`

Show changes between two arbitrary commits:

`git diff abc123 321cba`

All forms can be narrowed to a path or glob:

```
git diff -- foo.c
git diff -- 'bar/*.c'
```

## Options

* `--name-only` show only names of changed files
* `--stat` show only a summary of the changes (list of modified files,
  number of lines added/removed etc.)
* `-w` ignore whitespace changes in diff
