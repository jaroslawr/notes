# uniq

Examines adjacent lines for duplicates. Sorting the input first is
often useful.

Print those lines from stdin which are not duplicating the preceding
line:

    uniq

Like above, but precede each line by the number of its occurences in
the original stream:

    uniq -c

Print those lines from stdin which are not followed by any adjacent
duplicates:

    uniq -u

Print those lines from stdin which are followed by adjacent duplicates:

    uniq -d

Print those lines from stdin which are followed by adjacent duplicates,
along with the duplicates themselves:

    uniq -D

Set union (a ∪ b):

    sort a b | uniq

Set intersection (a ∩ b):

    sort a b | uniq -d

Set difference (a ∖ b):

    sort a b b | uniq

## Options

- `-u` prints a line only if there are no adjacent duplicate lines
- `-d` prints a line only if it has adjacent duplicate lines
- `-D` like `-d`, but also prints all the adjacent duplicates
- `-c` prefix each line by number of its occurences
