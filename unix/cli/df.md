# df

Stands for "disk free".

Show free disk space on all mounted filesystems:

```
df -h
```

Show free inodes on all mounted filesystems:

```
df -i
```

Show free disk space on filesystem holding `/xyz` (traverses symlinks):

```
df -h /xyz
```

## Options

* `-h` human-readable units
* `-i` show information on inodes instead of on disk space
