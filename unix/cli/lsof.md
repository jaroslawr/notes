# lsof

# Examples

* Use AND to join filtering criteria

  `lsof -a -p 123 -i TCP`

* Disable hostname resolution

  `lsof -n`

* Disable port name resolution

  `lsof -P`

* List files on a specific file system

  `lsof /`

* Find what processes access specific file

  `lsof file`
