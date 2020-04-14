# pgrep

List pids of processes matching pattern, one per line:

    pgrep -f postgres

List pids of processes matching pattern, comma-delimited:

    pgrep -fd, postgres

List pids and command lines of processes matching pattern:

    pgrep -fa postgres

The pattern is an Extended Regular Expression, like in `sed -E` and
`grep -E`.

## Options

### Matching

- `-f` match pattern against full command line
- `-x` only exact matches

### Output

- `-a` show full command line in output
- `-d <delim>` use `delim` as pid separator in output
- `-c` count processes instead of listing them
