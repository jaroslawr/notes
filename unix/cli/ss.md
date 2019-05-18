# ss

Show summary socket statistics:

`ss -s`

List sockets:

`ss`

List all sockets, including listening ones :

`ss -a`

List sockets along with associated processes:

`ss -p`

List connections FROM given host to given port:

`ss dst xyz.net sport = 443`

List connections TO given host and port:

`ss dst xyz.net dport = 8080`

List connections TO given subnet and port, in state ESTABLISHED (state
filter always has to come first):

`ss state ESTABLISHED dst 192.168.1/24 dport = 8080`

## Options

* `-a` list all sockets, including listening ones
* `-s` show summary statistics
* `-p` show process using socket
* `-i` show TCP state information
* `-r` show host names (resolve IPs)
* `-n` show port numbers rather than service names
