# git log

Search for commits changing foo.c anywhere in the tree:

    git log -- '**/foo.c'

Search for commits with message matching `pattern`:

    git log --grep=pattern

Search for commits with changes matching `pattern`:

    git log -Gpattern

Search for commits with changes adding or removing `pattern`:

    git log -Spattern

Regex syntax is POSIX basic by default, but can be changed with grep-like
options `-F`, `-E`, `-P`, `-i`, etc.

Syntax for specifying file globs is documented in `man gitglossary` under
`pathspec`.

## Options

- `-F` interpret any search patterns used as literals
- `-E` interpret any search patterns used as POSIX extended regexes
- `-P` interpret any search patterns used as Perl regular expressions
- `-i` ignore case in any search patterns used
