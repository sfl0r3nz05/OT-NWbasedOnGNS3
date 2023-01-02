# vIOS-Ser-I Configuration

![image](/img/9.png)

- vIOSL2 console is a bit verbose.
- No need to login. No username and no password by default.

> After configuration and logout, username becomes `admin`, password becomes `cisco`

- Use the following configuration for `vIOS-Ser-I`.

```
hostname vIOS-Ser-I
!
enable secret 5 $1$exdM$B0mb.myrmFM2UV2iT29.71
!
username admin privilege 15 secret 5 $1$TFKh$mWcFYm.aW6zma8.TC/hWl0
aaa new-model
!         
aaa authentication login default group radius local
aaa authentication enable default group radius enable
aaa authorization console
aaa authorization exec default group radius local 
!
aaa session-id common
clock timezone mytimez 2 0
!
ip domain-name companyXYZ.sk
ip name-server 172.16.50.1
!
ip ssh version 2
!
interface Loopback0
 ip address 10.1.1.4 255.255.255.255
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 #MyPass!034
!
interface Port-channel1
 switchport access vlan 50
 switchport mode access
!
interface GigabitEthernet0/2
 description Link to Server1
 switchport access vlan 50
 switchport mode access
 channel-group 1 mode on
!
interface GigabitEthernet0/3
 description Link2 to Server1
 switchport access vlan 50
 switchport mode access
 channel-group 1 mode on
!         
interface GigabitEthernet0/0
 description Link1 to ASAv-I 
 no switchport
 ip address 172.16.0.6 255.255.255.252
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 #MyPass!034
!
interface GigabitEthernet0/1
 description Link2 to ASAv-I
 no switchport
 ip address 172.16.0.18 255.255.255.252
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 #MyPass!034
!
interface Vlan50
 ip address 172.16.50.254 255.255.255.0
 ip ospf authentication message-digest
 ip ospf message-digest-key 1 md5 #MyPass!034
!
router ospf 1
 router-id 10.1.1.4
 passive-interface Vlan50
 network 10.1.1.4 0.0.0.0 area 0
 network 172.16.0.4 0.0.0.3 area 0
 network 172.16.0.16 0.0.0.3 area 0
 network 172.16.50.0 0.0.0.255 area 0
!
ip radius source-interface Loopback0 
logging trap notifications
logging source-interface Loopback0
logging host 172.16.50.1
!
radius server Server1
 address ipv4 172.16.50.1 auth-port 1812 acct-port 1813
 key test123
!
line con 0
 exec-timeout 0 0
line vty 5 1500
!
ntp source Loopback0
ntp server 172.16.50.1
!
end
!
```
