# sort

* Default sort order is ascending dictionary order

* Default field delimiter is any whitespace character

## Examples

* Show a histogram of lines

  `sort [file] | uniq -c`

* Sort by 1st field ascending, then by 2nd field descending:

  `sort [file] -k1,1 -k2,2r`

* Sort by descending numeric value of 2nd field, with : as field delimiter

  `sort [file] -t: -k2,2rn`

* Sort by human-readable units (1G, 1M, 1K etc.)

  `sort [file] -h`
