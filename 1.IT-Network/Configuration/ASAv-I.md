# ASAv-I Configuration

![image](https://user-images.githubusercontent.com/69375071/210246415-962006be-4427-41ac-a280-51395ebde498.png)

- ASAv will reboot on the first start, which is normal.
- No need to login. No username and no password by default. When prompted by password, just press enter.
- Need to choose whether to enable anonymous error reporting on entering terminal config mode for the first time.

> After configuration and logout, username becomes `admin`, password becomes `cisco`

- Use the following configuration for `ASAv-I`.

```
hostname ASAv-I
enable password 2KFQnbNIdI.2KYOU encrypted
zone inside_zone
zone server_zone
!
interface GigabitEthernet0/0
 no shutdown
 description Link to vIOS-Core-II
 nameif INSIDE0
 security-level 100
 zone-member inside_zone
 ip address 172.16.0.13 255.255.255.252 
 ospf message-digest-key 1 md5 #MyPass!034
 ospf authentication message-digest
!
interface GigabitEthernet0/1
 no shutdown
 description Link to vIOS-Core-I
 nameif INSIDE1
 security-level 100
 zone-member inside_zone
 ip address 172.16.0.9 255.255.255.252 
 ospf message-digest-key 1 md5 #MyPass!034
 ospf authentication message-digest
!
interface GigabitEthernet0/2
 no shutdown
 description Link to vIOS-L3-I
 nameif OUTSIDE
 security-level 0
 ip address 172.16.0.1 255.255.255.252 
!
interface GigabitEthernet0/3
 no shutdown
 description Link1 to vIOS-Ser-I
 nameif SERVER0
 security-level 50
 zone-member server_zone
 ip address 172.16.0.5 255.255.255.252 
 ospf message-digest-key 1 md5 #MyPass!034
 ospf authentication message-digest
!
interface GigabitEthernet0/4
 no shutdown
 description Link2 to vIOS-Ser-I
 nameif SERVER1
 security-level 50
 zone-member server_zone
 ip address 172.16.0.17 255.255.255.252 
 ospf message-digest-key 1 md5 #MyPass!034
 ospf authentication message-digest
!
clock timezone UTC+2 2
object network vlan30_192.168.30
 subnet 192.168.30.0 255.255.255.0
object network vlan10_192.168.10
 subnet 192.168.10.0 255.255.255.0
object network vlan20_192.168.20
 subnet 192.168.20.0 255.255.255.0
object network vlan40_192.168.40
 subnet 192.168.40.0 255.255.255.0
object network vlan50_172.16.50
 subnet 172.16.50.0 255.255.255.0
object network server1
 host 172.16.50.1
object network vios-l3
 host 10.1.1.5
object network loopbacks
 subnet 10.1.1.0 255.255.255.0
object network google_dns1
 host 8.8.8.8
object network google_dns2
 host 8.8.4.4
object-group network mgmt
 network-object object vlan40_192.168.40
object-group network end_vlans
 network-object object vlan10_192.168.10
 network-object object vlan20_192.168.20
 network-object object vlan30_192.168.30
 network-object object vlan40_192.168.40
object-group network server_vlans_all
 description All server VLANs
 network-object object vlan50_172.16.50
object-group network google_dns
 network-object object google_dns1
 network-object object google_dns2
object-group service server1_tcp_out tcp
 port-object eq www
 port-object eq https
 port-object eq domain
object-group service server1_udp_out udp
 port-object eq ntp
 port-object eq domain
access-list out-to-ins extended permit icmp object-group google_dns object-group end_vlans echo-reply 
access-list out-to-ins extended permit icmp any object-group mgmt echo-reply 
access-list out-to-ins extended permit icmp any object loopbacks echo-reply 
access-list out-to-ins extended permit udp object-group google_dns object server1 eq domain 
access-list out-to-ins extended permit icmp any object vlan50_172.16.50 echo-reply 
access-list out-to-ins extended permit udp object vios-l3 object server1 eq ntp 
access-list out-to-ins extended permit udp object vios-l3 object server1 eq syslog 
access-list dc-to-ins_out extended permit tcp object vlan50_172.16.50 any object-group server1_tcp_out 
access-list dc-to-ins_out extended permit udp object vlan50_172.16.50 any object-group server1_udp_out 
access-list dc-to-ins_out extended permit icmp object vlan50_172.16.50 object-group google_dns echo 
access-list dc-to-ins_out extended permit icmp object vlan50_172.16.50 object vlan40_192.168.40 echo-reply 
logging enable
logging console informational
logging monitor informational
logging buffered informational
logging trap notifications
logging host SERVER0 172.16.50.1
mtu INSIDE0 1500
mtu INSIDE1 1500
mtu OUTSIDE 1500
mtu SERVER0 1500
mtu SERVER1 1500                         
no monitor-interface service-module
!
icmp permit 192.168.40.0 255.255.255.0 INSIDE0
icmp permit 10.1.1.0 255.255.255.0 INSIDE0
icmp permit 192.168.40.0 255.255.255.0 INSIDE1
icmp permit 10.1.1.0 255.255.255.0 INSIDE1
icmp permit 172.16.50.0 255.255.255.0 SERVER0
icmp permit 172.16.50.0 255.255.255.0 SERVER1
access-group out-to-ins in interface OUTSIDE
access-group dc-to-ins_out in interface SERVER0
access-group dc-to-ins_out in interface SERVER1
router ospf 1
 router-id 10.1.1.3
 network 172.16.0.4 255.255.255.252 area 0
 network 172.16.0.8 255.255.255.252 area 0
 network 172.16.0.12 255.255.255.252 area 0
 network 172.16.0.16 255.255.255.252 area 0
 log-adj-changes
 default-information originate
!
route OUTSIDE 0.0.0.0 0.0.0.0 172.16.0.2 1
aaa-server Server1 protocol radius
aaa-server Server1 (SERVER0) host 172.16.50.1
 key test123
 authentication-port 1812
 accounting-port 1813
aaa authentication ssh console Server1 LOCAL
aaa authentication enable console Server1 LOCAL
aaa authentication serial console Server1 LOCAL
!
ssh 192.168.40.0 255.255.255.0 INSIDE0
ssh 172.16.0.14 255.255.255.255 INSIDE0
ssh 192.168.40.0 255.255.255.0 INSIDE1
ssh timeout 60
console timeout 0
ntp server 172.16.50.1
username admin password f3UhLvUj1QsXsuK7 encrypted privilege 15
!
policy-map type inspect http http_map
 parameters
  protocol-violation action drop-connection log
policy-map type inspect dns migrated_dns_map_1
 parameters
  message-length maximum client auto
  message-length maximum 512
policy-map global_policy
 class inspection_default
  inspect http http_map 
!
no call-home reporting anonymous
end
!
```
