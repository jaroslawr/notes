# lsof

## Caveats

* Running without sudo simply gives an incomplete file list and no
  warnings

## Examples

* Disable hostname resolution

  `lsof -n`

* Disable port name resolution

  `lsof -P`

* List files on a specific file system

  `lsof [path]`

* Find processes accessing given file

  `lsof [file]`

* List files belonging to given process

   `lsof -p [pid]`

* List TCP sockets

    `lsof -i TCP`

* Join filtering criteria with AND

  `lsof -a -p [pid] -i TCP`
