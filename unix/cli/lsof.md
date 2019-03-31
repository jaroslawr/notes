# lsof

## Caveats

* Running without sudo simply gives an incomplete file list and no
  warnings

## Examples

* List processes accessing file

  `lsof [file]`

* List processes accessing file system

  `lsof [path]`

* Display sockets connected to given hostname, with TCP state

  `lsof -i @hostname -Ts`

## Options

* `-p [pid]` files of process with specific pid
* `-i` list only sockets
* `-a` join given filtering criteria with AND
* `-P` disable portname resolution
* `-n` disable hostname resolution
