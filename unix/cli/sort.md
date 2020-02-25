# sort

Sorts all lines from all files and writes the result to standard
output. It uses an external merge sort algorithm, so it can sort files
larger than the amount of available memory.

Sort in ascending dictionary order:

    sort

Show a histogram of lines:

    sort | uniq -c

Sort by 1st field ascending, then by 2nd field descending:

    sort -k1,1 -k2,2r

Show one line per each unique 2nd field:

    sort -k2,2 -u

Sort by descending numeric value of 2nd field, with : as field separator:

    sort -t: -k2,2rn

Sort by human-readable units (1G, 1M, 1K etc.):

    sort -h

## Notes

Transition from non-blank to blank character is the default field separator.

## Options

  - `-t <c>` use `c` as field separator
