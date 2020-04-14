# du

Shows how much disk space directories and files occupy. Stands for "disk usage".

Show disk space used by subdirectories and files in the current
directory, sorted:

    du -ah -d1 | sort -rh

Show inode count used by subdirectories of the current directory,
sorted:

    du --inodes -d1 | sort -rn

## Options

- `-a` also show sizes for files
- `-h` use human readable units instead of raw bytes
- `-d <depth>` print total for each directory (with `-a` also for each file) at
  `depth`, recursively counting in all child directories and files
- `--inodes` show used inode count instead of disk space
- `--time` show last modification date for each file displayed
