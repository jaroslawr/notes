# TCP

## Handshake

- Client sends segment with SYN flag, sequence number I

- Server responds with SYN+ACK, sequence number J, acknowledgement number I+1

- SYN segment announces connection settings supported by the client and SYN+ACK
  those supported by the server:
    - MSS (Maximum Segment Size)
    - Receive window size in bytes
    - Window scale (when set to `N`, receive window size is scaled by `2**N`)
    - Support for TCP extensions
        - SACKs (Selective acknowledgments)
        - Timestamps

- Client responds with ACK, acknowledgement number J+1, the connection is now
  established on both ends

## Data transfer

### Reliable delivery & acknowledgement

- Sender sends out data, starts retransmission timeout (RTO) timer

    - If ACK arrives before RTO

        - If unacknowledged data present, reset the RTO timer
        - If no unacknowledged data present, disable the RTO timer

    - If ACK does not arrive before RTO, retransmit and increase RTO

- Receiver ACKs at least every other segment or after at most 500ms (if only a
  single segment has been received for that long)

- Receiver sends a dup-ACK (duplicate ACK) when receiving an out-of-order
  segment, re-ACKing the last byte received in-order.

- Sender monitors dup-ACKs to detect congestion and will do a *fast retransmit*
  after enough consecutive dup-ACKs, without waiting for the RTO timer to fire

### Flow control & congestion control basics

- Sender can send out segments until at most min(RWND, CWND) unacknowledged
  bytes are in flight on the wire, where RWND is the size of the *receive window*
  and CWND the size of the *congestion window*

- *Receive window* is a limit due to receivers finite receive buffer size

    - Sender learns RWND from receiver who announces it in ACK segments

    - Modern operating systems will by default adjust it dynamically

- *Congestion window* is a limit to try to protect the network from overload

    - CWND is only a part of the senders TCB, not announced in TCP segments

    - Adjusted by one of several existing congestion control algorithms

- For maximum throughput min(RWND, CWND) needs to become greater than or equal
  to the BDP (bandwidth-delay product) of the bottleneck link of the connection:

    - BDP example: datacenter
      `10 Gbit/s * 1ms RTT = 10 Mbit = 1.25 MB`
      In units of typical MSS:
      `1.25 MB / 1.5kB ~ 800`

    - BDP example: home internet
      `1 Gbit/s * 5ms RTT = 5 Mbit = 0.625 MB`
      In units of typical MSS:
      `0.625 MB / 1.5kB ~ 400`

    - Requires a send buffer at least that large on the sender side

    - Requires a receive buffer at least that large on the receiver side

### Flow control

- If sender fills the receive buffer faster than the receiver empties it, RWND
  will eventually become zero

    - When RWND becomes zero, the sender launches a persist timer, that when
      fired sends a single byte segment, a *zero-window probe*

    - The timer fires repeatedly until an ACK segment opening the window arrives
      from the receiver

### Congestion control

- One of two modes depending on the value of CWND:

    - when cwnd < ssthresh, slow start:
      CWND += MSS after each ACK

    - when cwnd > ssthresh, congestion avoidance:
      CWND += MSS each RTT

    - when cwnd = ssthresh, choose either one

- TCP starts in slow start, ssthresh starts arbitrary high, CWND starts as a low
  multiple of MSS (on Linux: `10*MSS`)

- On RTO timeout:
  ssthresh = max(bytes in flight / 2, 2\* sender MSS)

## Teardown

Each direction of communication is closed separately

- Endpoint 1: Sends FIN

- No more data should flow from endpoint 1 to endpoint 2

- Endpoint 2: Responds with ACK

- Endpoint 2: Sends FIN

- Endpoint 1: Responds with ACK

## References

[rfc4614]: <https://tools.ietf.org/html/rfc4614.html>
[rfc4614] A Roadmap for TCP Specification Documents

[rfc793]: https://tools.ietf.org/html/rfc793
[rfc793] Original TCP RFC

[rfc2581]: <https://tools.ietf.org/html/rfc2581>
[rfc2581] TCP Congestion Control RFC

[rfc1122]: https://tools.ietf.org/html/rfc1122
[rfc1122] Requirements for Internet Hosts -- Communication Layers

[rfc1123]: https://tools.ietf.org/html/rfc1123
[rfc1123] Requirements for Internet Hosts -- Application and Support

[rfc1958]: https://tools.ietf.org/html/rfc1958
[rfc1958] Architectural Principles of the Internet

[rfc3439]: https://tools.ietf.org/html/rfc3439
[rfc3439] Some Internet Architectural Guidelines and Philosophy

[Saltzer]: http://web.mit.edu/Saltzer/www/publications/endtoend/endtoend.pdf
[Saltzer] End-to-end arguments in system design
