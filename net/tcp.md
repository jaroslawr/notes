# TCP

## Handshake

- Client sends segment with SYN flag, sequence number X

- Server responds with SYN+ACK, sequence number Y, acknowledgement number X+1

- SYN segment announces connection settings supported by the client and SYN+ACK
  those supported by the server:
    - MSS (Maximum Segment Size)
    - Receive window size in bytes
    - Window scale (when set to N, receive window size is scaled by 2**N)
    - Support for TCP extensions
        - SACKs (Selective acknowledgments)
        - Timestamps

- Client responds with ACK, acknowledgement number Y+1, the connection is now
  established on both ends

## Data transfer

### Reliable delivery & acknowledgement

- Sender sends out data, starts retransmission timeout (RTO) timer

    - If ACK arrives before RTO:

        - If unacknowledged data is present: reset the RTO timer
        - If no unacknowledged data is present: disable the RTO timer

    - If ACK does not arrive before RTO: retransmit and increase RTO

- Receiver ACKs at least every other segment or after at most 500ms, whatever
  comes first (if only a single segment has been received for that long)

- Receiver sends a dup-ACK (duplicate ACK) when receiving an out-of-order
  segment, re-ACKing the last byte received in-order.

- Sender monitors dup-ACKs to detect congestion and will do a *fast retransmit*
  after enough consecutive dup-ACKs, without waiting for the RTO timer to fire

### Flow control & congestion control basics

For each direction of data flow in the TCP connection, there are two limits on
how many bytes can be sent out and unacknowledged at any given moment, that have
to be respected by the side that is sending the data:

- Congestion window (`cwnd`) is a limit self-imposed by the sending side to try
  to protect the network from overload:

  - `cwnd` is computed and updated by the operating system of the sending side,
    using one of several existing congestion control algorithms

  - `cwnd` is not announced in TCP segments, it is part of the connection state
    in the OS of the sending side, which is referred to in the RFC as TCB
    (Transmission Control Block)

- Receive window (`rwnd`) is the number of bytes remaining available in the
  receivers necessarily finite receive buffer:

  - Sender learns `rwnd` from receiver who announces it in ACK segments

  - Receivers operating system will typically adjust it automatically and
    dynamically

- Sending side of the connection can send out data until `min(rwnd, cwnd)` bytes
  are unacknowledged ("on the wire").

- For a single TCP connection to reach optimal bandwith, `min(rwnd, cwnd)` needs
  to become greater than or equal to the BDP (bandwidth-delay product) of the
  bottleneck link between sender and receiver:

  - Requires send buffer at least that large on the sending side

  - Requires receive buffer at least that large on the receiving side

  - BDP example: home internet  
    `1 Gbit/s * 10ms RTT = 10 Mbit = 1.25 MB`  
    In units of typical MSS:  
    `1.25 MB / 1.5kB ~ 800`

  - BDP example: communication inside datacenter  
    `10 Gbit/s * 1ms RTT = 10 Mbit = 1.25 MB`  
    In units of typical MSS:  
    `1.25 MB / 1.5kB ~ 800`

  - BDP example: communication across datacenters (e.g. EU<->US)  
    `5 Gbit/s * 100ms RTT = 500 Mbit = 62.5 MB`  
    In units of typical MSS:  
    `62.5 MB / 1.5kB ~ 42 000`

### Flow control

- If sender fills the receive buffer faster than the receiver empties it, `rwnd`
  will eventually become zero

    - When `rwnd` becomes zero, the sender launches a persist timer, that when
      fired sends a single byte segment, a zero-window probe

    - The timer fires repeatedly until an ACK segment opening the window arrives
      from the receiver

### Congestion control

- TCP is in one of two modes depending on the value of CWND:

    - when `cwnd < ssthresh`, TCP is in slow start mode:  
      `cwnd += mss` after each ACK

    - when `cwnd > ssthresh`, TCP is in congestion avoidance mode:  
      `cwnd += mss` each RTT

    - when `cwnd = ssthresh`, implementation can choose either mode

- TCP starts in slow start, `ssthresh` starts arbitrary high, `cwnd` starts as a
  low multiple of `mss` (on Linux: `10*mss`)

- On RTO timeout:  
  `ssthresh = max(bytes_in_flight/2, 2*sender_mss)`

## Teardown

Each direction of communication is closed separately

- Endpoint 1: Sends FIN

- No more data should flow from endpoint 1 to endpoint 2

- Endpoint 2: Responds with ACK

- Endpoint 2: Sends FIN

- Endpoint 1: Responds with ACK

## References

- RFC 4614: A Roadmap for TCP Specification Documents  
  <https://tools.ietf.org/html/rfc4614.html>

- RFC 793: Original RFC for TCP  
  <https://tools.ietf.org/html/rfc793>

- RFC 2581: TCP Congestion Control RFC  
  <https://tools.ietf.org/html/rfc2581>

- RFC 1122: Requirements for Internet Hosts -- Communication Layers  
  <https://tools.ietf.org/html/rfc1122>

- RFC 1123: Requirements for Internet Hosts -- Application and Support  
  <https://tools.ietf.org/html/rfc1123>

- RFC 1958: Architectural Principles of the Internet  
  <https://tools.ietf.org/html/rfc1958>

- RFC 3439: Some Internet Architectural Guidelines and Philosophy  
  <https://tools.ietf.org/html/rfc3439>

- End-to-end arguments in system design  
  <http://web.mit.edu/Saltzer/www/publications/endtoend/endtoend.pdf>
