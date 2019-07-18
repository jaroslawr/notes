# grep

Search for pattern in stdin:

`grep pattern`

Search for pattern recursively in current directory:

`grep -R pattern`

Search for pattern recursively in given directory:

`grep -R pattern dir`

Serach stdin for one of the patterns from patfile:

`grep -f patfile`

## Options

Patterns:

* `-e <pattern>` supply multiple times to match on one of multiple patterns
* `-f <file>` read patterns from `file`
* `-F` interpret `<pattern>` as a literal
* `-E` interpret `<pattern>` as an ERE (Extended Regular Expression)
* `-P` interpret `<pattern>` as Perl regular expression
* `-x` search for whole lines
* `-w` search for whole words
* `-v` search for non-matches
* `-i` ignore case

Mode:

* `-c` count occurences
* `-l` list files matching pattern
* `-L` list files NOT matching pattern

Display:

* `-n` show line number on matches
* `-o` only show matching parts of line

Directory traversal:

* `-R` recursive search
* `-I` ignore binary files (in recursive search)
