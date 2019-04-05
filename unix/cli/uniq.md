# uniq

Examines adjacent lines for duplicates. Presorting of the input might
be useful for some applications.

For simply selecting unique items from an unordered list, use `sort
-u` or `awk '!seen[$0]++'`.

## Options

* with no arguments, prints a line, skips all adjacent identical lines, etc.
* `-u` prints a line only if there are no adjacent duplicate lines
* `-d` prints a line only if it has adjacent duplicate lines
* `-D` like `-d`, but also prints all the adjacent duplicates
* `-c` prefix each line by number of its occurences
