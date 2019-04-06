# uniq

Examines adjacent lines for duplicates. By default, after every line
printed, it skips all adjacent identical lines.

Presorting of the input might be useful for some applications.

## Options

* `-u` prints a line only if there are no adjacent duplicate lines
* `-d` prints a line only if it has adjacent duplicate lines
* `-D` like `-d`, but also prints all the adjacent duplicates
* `-c` prefix each line by number of its occurences
