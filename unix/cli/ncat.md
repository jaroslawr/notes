# ncat

## Examples

* TCP server (one shot, util first connection ends)

  `ncat -l [hostname] [port]`

* TCP server (persistent, -k for "keep open")

  `ncat -l -k [hostname] [port]`

* TCP echo server (persistent)

  `ncat -l -k -e /bin/cat [hostname] [port]`

* TCP client

  `ncat [hostname] [port]`
