# ss

List sockets:

`ss`

List all sockets (including listening ones):

`ss -a`

List connections TO given host and port, including owner process:

`ss -p dst xyz.net and dport = 443`

List connections FROM given host to given port, including owner
process:

`ss -p dst xyz.net and sport = 80`

Show summary socket statistics:

`ss -s`

## Options

* `-a` list all sockets, including listening ones
* `-s` show summary statistics
* `-p` show process using socket
* `-i` show TCP state information
* `-r` show host names (resolve IPs)
* `-n` show port numbers rather than service names
