# grep

## Options

Patterns:

* `-e <pattern>` match `pattern`, can be supplied multiple times to
  search for all patterns
* `-E` interpret `pattern` as ERE (Extended Regular Expression)
* `-F` interpret `pattern` as a literal
* `-P` interpret `pattern` as Perl regular expression
* `-f <file>` read patterns from `file`
* `-i` ignore case
* `-w` search for whole words
* `-x` search for whole lines
* `-v` search for non-matches

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
