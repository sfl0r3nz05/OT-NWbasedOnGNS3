# vIOS-Core-I & II Configuration

![image](https://user-images.githubusercontent.com/69375071/210247015-b6359b9b-2b75-4bc6-a59f-ff6dd0b90518.png)

## vIOS-Core-I

- vIOSL2 console is a bit verbose.
- No need to login. No username and no password by default.

> After configuration and logout, username becomes `admin`, password becomes `cisco`

- Use the following configuration for `vIOS-Core-I`.

```
service password-encryption
!
hostname vIOS-Core-I
!
enable secret 5 $1$78b3$xtQa1A6wFCybA2fbZZWeU.
!
username admin privilege 15 secret 5 $1$SUUR$R.rWrThT1MWlk/GocKXzc0
aaa new-model
! 
aaa authentication login default group radius local
aaa authentication enable default group radius enable
aaa authorization console
aaa authorization exec default group radius local 
!
aaa session-id common
clock timezone UTC+2 2 0
!
ip domain-name companyXYZ.sk
ip name-server 172.16.50.1
!
ip ssh version 2
!
interface Loopback0
 ip address 10.1.1.1 255.255.255.255
 ip ospf message-digest-key 1 md5 7 14543F123C05393865786061
!
interface GigabitEthernet0/2
 description Link to vEOS-Dis-I
 no switchport
 ip address 10.0.0.10 255.255.255.252
 ip ospf message-digest-key 1 md5 7 03477612360E325F0F594A51
 ip ospf network point-to-point
!
interface GigabitEthernet0/1
 description Link to vEOS-Dis-II
 no switchport
 ip address 10.0.0.18 255.255.255.252
 ip ospf message-digest-key 1 md5 7 01502B1D6B0A151C601C1D5D
 ip ospf network point-to-point
!
interface GigabitEthernet0/0
 description Link to vIOS-Core-II     
 no switchport
 ip address 10.0.0.5 255.255.255.252
 ip ospf message-digest-key 1 md5 7 15512615342B383769636676
 ip ospf network point-to-point
!
interface GigabitEthernet0/3
 description Link to ASAv-I
 no switchport
 ip address 172.16.0.10 255.255.255.252
 ip ospf message-digest-key 1 md5 7 05482B16114D5D1A58554446
!
interface GigabitEthernet1/0
 description Unused
 shutdown
 no lldp transmit
 no lldp receive
!
interface GigabitEthernet1/1
 description Unused
 shutdown
 no lldp transmit
 no lldp receive
!
interface GigabitEthernet1/2
 description Unused
 shutdown
 no lldp transmit
 no lldp receive
!
interface GigabitEthernet1/3
 description Unused
 shutdown
 no lldp transmit
 no lldp receive
!
router ospf 1
 router-id 10.1.1.1
 area 0 authentication message-digest
 network 10.0.0.4 0.0.0.3 area 0
 network 10.0.0.8 0.0.0.3 area 0
 network 10.0.0.16 0.0.0.3 area 0
 network 10.1.1.1 0.0.0.0 area 0
 network 172.16.0.8 0.0.0.3 area 0
!
ip radius source-interface Loopback0 
logging trap notifications
logging source-interface Loopback0
logging host 172.16.50.1
!
radius server Server1
 address ipv4 172.16.50.1 auth-port 1812 acct-port 1813
 key 7 021201481F575D72
!
line vty 5 15
!
ntp source Loopback0
ntp server 172.16.50.1
!
end
!
```

## vIOS-Core-II

- Use the following configuration for `vIOS-Core-II`.

```
service password-encryption
!
hostname vIOS-Core-II
!
enable secret 5 $1$1ax8$sXGEbBRMnge31TUGAk25m0
!
username admin privilege 15 secret 5 $1$KX6y$zl0772CLMCexHYo6ioepW/
aaa new-model
!       
aaa authentication login default group radius local
aaa authentication enable default group radius enable
aaa authorization console
aaa authorization exec default group radius local 
!
aaa session-id common
clock timezone UTC+2 2 0
!
ip domain-name companyXYZ.sk
ip name-server 172.16.50.1
!
lldp run
!
ip ssh version 2
!
interface Loopback0
 ip address 10.1.1.2 255.255.255.255
 ip ospf message-digest-key 1 md5 7 114A341C2713181F457A7870
!
interface GigabitEthernet0/2
 description description Link to vEOS-Dis-II
 no switchport
 ip address 10.0.0.14 255.255.255.252
 ip ospf message-digest-key 1 md5 7 05482B16114D5D1A58554446
 ip ospf network point-to-point
!
interface GigabitEthernet0/1
 description description Link to vEOS-Dis-I
 no switchport
 ip address 10.0.0.22 255.255.255.252
 ip ospf message-digest-key 1 md5 7 0862615739181604535B5F50
 ip ospf network point-to-point
!
interface GigabitEthernet0/0
 description Link to vIOS-Core-I
 no switchport
 ip address 10.0.0.6 255.255.255.252
 ip ospf message-digest-key 1 md5 7 100D2400351601184D54797F
 ip ospf network point-to-point
!
interface GigabitEthernet0/3
 description Link to ASAv-I
 no switchport
 ip address 172.16.0.14 255.255.255.252
 ip ospf message-digest-key 1 md5 7 01502B1D6B0A151C601C1D5D
!
interface GigabitEthernet1/0
 description Unused
 shutdown
 no lldp transmit
 no lldp receive
!
interface GigabitEthernet1/1
 description Unused
 shutdown
 no lldp transmit
 no lldp receive
!
interface GigabitEthernet1/2
 description Unused
 shutdown
 no lldp transmit
 no lldp receive
!
interface GigabitEthernet1/3
 description Unused
 shutdown
 no lldp transmit
 no lldp receive
!
router ospf 1
 router-id 10.1.1.2
 area 0 authentication message-digest
 network 10.0.0.4 0.0.0.3 area 0
 network 10.0.0.12 0.0.0.3 area 0
 network 10.0.0.20 0.0.0.3 area 0
 network 10.1.1.2 0.0.0.0 area 0
 network 172.16.0.12 0.0.0.3 area 0
!
ip radius source-interface Loopback0 
logging trap notifications
logging source-interface Loopback0
logging host 172.16.50.1
!
radius server Server1
 address ipv4 172.16.50.1 auth-port 1812 acct-port 1813
 key 7 111D1C160343595F
!
line vty 5 15
!
ntp source Loopback0
ntp server 172.16.50.1
!
end
!
```
