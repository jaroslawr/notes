# proc

Described in detail in `man proc`.

## System-wide files

### `/proc/stat`

### `/proc/meminfo`

### `/proc/diskstats`

### `/proc/net/tcp`

## Per-process files

### `/proc/<pid>/stat`

### `/proc/<pid>/status`

### `/proc/<pid>/task/<tid>/`

### `/proc/<pid>/cmdline`

The full command line of the process.

### `/proc/<pid>/environ`

The environment of the process. The variable name-value pairs are
null-separated.

Show the process environment in a readable format:

    xargs -0 < /proc/<pid>/environ

### `/proc/<pid>/fd/`

Directory containing a symlink for each file descriptor the process uses. The
symlink either points to a real file, or is a string descrbing a special kind of
file, like "socket[123456]".

List top 5 processes with most open files:

    find /proc -maxdepth 1 -regex '/proc/[0-9]+' -printf "%f\n" |
        while read pid; do
            echo $(find /proc/$pid/fd | wc -l) $pid $(cat /proc/$pid/cmdline)
        done | 
        sort -k1,1 -rn | head -n5 | column -t

List file descriptors of process with given pid:

    find /proc/<pid>/fd -printf "%p %l\n"

### `/proc/<pid>/net/tcp`

### `/proc/<pid>/ns/`

Directory containing symlinks describing the namespaces the process uses:

    /proc/1/ns/net -> net:[4026531992]
    /proc/1/ns/uts -> uts:[4026531838]
    /proc/1/ns/ipc -> ipc:[4026531839]
    /proc/1/ns/pid -> pid:[4026531836]
    /proc/1/ns/pid_for_children -> pid:[4026531836]
    /proc/1/ns/user -> user:[4026531837]
    /proc/1/ns/mnt -> mnt:[4026531840]
    /proc/1/ns/cgroup -> cgroup:[4026531835]

