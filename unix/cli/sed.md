# sed

Prefix each input line:

    sed 's/^/prefix /

Print specific field of a line matching regexp:

    sed -nE 's/.*?xyz=([0-9]+).*/\1/p'

Print input file until and including line that matches /regexp/:

    sed '/regexp/q' input

Print fragment of input file between two regexps:

    sed -n '/regexp1/,/regexp2/p' input

Print lines from 3 to 5 (inclusive) from input file:

    sed -n '3,5p' input

## Options

- `-E` extended regexps
- `-i` edit files in place
- `-n` do not print lines automatically
