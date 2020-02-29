# git log

Search for commits changing foo.c anywhere in the tree:

    git log -- '**/foo.c'

Search for commits with changes matching `pattern`:

    git log -Gpattern

Search for commits with changes matching `pattern`:

    git log -Spattern

Search for commits with message matching `pattern`:

    git log --grep=pattern

Regex syntax is POSIX basic by default, but can be changed with grep-like
options.

Syntax for specifying file globs is documented in `man gitglossary` under
`pathspec`.

## Options

  - `-F` interpret any patterns used as literals
  - `-E` interpret any patterns used as POSIX extended regexes
  - `-P` interpret any patterns used as Perl regular expressions
  - `-i` ignore case in any patterns used
