# git log

Search for commits changing foo.c anywhere in the tree:

    git log -- '**/foo.c'

Search for commits with message matching `pattern`:

    git log --grep=pattern

Search for commits with changes matching `pattern`:

    git log -Gpattern

Search for commits with changes adding or removing `pattern`:

    git log -Spattern

Show commits since a given fixed date:

    git log --since=2020-01-01

Show commits since a given time period:

    git log --since="1 month ago"

Show commits between two dates:

    git log --since=2020-01-01 --until=2020-01-31

Like in grep, patterns by default are interpreted as POSIX basic regular
expressions, but this can be changed with options: `-F`, `-E`, `-P`, `-i`.

Syntax for specifying file globs is documented in `man gitglossary` under
`pathspec`.

## Options

- `-F` interpret any search patterns used as literals
- `-E` interpret any search patterns used as POSIX extended regexes
- `-P` interpret any search patterns used as Perl regular expressions
- `-i` ignore case in any search patterns used
