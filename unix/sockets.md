# Sockets

## TCP session with BSD sockets

### Server startup

- Server calls `socket()`, which returns a file descriptor for a new socket

- Server calls `bind()`, assigns hostname and port to the socket

- Server calls `listen()`, turning the socket into a listening socket, in
  LISTEN state

- Server calls `accept()`, which blocks until there is a connection ready in the
  accept queue

### Client-side connection start (*active open*)

- Client calls `socket()`, followed by `connect()`, kernel picks ephemeral port
  for the connection, TCP handshake is initiated

- TCP SYN segment is sent to the server, clients socket enters the SYN-SENT
  state

- Server responds with SYN-ACK segment

- Client receives SYN-ACK, `connect()` returns, client socket enters ESTABLISHED
  state, ACK is sent back

### Server-side connection start (*passive open*)

- Server receives SYN from client, puts the connection in the SYN queue,
  responds with SYN-ACK, waits for an ACK

- Server receives the final ACK of the handshake from client

  - If the accept queue is not full, kernel moves the connection from SYN queue
    to accept queue

  - If accept queue is full, kernel simply ignores the ACK. In consequence, the
    timer for retransmission of SYN-ACK will fire as if the ACK did not arrive,
    causing the client to resend the ACK and causing another attempt at putting
    the connection in the accept queue after some delay

- `accept()` completes, removes a connection from front of the queue, returns a
  file descriptor for a separate connected socket, which starts in state
  ESTABLISHED

### Data transfer

Client and server use the same syscalls for receiving and sending data:
read()/write(), recv()/send() or recvmsg()/sendmsg()

### Connection termination (*active close*)

Active close can be initiated by either side of the connection:

- The active side calls `close()`, FIN is sent to the peer, socket enters the
  FIN-WAIT-1 state

- Neither `send()` nor `recv()` can be done anymore, although at TCP level only
  one end of the connection is closed and the peer can still send in data

- ACK is received from the peer, socket enters the FIN-WAIT-2 state

- FIN is received from the peer, ACK is sent back, socket enters the TIME-WAIT
  state

### Connection termination (*passive close*)

- FIN is received, socket enters the CLOSE-WAIT state

- The passive side learns the peer has closed its part of the connection on the
  next attempt to call `recv()`, which returns 0

- The passive side can still use `send()`

- The passive side calls `close()`, sends its own FIN to the peer, socket enters
  the LAST-ACK state

- ACK is received from the peer, socket gets closed

## Limits

### Common

- `fs.file-max` sysctl - system-wide limit on the number of open file
  descriptors

    - opening a socket will fail with errno `ENFILE` if exhausted

- `fs.nr_open` sysctl - process-wide limit on the number of open file
  descriptors

    - opening a socket will fail with errno `EMFILE` if exhausted

    - the limit can be lowered by a process with `setrlimit()` and any created
      child processes will then inherit the change

    - `setrlimit()` allows to set a soft limit and a hard limit, the hard limit
      caps the soft limit and can only be decreased, the soft limit can be
      changed up and down and is the ultimately effective limit

    - systemd, docker, PAM etc. can manipulate this, in bash it can be changed
      with `ulimit -n`

    - check effective value with `prlimit -n -p <pid>`

### Server side

- `net.ipv4.tcp_max_syn_backlog` sysctl - length of the SYN queue for a single
  socket

- `net.core.somaxconn` sysctl - length of the accept queue for a single socket

    - can be lowered by supplying a `backlog` argument to `listen()`

### Client side

- `net.ipv4.ip_local_port_range` sysctl - range of ports to be used for outgoing
  connections, effectively a limit on the number of connections to a single
  destination IP address and port

