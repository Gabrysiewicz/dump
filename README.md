## Part 2

**Routing table R3**
```
      10.0.0.0/8 is variably subnetted, 3 subnets, 2 masks
O        10.1.1.0/30 [110/128] via 10.2.2.2, 00:00:49, Serial0/0/1
C        10.2.2.0/30 is directly connected, Serial0/0/1
L        10.2.2.1/32 is directly connected, Serial0/0/1
O     192.168.10.0/24 [110/129] via 10.2.2.2, 00:00:49, Serial0/0/1
      192.168.20.0/32 is subnetted, 1 subnets
O        192.168.20.1 [110/129] via 10.2.2.2, 00:00:49, Serial0/0/1
      192.168.30.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.30.0/24 is directly connected, GigabitEthernet0/1
L        192.168.30.1/32 is directly connected, GigabitEthernet0/1
      192.168.40.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.40.0/24 is directly connected, Loopback0
L        192.168.40.1/32 is directly connected, Loopback0
      209.165.200.0/32 is subnetted, 1 subnets
O        209.165.200.225 [110/65] via 10.2.2.2, 00:00:39, Serial0/0/1
      209.165.201.0/32 is subnetted, 1 subnets
O        209.165.201.1 [110/65] via 10.2.2.2, 00:00:39, Serial0/0/1

```

**Z komputera PC-C, wyślij ping do PC-A i interfejsu loopback oraz interfejsu szeregowego na R1.Czy ping zakończył się sukcesem?**
```
C:\Users\student>ping 192.168.10.3

Pinging 192.168.10.3 with 32 bytes of data:
Reply from 192.168.10.3: bytes=32 time=18ms TTL=125
Reply from 192.168.10.3: bytes=32 time=19ms TTL=125
Reply from 192.168.10.3: bytes=32 time=18ms TTL=125
Reply from 192.168.10.3: bytes=32 time=19ms TTL=125

Ping statistics for 192.168.10.3:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 18ms, Maximum = 19ms, Average = 18ms
```

**Z R3, wyślij ping do PC-A i interfejsu loopback oraz interfejsu szeregowego na R1.Czy ping zakończył się sukcesem?**
```
R3#ping 192.168.10.3
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.10.3, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 28/28/32 ms
```

**Z PC-C, wyślij ping do interfejsu loopback na routerze ISP. Czy ping zakończył się sukcesem?**
```
C:\Users\student>ping 209.165.200.225

Pinging 209.165.200.225 with 32 bytes of data:
Reply from 209.165.200.225: bytes=32 time=9ms TTL=254
Reply from 209.165.200.225: bytes=32 time=9ms TTL=254
Reply from 209.165.200.225: bytes=32 time=9ms TTL=254
Reply from 209.165.200.225: bytes=32 time=9ms TTL=254

Ping statistics for 209.165.200.225:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 9ms, Maximum = 9ms, Average = 9ms
```
```
C:\Users\student>ping 209.165.201.1

Pinging 209.165.201.1 with 32 bytes of data:
Reply from 209.165.201.1: bytes=32 time=9ms TTL=254
Reply from 209.165.201.1: bytes=32 time=9ms TTL=254
Reply from 209.165.201.1: bytes=32 time=9ms TTL=254
Reply from 209.165.201.1: bytes=32 time=9ms TTL=254

Ping statistics for 209.165.201.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 9ms, Maximum = 9ms, Average = 9ms
```
**Otwórz  przeglądarkę  na  komputerze  PC-C  i  przejdź  do  strony http://10.1.1.1na  R1.  Zostaniesz poproszony do podania nazwy użytkownika i hasła. Użyj admin jako nazwy użytkownika i classjako hasła. Jeśli  zostaniesz  zachęcony  do  zaakceptowania certyfikatu,  zaakceptuj go. Router  załaduje Cisco  Configuration  Professional  (CCP)  Express  w  oddzielnym  oknie.  Możesz  być  wezwany  do podania nazwy użytkownika i hasła. Użyj admin jako nazwy użytkownika i classjako hasła.**
<img src="https://github.com/Gabrysiewicz/S8_Bezpieczenstwo-w-sieciach/blob/main/lab9_login.png" />


```
R3#show access-lists
Extended IP access list WWW-POLICY
    10 permit tcp 192.168.30.0 0.0.0.255 host 10.1.1.1 eq www (10 matches)
    20 permit tcp 192.168.30.0 0.0.0.255 209.165.200.224 0.0.0.31 eq www (29 matches)
    30 permit ip 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255
```

## PART 3
**Jak, jeśli jest, nazywa się ACL?**
```
  Outgoing access list is WWW-POLICY
```
**W jakim kierunku została zastosowana lista ACL?** 
```
 Output features: Access List
 Kierunek: Out
```
**Ile linii zawiera ta lista dostępu?**
```
2 linie
```

**Otwórz przeglądarkę internetową na PC-C i  wejdź na stronę  http://209.165.200.225( ISP router). Dostęp powinien być możliwy, Jeśli nie, rozwiąż problemy.**
<img src="https://github.com/Gabrysiewicz/S8_Bezpieczenstwo-w-sieciach/blob/main/lab9_login_ISP.png" />

**Z PC-C, otwórz sesję WWW do  http://10.1.1.1(R1). Dostęp powinien być możliwy, Jeśli nie, rozwiążproblemy**
<img src="https://github.com/Gabrysiewicz/S8_Bezpieczenstwo-w-sieciach/blob/main/lab9_login_R1.png" />

**Z PC-C, otwórz sesję WWW do  http://209.165.201.1(ISP router). Dostęp powinien być niemożliwy. Jeśli nie, rozwiąż problemy.**
<img src="https://github.com/Gabrysiewicz/S8_Bezpieczenstwo-w-sieciach/blob/main/lab9_login_ISP_v2.png" />


**Z linii komend  PC-C, wykonaj ping do PC-A. Zapisz jaki jest rezultat i dlaczego?**
Zapewne wynika to z blokowanego `ping` przez `ACL` na `R1`
```
Pinging 192.168.10.3 with 32 bytes of data:
Reply from 192.168.30.1: Destination net unreachable.
Reply from 192.168.30.1: Destination net unreachable.
Reply from 192.168.30.1: Destination net unreachable.
Reply from 192.168.30.1: Destination net unreachable.

Ping statistics for 192.168.10.3:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

### Part 4

**Ile linii zawiera ta lista dostępu?**
A: 2
```
Extended IP access list WWW-POLICY
    10 permit tcp 192.168.30.0 0.0.0.255 host 10.1.1.1 eq www (10 matches)
    20 permit tcp 192.168.30.0 0.0.0.255 209.165.200.224 0.0.0.31 eq www (29 matches)
```

#### Z PC-C, wykonaj pinguj na adres IP komputera PC-A.
```
C:\Users\student>ping 192.168.10.3

Pinging 192.168.10.3 with 32 bytes of data:
Reply from 192.168.10.3: bytes=32 time=18ms TTL=125
Reply from 192.168.10.3: bytes=32 time=19ms TTL=125
Reply from 192.168.10.3: bytes=32 time=19ms TTL=125
Reply from 192.168.10.3: bytes=32 time=18ms TTL=125

Ping statistics for 192.168.10.3:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 18ms, Maximum = 19ms, Average = 18ms
```

