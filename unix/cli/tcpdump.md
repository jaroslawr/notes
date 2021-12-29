# tcpdump

Capture all traffic:

    tcpdump -i eth0

Capture connection traffic:

    tcpdump -i eth0 'host 192.168.0.100 and port 50000 and host 192.168.0.1 and port 443'

Capture subnet traffic:

    tcpdump -i eth0 'net 192.168.0/24'

Capture all traffic, write pcap file:

    tcpdump -i eth0 -w capture.pcap

Read and print pcap file:

    tcpdump -r capture.pcap

Read pcap file, filter and write new pcap file:

    tcpdump -r capture.pcap -w filtered.pcap 'net 192.168.0/24'

`man pcap-filter` gives details on the network filter syntax.

## Options

- `-i <interface>|any` pick network interface to use
- `-p` do not put interface in promiscuous mode
- `-w <file>` write capture to pcap file
- `-r <file>` read and print capture from pcap file
- `-c <N>` capture only N segments
- `-A` show payload in ascii
- `-X` show payload in ascii and in hex
- `-ttt` print delta time between segments
