# grep

Search stdin for lines matching pattern:

    grep pattern

Search stdin for lines matching pattern or pattern2:

    grep -e pattern -e pattern2

Serach stdin for lines matching any of the patterns from patfile:

    grep -f patfile

Recursively search current directory for lines matching pattern:

    grep -r pattern

Recursively search dir for lines matching pattern:

    grep -r pattern dir

List files in dir matching pattern:

    grep -rl pattern dir

<pattern> is a POSIX Basic Regular Expression by default, with `.` matching any
character, with `\(` and `\)` for grouping, `\|` for alternative `\{` and `\}`
for counts etc.

<pattern> might need to be quoted to prevent shell expansion.

## Options

### Patterns

  - `-e <pattern>` supply multiple times to match any of multiple patterns
  - `-f <file>` read patterns from `file`
  - `-F` interpret `<pattern>` as a literal
  - `-E` interpret `<pattern>` as an ERE (Extended Regular Expression)
  - `-P` interpret `<pattern>` as Perl regular expression
  - `-x` search for whole lines
  - `-w` search for whole words
  - `-v` search for non-matches
  - `-i` ignore case

### Mode

  - `-c` count occurences
  - `-l` list files matching pattern
  - `-L` list files NOT matching pattern
  - `-q` no output, exit with 0 status on first match

### Display

  - `-n` show line number on matches
  - `-o` only show matching parts of line

### Directory traversal

  - `-r` recursive search
  - `-R` recursive search which also follows symlinks
  - `-I` ignore binary files (in recursive search)
