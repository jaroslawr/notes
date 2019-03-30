# ps

## Examples

* Display information about specific process

  `ps u -p [pid]`

* Show memory usage of a process

  `ps -o rss,pid,cmd -p [pid]`

* Show threads of a process, with names

  `ps -T -p [pid]`

* Top 5 processes by thread count

  `ps axh -o nlwp,pid,cmd --sort -nlwp | head -n 5`

* Top 5 processes by memory usage (in kbs)

  `ps axh -o rss,pid,cmd --sort -rss | head -n 5`

## Options - BSD style

* `a` from all users
* `f` display a process tree
* `h` do not display header
* `u` user-oriented format (display additional columns)
* `x` including processes without tty

## Options - UNIX style

* `-o` specify columns to display
* `-p` filter by pid
* `-C` filter by executable name
* `-T` show threads (will display thread names if format is not overwritten by other flags)

## Options - long style

* `--sort` sort by given column, `-xyz` is descending sort by xyz,
  `+xyz` is ascending

## Column names

* `pid`
* `tid`
* `cmd`
* `rss` memory usage
* `nlwp` number of threads
* `stat` process state
