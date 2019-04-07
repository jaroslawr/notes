# lsof

Lists file descriptors.

```
lsof
lsof file
lsof /mnt/data
lsof -i # only sockets
lsof -i @host
lsof -i @host:80
lsof -i @host:http
lsof -i @1.2.3.4
lsof -i @1.2.3.4:80
lsof -i @1.2.3.4:http
```

The output is based on info from `/proc/<pid>/fd/` and
`/proc/<pid>/fdinfo/`.

Threads are displayed by default and files inherited from the parent
process will be shown for each thread separately.

Running without sudo might simply give an incomplete file list and no
warnings.

## Options

Filters:

* `-a` join criteria with AND
* `-p <pid>` filter by pid
* `-u <uid>` filter by uid
* `-u <uname>` filter by username
* `-d <fd>` filter by file descriptor number
* `-i` only sockets

Output:

* `-P` disable portname resolution
* `-n` disable hostname resolution
* `-Ts` display TCP socket state
