# ps

## Examples

* Display information about specific process

  `ps u -p [pid]`

* Show memory usage of a process (in kilobytes)

  `ps -O rss -p [pid]`

* Show threads of a process, with names

  `ps -T -p [pid]`

* Top 5 processes by thread count

  `ps axh -O nlwp --sort -nlwp | head -n 5`

* Top 5 processes by memory usage (in kbs)

  `ps axh -O rss --sort -rss | head -n 5`

## Options - BSD style

* Filters
  * `a` from all users
  * `x` including processes without tty

* Display
  * `u` user-oriented format (display additional columns)
  * `e` display environment
  * `h` do not display header

* Others
  * `f` display a process tree

## Options - UNIX style

* Filters
  * `-p` by pid
  * `-C` by executable name

* Display
  * `-o` specify columns to display
  * `-O` specify columns to display, preloaded with basic columns like pid and cmd
  * `-T` show threads (will display thread names if format is not overwritten by other flags)

## Options - long style

* `--sort` sort by given column, `-xyz` is descending sort by xyz,
  `+xyz` is ascending

## Process states

* `R` running or runnable (on run queue)
* `S` interruptible sleep (waiting for an event to complete)
* `D` uninterruptible sleep (usually IO)
* `I` idle kernel thread
* `T` stopped by job control signal
* `t` stopped by debugger during the tracing
* `W` paging (not valid since the 2.6.xx kernel)
* `X` dead (should never be seen)
* `Z` defunct ("zombie") process, terminated but not reaped by its parent

For BSD formats and when the stat keyword is used, additional characters may be displayed:

* `<` high-priority (not nice to other users)
* `N` low-priority (nice to other users)
* `L` has pages locked into memory (for real-time and custom IO)
* `s` is a session leader
* `l` is multi-threaded (using CLONE_THREAD, like NPTL pthreads do)
* `+` is in the foreground process group

## Column names

* `pid`
* `tid`
* `cmd`
* `rss` memory usage
* `nlwp` number of threads
* `stat` process state
