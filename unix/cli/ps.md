# ps

List all processes:

`ps ax`

List all processes, with additional columns:

`ps aux`

Show process hierarchy:

`ps auxf`

List top 5 processes by memory usage (in kbs):

`ps ax -O rss --sort -rss | head -n 6`

List top 5 processes by thread count:

`ps ax -O nlwp --sort -nlwp | head -n 6`

Show full info on process with PID 123:

`ps u 123`

Show info on group of processes:

`ps u $(pgrep chrome)`

Show threads of process with PID 123, with names:

`ps -T 123`

## Options - BSD style

Filters:

* `a` from all users
* `x` including processes without tty

Output:

* `u` user-oriented format (adds columns: %CPU, %MEM, RSS, start time)
* `e` display environment
* `h` do not display header
* `f` display a process tree

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
* `-T` show threads (will display thread names if used with -p and without format flags)

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
* `cgroup`
