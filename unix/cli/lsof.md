# lsof

List all file descriptors:

```
lsof
```

List file descriptors referencing `file`:

```
lsof file
```

List file descriptors referencing anything on `/mnt/data`:

```
lsof /mnt/data
```

List file descriptors of process with pid `123`:

```
lsof -p 123
```

List socket file descriptors:

```
lsof -i
```

List socket file descriptors connected to `host`:
```
lsof -i @host
```

List socket file descriptors connected to `host` on port 80:

```
lsof -i @host:80
```

List socket file descriptors owned by process with pid `123`:

```
lsof -a -i -p 123
```

The output is based on info from `/proc/<pid>/fd/` and
`/proc/<pid>/fdinfo/`.

Threads are displayed by default and files inherited from the parent
process will be shown for each thread separately.

Running without sudo might simply give an incomplete file list and no
warnings.

Disabling hostname resolution with `-n` makes `lsof` much faster when
there are lots of sockets.

Disabling portname resolution with `-P` is often also helpful.

Disabling username resolution with `-l` prevents UID resolution
errors, e.g. with Docker.

## Options

Filters:

* `-a` join criteria with AND
* `-p <pid>` filter by process id
* `-c <cmd>` filter by process executable name
* `-u <uid>` filter by process uid
* `-u <uname>` filter by process username
* `-d <fd>` filter by file descriptor number
* `-i` only sockets

Output:

* `-t` only display pids
* `-P` disable portname resolution
* `-n` disable hostname resolution
* `-l` disable username resolution
* `-Ts` display TCP socket state
