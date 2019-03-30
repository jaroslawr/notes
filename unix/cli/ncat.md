# ncat

## Examples

* Start one-shot server

  `ncat -l [hostname] [port]`

* Start persisent server (-k for "keep open")

  `ncat -kl [hostname] [port]`

* Echo server

  `ncat -kl -e /bin/cat [hostname] [port]`

* Start client

  `ncat [hostname] [port]`
