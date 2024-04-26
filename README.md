# 2.Konfiguracja urządzeń i weryfikacja łączności

### Show ip route
```
      10.0.0.0/8 is variably subnetted, 3 subnets, 2 masks
O        10.1.1.0/30 [110/128] via 10.2.2.2, 00:00:15, Serial0/0/1
C        10.2.2.0/30 is directly connected, Serial0/0/1
L        10.2.2.1/32 is directly connected, Serial0/0/1
O     192.168.10.0/24 [110/129] via 10.2.2.2, 00:00:15, Serial0/0/1
      192.168.20.0/32 is subnetted, 1 subnets
O        192.168.20.1 [110/129] via 10.2.2.2, 00:00:15, Serial0/0/1
      192.168.30.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.30.0/24 is directly connected, GigabitEthernet0/1
L        192.168.30.1/32 is directly connected, GigabitEthernet0/1
      192.168.40.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.40.0/24 is directly connected, Loopback0
L        192.168.40.1/32 is directly connected, Loopback0
      209.165.200.0/32 is subnetted, 1 subnets
O        209.165.200.225 [110/65] via 10.2.2.2, 00:00:25, Serial0/0/1

```

### 2.5.d Ping R3 -> PC-A
```
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.10.3, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 28/28/32 ms
```
### Ping PC-C -> PC-A
```
C:\Users\student>ping 192.168.10.3

Pinging 192.168.10.3 with 32 bytes of data:
Reply from 192.168.10.3: bytes=32 time=18ms TTL=125
Reply from 192.168.10.3: bytes=32 time=18ms TTL=125
Reply from 192.168.10.3: bytes=32 time=18ms TTL=125
Reply from 192.168.10.3: bytes=32 time=18ms TTL=125

Ping statistics for 192.168.10.3:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 18ms, Maximum = 18ms, Average = 18ms
```

### PC-C -> R1:loopback
```
C:\Users\student>ping 192.168.20.1

Pinging 192.168.20.1 with 32 bytes of data:
Reply from 192.168.20.1: bytes=32 time=18ms TTL=253
Reply from 192.168.20.1: bytes=32 time=18ms TTL=253
Reply from 192.168.20.1: bytes=32 time=18ms TTL=253
Reply from 192.168.20.1: bytes=32 time=18ms TTL=253

Ping statistics for 192.168.20.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 18ms, Maximum = 18ms, Average = 18ms
```
# 3.Konfiguracja i   weryfikacja   standardowych   numerowanych   oraz nazywanych list ACL

## 3.1 Konfiguracja i weryfikacja standardowych numerowanych list ACL

Jaka  maska blankietowa (wildcard mask) powinna być użyta w celu zezwolenia na ruch od wszystkich hostów z sieci 192.168.10.0/24 do hostów z sieci 192.168.30.0/24?Wynik zapisz w pliku tekstowym

```
Router(config)# access-list 1 permit ip 192.168.10.0 0.0.0.255 192.168.30.0 0.0.0.255
```

Bazując na polityce bezpieczeństwa, na którym routerze ustawisz tę listę ACL? 
```
Router R3
```

Na którym interfejsie uruchomisz tę listę ACL? Do którego kierunku ruchu będzie się ona odnosić?
```
R3 G0/1 Out
```

### Zweryfikuj numerowaną listę ACL
```
R3#show access-list 1
Standard IP access list 1
    10 permit 192.168.10.0, wildcard bits 0.0.0.255 (4 matches)
    20 permit 192.168.20.0, wildcard bits 0.0.0.255
    30 deny   any
```
```
R3#show access-lists
Standard IP access list 1
    10 permit 192.168.10.0, wildcard bits 0.0.0.255 (4 matches)
    20 permit 192.168.20.0, wildcard bits 0.0.0.255
    30 deny   any
```

```
R3#show ip interface g0/1
GigabitEthernet0/1 is up, line protocol is up
  Internet address is 192.168.30.1/24
  Broadcast address is 255.255.255.255
  Address determined by setup command
  MTU is 1500 bytes
  Helper address is not set
  Directed broadcast forwarding is disabled
  Multicast reserved groups joined: 224.0.0.5 224.0.0.6
  Outgoing access list is 1
  Inbound  access list is not set
  Proxy ARP is enabled
  Local Proxy ARP is disabled
  Security level is default
  Split horizon is enabled
  ICMP redirects are always sent
  ICMP unreachables are always sent
  ICMP mask replies are never sent
  IP fast switching is enabled
  IP fast switching on the same interface is disabled
  IP Flow switching is disabled
  IP CEF switching is enabled
  IP CEF switching turbo vector
  IP multicast fast switching is enabled
  IP multicast distributed fast switching is disabled
  IP route-cache flags are Fast, CEF
  Router Discovery is disabled
  IP output packet accounting is disabled
  IP access violation accounting is disabled
  TCP/IP header compression is disabled
  RTP/IP header compression is disabled
  Policy routing is disabled
  Network address translation is disabled
  BGP Policy Mapping is disabled
  Input features: MCI Check
  Output features: Access List
  IPv4 WCCP Redirect outbound is disabled
  IPv4 WCCP Redirect inbound is disabled
  IPv4 WCCP Redirect exclude is disabled
```

## 3.2 Konfiguracja i weryfikacja standardowych nazywanych list ACL.

Bazując na polityce bezpieczeństwa rekomendowanej przez Cisco, na którym routerze ustawisz tę listę ACL?Wynik zapisz w pliku tekstowym
```
number 3
```

### Extended Ping R3:G0/1 -> PC-A
```
R3#ping
Protocol [ip]:
Target IP address: 192.168.10.3
Repeat count [5]:
Datagram size [100]:
Timeout in seconds [2]:
Extended commands [n]: y
Ingress ping [n]:
Source address or interface: 192.168.30.1
DSCP Value [0]:
Type of service [0]:
Set DF bit in IP header? [no]:
Validate reply data? [no]:
Data pattern [0x0000ABCD]:
Loose, Strict, Record, Timestamp, Verbose[none]:
Sweep range of sizes [n]:
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.10.3, timeout is 2 seconds:
Packet sent with a source address of 192.168.30.1
U.U.U
Success rate is 0 percent (0/5)
```

### R3:loopback0 -> PC-A
```
R3#ping
Protocol [ip]:
Target IP address: 192.168.10.3
Repeat count [5]:
Datagram size [100]:
Timeout in seconds [2]:
Extended commands [n]: y
Ingress ping [n]:
Source address or interface: 192.168.40.1
DSCP Value [0]:
Type of service [0]:
Set DF bit in IP header? [no]:
Validate reply data? [no]:
Data pattern [0x0000ABCD]:
Loose, Strict, Record, Timestamp, Verbose[none]:
Sweep range of sizes [n]:
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.10.3, timeout is 2 seconds:
Packet sent with a source address of 192.168.40.1
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 28/28/32 ms
```
