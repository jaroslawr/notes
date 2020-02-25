# pstree

Show process tree (including threads):

    pstree

Show process tree with thread names:

    pstree -t

Show process tree (without threads):

    pstree -T

Show process tree with pids and command line arguments, rooted at
process 123:

    pstree -ap 123

Show separate process tree for each pid namespace (needs root for full
info):

    pstree -N pid

## Options

  - `-a` show command line arguments
  - `-p` show pids
  - `-T` exclude threads
  - `-N [nstype]` show separate tree for each `nstype` namespace
  (`nstype` is one of `pid`, `mnt`, `net`, `user`, `ipc`, `uts`)
