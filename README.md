```
Część 1: Konfiguracja urządzeń sieciowych
	•Wykonaj okablowanie sieci.
	•Skonfigurować nazwę, adresy IP i hasła dostępowe do przełącznika.
•Część 2: Konfigurowaniebezpiecznych portów trunk.
	•Skonfigurowaćporty trunk.
	•Zmodyfikować natywny VLAN.
	•Zweryfikować konfiguracje portów trunk.
	•Wyłączyć porty trunk.
•Część 3: Ochrona przed atakiem na protokół STP.
	•WłączyćPortFast iBPDU guard.
	•Zweryfikować iBPDU guard.
	•Włącz root guard.
	•Włącz loopguard.
•Część 4: Konfiguracja i weryfikacja zabezpieczania portów.
	•Konfiguracja i weryfikacja zabezpieczenia portów.
	•Wyłączyć nieużywane porty
	•Przenieść porty z domyślnego VLAN1 do alternatywnego VLAN
	•Konfiguracja na portach funkcji PVLAN Edge

#### PING PC-A ---> R1
C:\Users\student>ping 192.168.1.1

Pinging 192.168.1.1 with 32 bytes of data:
Reply from 192.168.1.1: bytes=32 time=10ms TTL=255
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255

Ping statistics for 192.168.1.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 10ms, Average = 2ms

#### Jaki jest priorytet przełacznika S1?
> 1 
#### Które porty sa w uzyciu I jaki jest ich status ?
> Fa0/1, Fa0/5, Fa0/6, Status Forward

S1#show interface trunk

Port        Mode             Encapsulation  Status        Native vlan
Fa0/1       on               802.1q         trunking      1

Port        Vlans allowed on trunk
Fa0/1       1-4094

Port        Vlans allowed and active in management domain
Fa0/1       1

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       1

*Mar  1 00:18:37.983: %SYS-5-CONFIG_I: Configured from console by console


Port        Mode             Encapsulation  Status        Native vlan
Fa0/1       on               802.1q         trunking      99

Port        Vlans allowed on trunk
Fa0/1       1-4094

Port        Vlans allowed and active in management domain
Fa0/1       1

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       1

Name: Fa0/1
Switchport: Enabled
Administrative Mode: trunk
Operational Mode: trunk
Administrative Trunking Encapsulation: dot1q
Operational Trunking Encapsulation: dot1q
Negotiation of Trunking: Off
Access Mode VLAN: 1 (default)

interface FastEthernet0/1
 switchport trunk native vlan 99
 switchport mode trunk
 switchport nonegotiate


 Port 6 (FastEthernet0/6) of VLAN0001 is designated forwarding
   Port path cost 19, Port priority 128, Port Identifier 128.6.
   Designated root has priority 1, address d0c7.89e2.4f00
   Designated bridge has priority 1, address d0c7.89e2.4f00
   Designated port id is 128.6, designated path cost 0
   Timers: message age 0, forward delay 0, hold 0
   Number of transitions to forwarding state: 1
>   The port is in the portfast mode     <
   Link type is point-to-point by default
>   Bpdu guard is enabled                <
   BPDU: sent 737, received 0

#### Zapisz w pliku tekstowym jaka jest wartość licznika naruszeń bezpieczeństw portuoraz jaki jest aktualnieadres #### MAC na porcie.
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Aging Time                 : 0 mins
Aging Type                 : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 1
Total MAC Addresses        : 1
Configured MAC Addresses   : 0
Sticky MAC Addresses       : 1
> Last Source Address:Vlan   : f872.eab1.d0d0:1
> Security Violation Count   : 0

#### PC-A ---> R1
Pinging 192.168.1.1 with 32 bytes of data:
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255

Ping statistics for 192.168.1.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

Pruning VLANs Enabled: 2-1001
Capture Mode Disabled
Capture VLANs Allowed: ALL

Protected: true
Unknown unicast blocked: disabled
Unknown multicast blocked: disabled
Appliance trust: none


#### PINGI
## PC-A ---> R1
C:\Users\student>ping 192.168.1.1

Pinging 192.168.1.1 with 32 bytes of data:
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255
Reply from 192.168.1.1: bytes=32 time<1ms TTL=255

Ping statistics for 192.168.1.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

## PC-A ---> S1
C:\Users\student>ping 192.168.1.2

Pinging 192.168.1.2 with 32 bytes of data:
Reply from 192.168.1.10: Destination host unreachable.
Request timed out.
Request timed out.

Ping statistics for 192.168.1.2:
    Packets: Sent = 3, Received = 1, Lost = 2 (66% loss),
Control-C
^C

## PC-A ---> S2
C:\Users\student>ping 192.168.1.3

Pinging 192.168.1.3 with 32 bytes of data:
Reply from 192.168.1.10: Destination host unreachable.

Ping statistics for 192.168.1.3:
    Packets: Sent = 1, Received = 1, Lost = 0 (0% loss),
Control-C
^C

## PC-A ---> PC-B
C:\Users\student>ping 192.168.1.11

Pinging 192.168.1.11 with 32 bytes of data:
Reply from 192.168.1.11: bytes=32 time=1ms TTL=128
Reply from 192.168.1.11: bytes=32 time=1ms TTL=128
Reply from 192.168.1.11: bytes=32 time=1ms TTL=128

Ping statistics for 192.168.1.11:
    Packets: Sent = 3, Received = 3, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 1ms, Maximum = 1ms, Average = 1ms
Control-C

Building configuration...

Current configuration : 2386 bytes
!
! Last configuration change at 01:11:55 UTC Mon Mar 1 1993
!
version 15.0
no service pad
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname S1
!
boot-start-marker
boot-end-marker
!
enable secret 9 $9$s.xyicK2vjGVS5$wYc/ABhBXaaablr2z8QBXK1fZ7nTa5.LS2dPzgjvBY2
!
no aaa new-model
system mtu routing 1500
!
!
no ip domain-lookup
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
spanning-tree vlan 1 priority 0
!
vlan internal allocation policy ascending
!
!
!
!
!
!
interface FastEthernet0/1
 switchport trunk native vlan 99
 switchport mode trunk
 switchport nonegotiate
!
interface FastEthernet0/2
 shutdown
!
interface FastEthernet0/3
 shutdown
!
interface FastEthernet0/4
 shutdown
!
interface FastEthernet0/5
 switchport mode access
 switchport port-security mac-address sticky
 switchport port-security mac-address sticky f872.eab1.d0d0
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/6
 switchport access vlan 20
 switchport mode access
 switchport protected
 switchport port-security maximum 3
 switchport port-security mac-address sticky
 switchport port-security mac-address sticky 68e4.3b30.a061
 switchport port-security aging time 120
 spanning-tree portfast
 spanning-tree bpduguard enable
!
interface FastEthernet0/7
 switchport protected
!
interface FastEthernet0/8
 shutdown
!
interface FastEthernet0/9
 shutdown
!
interface FastEthernet0/10
 shutdown
!
interface FastEthernet0/11
 shutdown
!
interface FastEthernet0/12
 shutdown
!
interface FastEthernet0/13
 shutdown
!
interface FastEthernet0/14
 shutdown
!
interface FastEthernet0/15
 shutdown
!
interface FastEthernet0/16
 shutdown
!
interface FastEthernet0/17
 shutdown
!
interface FastEthernet0/18
 shutdown
!
interface FastEthernet0/19
 shutdown
!
interface FastEthernet0/20
 shutdown
!
interface FastEthernet0/21
 shutdown
!
interface FastEthernet0/22
 shutdown
!
interface FastEthernet0/23
 shutdown
!
interface FastEthernet0/24
 shutdown
!
interface GigabitEthernet0/1
 shutdown
!
interface GigabitEthernet0/2
 shutdown
!
interface Vlan1
 ip address 192.168.1.2 255.255.255.0
!
ip default-gateway 192.168.1.1
no ip http server
no ip http secure-server
!
vstack
!
line con 0
 exec-timeout 5 0
 password pollub
 logging synchronous
 login
line vty 0 4
 login
line vty 5 15
 login
!
end
```
