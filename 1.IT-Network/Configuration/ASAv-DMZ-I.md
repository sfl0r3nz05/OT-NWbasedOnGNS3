# ASAv-DMZ-I Configuration

![image](/img/12.png)

- ASAv will reboot on the first start, which is normal.
- No need to login. No username and no password by default. When prompted by password, just press enter.
- Need to choose whether to enable anonymous error reporting on entering terminal config mode for the first time.

> After configuration and logout, username becomes `admin`, password becomes `cisco`

- Use the following configuration for `ASAv-DMZ-I`.

```
hostname ASAv-DMZ-I
enable password 2KFQnbNIdI.2KYOU encrypted
!
interface GigabitEthernet0/0
 no shutdown
 description Link to vIOS-EDGE-I
 nameif OUTSIDE
 security-level 0
 ip address 195.1.1.130 255.255.255.252 
!
interface GigabitEthernet0/1
 no shutdown
 description Link to vIOS-DMZ-I
 nameif INSIDE
 security-level 100
 ip address 195.1.1.133 255.255.255.252 
!
clock timezone UTC+2 2
dns domain-lookup INSIDE
dns server-group DefaultDNS
 name-server 195.1.1.161 
object network serv-dmz-i
 host 195.1.1.161
object network public_add
 subnet 195.1.1.0 255.255.255.0
object network google_dns1
 host 8.8.8.8
object network google_dns2
 host 8.8.4.4
object network vios-edge-i_gi0_0
 host 195.1.1.129
object-group network google_dns
 network-object object google_dns1
 network-object object google_dns2
access-list out-to-ins extended permit tcp object public_add object public_add eq ssh 
access-list out-to-ins extended permit icmp object public_add object public_add echo 
access-list out-to-ins extended permit tcp any object serv-dmz-i range www https 
access-list out-to-ins extended permit icmp object-group google_dns object public_add echo-reply 
access-list out-to-ins extended permit udp object vios-edge-i_gi0_0 object serv-dmz-i eq domain 
logging enable
logging console informational
logging monitor informational
logging buffered informational
logging trap notifications
logging host INSIDE 195.1.1.161
mtu OUTSIDE 1500
mtu INSIDE 1500
no monitor-interface service-module
access-group out-to-ins in interface OUTSIDE
route OUTSIDE 0.0.0.0 0.0.0.0 195.1.1.129 1
route INSIDE 195.1.1.160 255.255.255.224 195.1.1.134 1
route INSIDE 195.1.1.192 255.255.255.192 195.1.1.134 1
aaa authentication ssh console LOCAL
aaa authentication serial console LOCAL
ssh 195.1.1.0 255.255.255.128 OUTSIDE
ssh version 2 
ssh cipher encryption high
ssh key-exchange group dh-group14-sha1
ntp server 195.1.1.161
username admin password f3UhLvUj1QsXsuK7 encrypted
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
