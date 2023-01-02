# vIOS-Edge-I Configuration

![image](/img/10.png)

- No need to login. No username and no password by default.

> After configuration and logout, username becomes `admin`, password becomes `cisco`

- Use the following configuration for `vIOS-Edge-I`.

```
hostname vIOS-EDGE-I
!
enable secret 5 $1$G3j8$h06fjiGZVnG4FGl8jSV/m1
!      
clock timezone mytimez 2 0
!
ip domain name companyXYZ.sk
ip name-server 195.1.1.161
!
username admin secret 5 $1$Otka$Cuzz6Lis374vv3OJ33mOy1
!
interface Loopback0
 ip address 10.1.1.5 255.255.255.255
!
interface GigabitEthernet0/0
 no shutdown
 description Link to ASA-DMZ-I
 ip address 195.1.1.129 255.255.255.252
 ip nat outside
 ip virtual-reassembly in
!
interface GigabitEthernet0/1
 no shutdown
 description Link to ISP1
 ip address 198.10.10.2 255.255.255.252
 ip nat outside
 ip virtual-reassembly in
 duplex full
!
interface GigabitEthernet0/2
 no shutdown
 description Link to ASAv-I
 ip address 172.16.0.2 255.255.255.252
 ip nat inside
 ip virtual-reassembly in
!
interface GigabitEthernet0/3
 no shutdown
 description Link to ISP2
 ip address 197.10.10.2 255.255.255.252
 ip nat outside
 ip virtual-reassembly in
 duplex full
!
router bgp 64500
 bgp log-neighbor-changes
 network 195.1.1.0
 neighbor isp-group peer-group
 neighbor isp-group ttl-security hops 1
 neighbor isp-group filter-list 10 out
 neighbor 197.10.10.1 remote-as 64502
 neighbor 197.10.10.1 peer-group isp-group
 neighbor 197.10.10.1 password isp2md5pass
 neighbor 198.10.10.1 remote-as 64501
 neighbor 198.10.10.1 peer-group isp-group
 neighbor 198.10.10.1 password isp1md5pass
 neighbor 198.10.10.1 route-map setlocalin in
!
ip as-path access-list 10 permit ^$
!
ip nat pool 1 195.1.1.1 195.1.1.127 netmask 255.255.255.128
ip nat inside source list 1 pool 1 overload
ip route 10.0.0.0 255.0.0.0 172.16.0.1
ip route 172.16.0.0 255.255.0.0 172.16.0.1
ip route 192.168.0.0 255.255.192.0 172.16.0.1
ip route 195.1.1.0 255.255.255.0 Null0
ip route 195.1.1.128 255.255.255.128 195.1.1.130
ip ssh version 2
!
ip access-list standard ssh-access
 permit 192.168.40.0 0.0.0.255
 deny   any
!
logging trap notifications
logging source-interface Loopback0
logging host 172.16.50.1
!
route-map setlocalin permit 10
 set local-preference 150
!
access-list 1 permit 192.168.10.0 0.0.0.255
access-list 1 permit 192.168.20.0 0.0.0.255
access-list 1 permit 192.168.30.0 0.0.0.255
access-list 1 permit 192.168.40.0 0.0.0.255
access-list 1 permit 10.0.0.0 0.0.0.255
access-list 1 permit 10.1.1.0 0.0.0.255
access-list 1 permit 172.16.0.0 0.0.0.255
access-list 1 permit 172.16.50.0 0.0.0.255
access-list 1 deny   any
!
line con 0
 login local
line vty 0 4
 access-class ssh-access in
 login local
 transport input ssh
line vty 5 924
 access-class ssh-access in
 login local
 transport input ssh
!
ntp source Loopback0
ntp server 172.16.50.1
!
end
!
```
