# strace

Trace system calls of `ls`:

    strace ls

Trace system calls of process with pid:

    strace -p <pid>

## Options

- `-tt` print timestamps with microsecond precision
- `-y` annotate file fds with filename
- `-yy` annotate all possible fds: file fds with paths, sockets with IP addresses, etc.
- `-v` do not abbreviate information about structures
