# ss

List sockets (in states other than `LISTEN`, `TIME-WAIT` or
`SYN-RECV`):

    ss

List all sockets:

    ss -a

List TCP sockets:

    ss -t

List sockets with their owner processes:

    ss -p

List listening TCP sockets with their owner process:

    ss -lptn

List connections FROM given host to given port:

    ss dst xyz.net sport = 443

List connections TO given host and port:

    ss dst xyz.net dport = 8080

List connections TO given subnet and port, in state ESTABLISHED (state
filter always has to come first):

    ss state ESTABLISHED dst 192.168.1/24 dport = 8080

Show summary socket statistics:

    ss -s

Some information will only be shown correctly when running as root.

## Options

  - `-a` list all sockets
  - `-l` list only listening sockets
  - `-t` list only TCP sockets
  - `-u` list only UDP sockets
  - `-s` show summary statistics
  - `-p` show process using socket
  - `-i` show TCP socket state (e.g. total bytes sent, total bytes received)
  - `-r` show host names (resolve IPs)
  - `-n` show port numbers rather than service names
