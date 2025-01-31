# VPN_Cisco

## R1

```bash

interface Tunnel0
 ip address 192.168.3.1 255.255.255.252
 mtu 1476
 tunnel source Serial0/1/0
 tunnel destination 198.133.219.2

interface GigabitEthernet0/0
 ip address 192.168.1.254 255.255.255.0
 duplex auto
 speed auto

interface GigabitEthernet0/1
 no ip address
 duplex auto
 speed auto
 shutdown

interface Serial0/1/0
 ip address 209.165.201.1 255.255.255.0

interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown

interface Vlan1
 no ip address
 shutdown

router ospf 1
 router-id 1.1.1.1
 log-adjacency-changes
 network 192.168.1.0 0.0.0.255 area 0
 network 209.165.201.0 0.0.0.255 area 0
 network 192.168.3.0 0.0.0.3 area 0

ip classless
ip route 192.168.2.0 255.255.255.0 192.168.3.2 

```

## R2 

```bash

interface Tunnel0
 ip address 192.168.3.2 255.255.255.252
 mtu 1476
 tunnel source Serial0/1/0
 tunnel destination 209.165.201.1
!
!
interface GigabitEthernet0/0
 ip address 192.168.2.254 255.255.255.0
 duplex auto
 speed auto
!
interface GigabitEthernet0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/1/0
 ip address 198.133.219.2 255.255.255.0
 clock rate 2000000
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
router ospf 1
 router-id 2.2.2.2
 log-adjacency-changes
 network 198.133.219.0 0.0.0.255 area 0
 network 192.168.2.0 0.0.0.255 area 0
 network 192.168.3.0 0.0.0.3 area 0
!
ip route 192.168.1.0 255.255.255.0 192.168.3.1 
```
