# ncat

Sends stdin to remote endpoint, writes received response to stdout.

TCP client:

`ncat localhost 1234`

TCP server:

`ncat -l localhost 1234`

TCP echo server (persistent, -k is for "keep open"):

`ncat -l -k -e /bin/cat localhost 1234`

HTTP client:

`ncat localhost 1234 <req >resp`
