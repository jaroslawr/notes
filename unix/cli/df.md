# df

Stands for "disk free".

Show free disk space on all mounted filesystems, showing filesystem
type and using human-readable units:

    df -Th

Show free disk space on filesystem holding `/xyz` (traverses symlinks):

    df -Th /xyz

Show free inodes on all mounted filesystems:

    df -i

## Options

- `-T` add filesystem type column
- `-h` use human-readable units
- `-i` show information on inodes instead of on disk space
