# pidstat

Show process CPU utilization, with full command lines, reporting every second:

    pidstat -ul 1

Show process I/O activity, with full command line, reporting every second:

    pidstat -dl 1

Show process CPU utilization and I/O activity, with full command line and in one
summary, reporting every second:

    pidstat -udlh 1
    
Show process memory utilization, with full command line, reporting every second:

    pidstat -rl 1

Show CPU utilization of given process and its threads, reporting every second:

    pidstat -p 123 -t 1

## Options

### Resources to monitor

- `-u` CPU
- `-d` Disk
- `-r` Memory
- `-t` Fds and threads

### Formatting

- `-l` Show full command lines
- `-h` Show statistics on multiple resources in a single line
- `--human` Use human readable units
