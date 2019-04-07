# pgrep

List pids of processes matching pattern, one per line:

```
pgrep -f postgres
```

List pids of processes matching pattern, comma-delimited:

```
pgrep -fd, postgres
```

List pids and command lines of processes matching pattern:

```
pgrep -fa postgres
```

The pattern is an Extended Regular Expression, like in `sed -E` and
`grep -E`.

## Options

* `-a` show full command line in output
* `-f` match pattern against full command line
* `-d <delim>` use delim as separator
* `-c` count processes instead of listing them
