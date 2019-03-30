# Sort

## Examples

* Show a histogram of lines

  `<input | sort | uniq -c`

* Sort by descending value of 2nd field, with : as delimiter

  `<input | sort -rn -t: -k2,2`

* Sort by 1st field ascending, then by 2nd field descending: (with default delimiter: whitespace)

  `<input | sort -r -k1,1 -k2,2r`

* Sort by human-readable units (1G, 1M, 1K etc.)

  `<input | sort -h`
