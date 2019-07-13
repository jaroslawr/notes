# Sockets

## TCP session with BSD sockets

### Server startup (*passive open*)

* Server calls `socket()`, which returns a file descriptor for a new
  socket

* Server calls `bind()`, assigns hostname and port to the socket

* Server calls `listen()`, turning the socket into a *listening
  socket*, in LISTEN state
  
* Server receives SYN from client, kernel places the connection in a
  *SYN queue*, responds with SYN-ACK
  
* Server receives the final ACK of the handshake from client, kernel
  moves the connection from *SYN queue* to *accept queue*
  
* Server calls `accept()`, which blocks until there is a connection
  ready in the accept queue

* `accept()` completes, removes a connection from front of the queue,
  returns a file descriptor for a separate *connected socket*, which
  starts in state ESTABLISHED
  
The length of the SYN queue for a socket is limited by
`/proc/sys/net/ipv4/tcp_max_syn_backlog`.

The length of the accept queue for a socket is limited by the
`backlog` argument of `listen()` and by the system limit
`/proc/sys/net/core/somaxconn`.
  
### Connection start (*active open*)

* Client calls `socket()`, followed by `connect()`, initiating the TCP
  handshake

* TCP SYN segment is sent to the server, clients socket enters the
  SYN-SENT state

* Server responds with SYN-ACK segment

* Client receives SYN-ACK, `connect()` returns, client socket enters
  ESTABLISHED state, ACK is sent back

### Data transfer

Client and server use the same syscalls for receiving and sending
data: read()/write(), recv()/send() or recvmsg()/sendmsg()

### Connection termination (*active close*)

*Active close* can be done by either side of the connection:

* The active side calls `close()`, FIN is sent to the peer, socket
  enters the FIN-WAIT-1 state
  
* Neither `send()` nor `recv()` can be done anymore, although at TCP
  level only one end of the connection is closed and the peer can
  still send in data

* ACK is received from the peer, socket enters the FIN-WAIT-2 state

* FIN is received from the peer, ACK is sent back, socket enters the
  TIME-WAIT state

### Connection termination (*passive close*)

* FIN is received, socket enters the CLOSE-WAIT state

* The passive side learns the peer has closed its part of the
  connection on the next attempt to call `recv()`, which returns 0
  
* The passive side can still use `send()`
  
* The passive side calls `close()`, sends its own FIN to the peer,
  socket enters the LAST-ACK state

* ACK is received from the peer, socket gets closed
