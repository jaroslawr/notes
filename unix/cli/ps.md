# ps

List all processes:

`ps -e`

Show process hierarchy:

`ps -eH`

List top 5 processes by memory usage (in kbs):

`ps -e -O rss --sort -rss | head -n 6`

List top 5 processes by thread count:

`ps -e -O nlwp --sort -nlwp | head -n 6`

Show full info on specific process:

`ps -p 123 -Fl`

Show info on group of processes:

`ps -p $(pgrep -d, chrome) -Fl`

Show threads of a process, with names:

`ps -p 123 -T`

## Options - UNIX style

Filters:

* `-e` all processes
* `-p <pid>` by pid
* `-C <name>` by executable name

Output:

* `-f` full format (adds user name column among others)
* `-F` extra-full format (adds memory usage column among others)
* `-l` long format (adds process state column among others)
* `-o <columns>` specify columns to display
* `-O <columns>` specify columns to display, preloaded with basic columns like pid and cmd
* `-H` show process hierarchy
* `-T` show threads (will display thread names if format is not overwritten by other flags)

## Options - BSD style

Filters:

* `a` from all users
* `x` including processes without tty

Output:

* `u` user-oriented format (display additional columns)
* `e` display environment
* `h` do not display header
* `f` display a process tree

## Options - long style

* `--ppid` filter by parent process pid
* `--sort` sort by given column, `-xyz` is descending sort by xyz,
  `+xyz` is ascending

## Process states

* `R` running or runnable (on run queue)
* `S` interruptible sleep (waiting for an event to complete)
* `D` uninterruptible sleep (usually IO)
* `I` idle kernel thread

## Column names

* `pid`
* `tid`
* `cmd`
* `rss` memory usage
* `nlwp` number of threads
* `stat` process state
