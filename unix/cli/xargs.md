# xargs

Executes command using standard input to build the argument list.

By default whitespace and newlines are treated as delimeters.

## Options

  - `-d <delim>` use `delim` as separator for input items
  - `-n <N>` use a max of `N` args per executed command line
  - `-L <L>` use a max of `L` input lines per executed command line
  - `-P <P>` run up to `P` concurrent processes
  - `-I <dummy>` replace occurrences of `dummy` in the command line
  with the read inputs
