# ss

Show summary socket statistics:

`ss -s`

List (non-listening) sockets:

`ss`

List all sockets:

`ss -a`

List connections TO given host and port:

`ss dst xyz.net and dport = 443`

List connections FROM given host to given port:

`ss dst xyz.net and sport = 80`

## Options

* `-a` list all sockets (including listening ones)
* `-s` show summary statistics
* `-p` show process using socket
* `-i` show additional socket TCP information
