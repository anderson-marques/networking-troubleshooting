# Networking Troubleshooting

Networking Troubleshooting doesn't need to be a pain in the ass. Knowing the OSI layers and how to breaking down the problem, define a plan and have the tooling tool belt is all you need.

## Toolbelt

### nslookup - Detecting Naming Servers issues

```bash
☁  networking-troubleshooting [master] ⚡  ping www.google.com
PING www.google.com (216.58.211.228): 56 data bytes
64 bytes from 216.58.211.228: icmp_seq=0 ttl=56 time=17.468 ms
64 bytes from 216.58.211.228: icmp_seq=1 ttl=56 time=17.924 ms
64 bytes from 216.58.211.228: icmp_seq=2 ttl=56 time=19.966 ms
64 bytes from 216.58.211.228: icmp_seq=3 ttl=56 time=18.144 ms
^C
--- www.google.com ping statistics ---
4 packets transmitted, 4 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 17.468/18.375/19.966/0.950 ms
```

### ping - Testing the ICMP protocol connectivity

```bash
☁  networking-troubleshooting [master] ⚡  nslookup www.google.com
Server:         8.8.8.8
Address:        8.8.8.8#53

Non-authoritative answer:
Name:   www.google.com
Address: 216.58.211.36
```

### ipconfig/ifconfig - Getting/Updating local networking configuration

```bash
☁  networking-troubleshooting [master] ⚡  ifconfig
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
        options=1203<RXCSUM,TXCSUM,TXSTATUS,SW_TIMESTAMP>
        inet 127.0.0.1 netmask 0xff000000
        inet6 ::1 prefixlen 128
        inet6 fe80::1%lo0 prefixlen 64 scopeid 0x1
        nd6 options=201<PERFORMNUD,DAD>
gif0: flags=8010<POINTOPOINT,MULTICAST> mtu 1280
stf0: flags=0<> mtu 1280
XHC20: flags=0<> mtu 0
XHC0: flags=0<> mtu 0
en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
        ether 88:e9:fe:6c:20:96
        inet6 fe80::149c:119e:861b:f473%en0 prefixlen 64 secured scopeid 0x7
        inet 192.168.1.72 netmask 0xffffff00 broadcast 192.168.1.255
        inet6 2001:818:dbad:f00:10b5:fa68:41e6:1f58 prefixlen 64 autoconf secured
        inet6 2001:818:dbad:f00:3c8b:62ea:c649:7a04 prefixlen 64 autoconf temporary
        nd6 options=201<PERFORMNUD,DAD>
        media: autoselect
        status: active
p2p0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 2304
        ether 0a:e9:fe:6c:20:96
        media: autoselect
        status: inactive
awdl0: flags=8943<UP,BROADCAST,RUNNING,PROMISC,SIMPLEX,MULTICAST> mtu 1484
        ether a2:5a:7c:10:c3:7b
        inet6 fe80::a05a:7cff:fe10:c37b%awdl0 prefixlen 64 scopeid 0x9
        nd6 options=201<PERFORMNUD,DAD>
        media: autoselect
        status: active
en1: flags=8963<UP,BROADCAST,SMART,RUNNING,PROMISC,SIMPLEX,MULTICAST> mtu 1500
        options=60<TSO4,TSO6>
        ether 7a:00:38:39:0a:01
        media: autoselect <full-duplex>
        status: inactive
en2: flags=8963<UP,BROADCAST,SMART,RUNNING,PROMISC,SIMPLEX,MULTICAST> mtu 1500
        options=60<TSO4,TSO6>
        ether 7a:00:38:39:0a:00
        media: autoselect <full-duplex>
        status: inactive
bridge0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
        options=63<RXCSUM,TXCSUM,TSO4,TSO6>
        ether 7a:00:38:39:0a:01
        Configuration:
                id 0:0:0:0:0:0 priority 0 hellotime 0 fwddelay 0
                maxage 0 holdcnt 0 proto stp maxaddr 100 timeout 1200
                root id 0:0:0:0:0:0 priority 0 ifcost 0 port 0
                ipfilter disabled flags 0x2
        member: en1 flags=3<LEARNING,DISCOVER>
                ifmaxaddr 0 port 10 priority 0 path cost 0
        member: en2 flags=3<LEARNING,DISCOVER>
                ifmaxaddr 0 port 11 priority 0 path cost 0
        nd6 options=201<PERFORMNUD,DAD>
        media: <unknown type>
        status: inactive
utun0: flags=8051<UP,POINTOPOINT,RUNNING,MULTICAST> mtu 2000
        inet6 fe80::d914:6d0f:dc1e:a054%utun0 prefixlen 64 scopeid 0xd
        nd6 options=201<PERFORMNUD,DAD>
utun1: flags=8051<UP,POINTOPOINT,RUNNING,MULTICAST> mtu 1380
        inet6 fe80::dc66:80d:1ead:c8b3%utun1 prefixlen 64 scopeid 0xe
        nd6 options=201<PERFORMNUD,DAD>
```

### tracert/traceroute - Trace the route until a server

```bash
☁  networking-troubleshooting [master] ⚡  traceroute www.google.com
traceroute to www.google.com (172.217.168.164), 64 hops max, 52 byte packets
 1  192.168.1.1 (192.168.1.1)  1.458 ms  1.083 ms  0.899 ms
 2  3.64.54.77.rev.vodafone.pt (77.54.64.3)  4.373 ms  3.176 ms  4.411 ms
 3  113.41.30.213.rev.vodafone.pt (213.30.41.113)  3.897 ms  4.133 ms  3.505 ms
 4  74.125.52.198 (74.125.52.198)  9.268 ms  9.429 ms  9.303 ms
 5  * * *
 6  108.170.253.241 (108.170.253.241)  20.179 ms  20.194 ms  20.638 ms
 7  108.170.253.247 (108.170.253.247)  66.081 ms
    74.125.253.203 (74.125.253.203)  130.288 ms
    108.170.253.248 (108.170.253.248)  130.316 ms
 8  74.125.242.177 (74.125.242.177)  129.328 ms
    74.125.242.161 (74.125.242.161)  18.119 ms  19.829 ms
 9  74.125.253.203 (74.125.253.203)  18.297 ms
    mad07s10-in-f4.1e100.net (172.217.168.164)  128.941 ms
    74.125.253.201 (74.125.253.201)  17.379 ms
```

### telnet - Testing TCP port connectivity

```bash
☁  networking-troubleshooting [master] ⚡  telnet www.google.com 80
Trying 2a00:1450:4003:809::2004...
Connected to www.google.com.
Escape character is '^]'.
```

