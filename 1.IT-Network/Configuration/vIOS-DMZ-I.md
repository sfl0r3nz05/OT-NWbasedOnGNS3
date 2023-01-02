# vIOS-DMZ-I Configuration

![image](https://user-images.githubusercontent.com/69375071/210247052-aa524a52-8186-49d4-963e-60ae35945b0a.png)

- vIOSL2 console is a bit verbose.
- No need to login. No username and no password by default.

> After configuration and logout, username becomes `admin`, password becomes `cisco`

- Use the following configuration for `vIOS-DMZ-I`.

```
hostname vIOS-DMZ-I
!
enable secret 5 $1$6DtG$twD5vtdTaNSxRT3eO39cz/
!
username admin secret 5 $1$az/O$NyIgazV2xiDIgrJB/xMKj.
clock timezone UTC+2 2 0
!
vtp mode off
!
ip domain-name companyXYZ.sk
ip name-server 195.1.1.161
!
vlan 10
 name Servers_DMZ
!
ip ssh version 2
!
interface GigabitEthernet0/1
 description Link to Serv-DMZ-I
 switchport access vlan 10
 switchport mode access
!
interface GigabitEthernet0/0
 description Link to ASAv-DMZ-I
 no switchport
 ip address 195.1.1.134 255.255.255.252
!
interface Vlan10
 ip address 195.1.1.166 255.255.255.248
!
ip route 0.0.0.0 0.0.0.0 195.1.1.133
!
ip access-list standard ssh-access
 permit 195.1.1.0 0.0.0.127
 deny   any
!
logging trap notifications
logging host 195.1.1.161
!
line con 0
 exec-timeout 0 0
 login local
line vty 0 4
 access-class ssh-access in
 login local
 transport input ssh
line vty 5 1500
 access-class ssh-access in
 login local
 transport input ssh
!
ntp server 195.1.1.161
!
end
!
```
