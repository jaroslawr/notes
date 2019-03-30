# Sed

## Examples

* Enable extended regexps

  `sed -E`

* Do not print lines automatically

  `sed -n`

* Change files in place

  `sed -i '[script]' *.txt`

* Print specific field of a line matching regexp

  `sed -nE 's/.*?xyz=([0-9]+).*/\1/p'`

* Print input file until and including line that matches /regexp/

  `sed '/regexp/q' input`

* Print fragment of input file between two regexps

  `sed -n '/regexp1/,/regexp2/p' input`

* Print lines from 3 to 5 (inclusive) from input file

  `sed -n '3,5p' input`
