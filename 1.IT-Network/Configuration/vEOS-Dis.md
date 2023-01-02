# vEOS-Dis-I & II Configuration

![image](/img/6.png)

## vEOS-Dis-I

- The configuration process is similar to `OpenSwitch-Acc-I`. The differences are addressed below.
- Be patient that initialization of vEOS is much longer than OpenSwitch.
- Login with username `admin`, no password.
- Copy running-config to startup-config using a shorter command.

```
wr
```

> After configuration and logout, username remains `admin`, password becomes `cisco`

- Use the following configuration for `vEOS-Dis-I`.

```
logging trap notifications
logging host 172.16.50.1
logging source-interface Loopback0
!
hostname vEOS-Dis-I
ip name-server vrf default 172.16.50.1
!
ntp source Loopback0
ntp server 172.16.50.1
!
radius-server key 7 071B245F5A584B56
radius-server host 172.16.50.1
!
aaa authentication login default group radius local
aaa authentication enable default group radius local
aaa authorization console
aaa authorization exec default group radius local
!
enable secret sha512 $6$CacB44/JpcUZ0AQo$wo1GhoDSRSonKbUjRNa9Nb6/p4WXH9K0M2rRozzudd77VFIaOLvrch3lRDUV/sslHg8yUzBo2Pkv2d8.EmWhQ.
!
username admin privilege 15 role network-admin secret sha512 $6$DYjKa2m1a4SmsTLt$ZBUvPOayYeM2HpmGX6nebngi1IwTybGAoGOiJJlNYF1ti7mWR5Hb0N8iXA0DioJsBhpQjSZHSRsp/b1e0QIKq/
!
clock timezone Europe/Bratislava
!
vlan 10,20,30,40
!
interface Ethernet1
   description Link to vIOS-Core-II
   no switchport
   ip address 10.0.0.21/30
   ip ospf network point-to-point
   ip ospf authentication message-digest
   ip ospf message-digest-key 1 md5 7 bS8fz/oIV8WdkUoexvixrA==
!
interface Ethernet2
   description Link to vIOS-Core-I
   no switchport
   ip address 10.0.0.9/30
   ip ospf network point-to-point
   ip ospf authentication message-digest
   ip ospf message-digest-key 1 md5 7 n+Pkjf+gomK+msssg0WWXA==
!
interface Ethernet3
   description Link to vEOS-Dis-II
   no switchport
   ip address 10.0.0.1/30
   ip ospf network point-to-point
   ip ospf authentication message-digest
   ip ospf message-digest-key 1 md5 7 n+Pkjf+gomK+msssg0WWXA==
!
interface Ethernet4
   description Link to OpenSwitch-Acc-I
   switchport trunk allowed vlan 10,20
   switchport mode trunk
!
interface Ethernet5
   description Link to OpenSwitch-Acc-II
   switchport trunk allowed vlan 30,40
   switchport mode trunk
!
interface Ethernet6
   description Link to Management OpenSwitch-Acc-I
   no switchport
   ip address 10.1.1.10/30
!
interface Ethernet7
   description Unused
   shutdown
   no lldp transmit
   no lldp receive
!
interface Loopback0
   ip address 10.1.1.6/32
!
interface Vlan10
   ip address 192.168.10.253/24
   ip helper-address 172.16.50.1
   vrrp 10 priority 150
   vrrp 10 authentication ietf-md5 key-string 7 yqR5KJBqI+v/QzlmfBfPZQ==
   vrrp 10 ip 192.168.10.254
!
interface Vlan20
   ip address 192.168.20.253/24
   ip helper-address 172.16.50.1
   vrrp 20 priority 150
   vrrp 20 authentication ietf-md5 key-string 7 FBqWt0HgqJrI16piy59Scw==
   vrrp 20 ip 192.168.20.254
!
interface Vlan30
   ip address 192.168.30.253/24
   ip helper-address 172.16.50.1
   vrrp 30 authentication ietf-md5 key-string 7 FBqWt0HgqJrI16piy59Scw==
   vrrp 30 ip 192.168.30.254
!
interface Vlan40
   ip address 192.168.40.253/24
   vrrp 40 authentication ietf-md5 key-string 7 puOyeqkMgX3Ql1U7YaAQGg==
   vrrp 40 ip 192.168.40.254
!
ip routing
!
ip radius source-interface Loopback0
!
router ospf 1
   router-id 10.1.1.6
   passive-interface Ethernet4
   passive-interface Ethernet5
   passive-interface Ethernet6
   passive-interface Vlan10
   passive-interface Vlan20
   passive-interface Vlan30
   passive-interface Vlan40
   network 10.0.0.0/30 area 0.0.0.0
   network 10.0.0.8/30 area 0.0.0.0
   network 10.0.0.20/30 area 0.0.0.0
   network 10.1.1.6/32 area 0.0.0.0
   network 10.1.1.8/30 area 0.0.0.0
   network 192.168.10.0/24 area 0.0.0.0
   network 192.168.20.0/24 area 0.0.0.0
   network 192.168.30.0/24 area 0.0.0.0
   network 192.168.40.0/24 area 0.0.0.0
   max-lsa 12000
!
end
!
```

## vEOS-Dis-II

- Use the following configuration for `vEOS-Dis-II`.

```
logging trap notifications
logging host 172.16.50.1
logging source-interface Loopback0
!
hostname vEOS-Dis-II
ip name-server vrf default 172.16.50.1
!
ntp source Loopback0
ntp server 172.16.50.1
!
radius-server key 7 071B245F5A584B56
radius-server host 172.16.50.1
!
aaa authentication login default group radius local
aaa authentication enable default group radius local
aaa authorization console
aaa authorization exec default group radius local
!
enable secret sha512 $6$h7Vp2vi9tRF3EcXR$vjl6ZLcyQKo45mtBt9yrIZ0erxyp0yIP1qiOmpFVXYRvjHDFlAjRL67x5gzI8YpmpSHrOruPoffTNkWOc4sd0/
!
username admin privilege 15 role network-admin secret sha512 $6$WckLvxaEnBKW87vw$tJWlClN/EFoNfd/laqXVw1BX3dSynvI3UUlJsLEL6B1j97KkZk31R1UnstWcbiw/j4Tme5agvyLKHnqr0Wpbu1
!
clock timezone Europe/Bratislava
!
vlan 10,20,30,40
!
interface Ethernet1
   description Link to vIOS-Core-I
   no switchport
   ip address 10.0.0.17/30
   ip ospf network point-to-point
   ip ospf authentication message-digest
   ip ospf message-digest-key 1 md5 7 bS8fz/oIV8WdkUoexvixrA==
!
interface Ethernet2
   description Link to vIOS-Core-II
   no switchport
   ip address 10.0.0.13/30
   ip ospf network point-to-point
   ip ospf authentication message-digest
   ip ospf message-digest-key 1 md5 7 n+Pkjf+gomK+msssg0WWXA==
!
interface Ethernet3
   description Link to vEOS-Dis-I
   no switchport
   ip address 10.0.0.2/30
   ip ospf network point-to-point
   ip ospf authentication message-digest
   ip ospf message-digest-key 1 md5 7 n+Pkjf+gomK+msssg0WWXA==
!
interface Ethernet4
   description Link to OpenSwitch-Acc-II
   switchport trunk allowed vlan 30,40
   switchport mode trunk
!
interface Ethernet5
   description Link to OpenSwitch-Acc-I
   switchport trunk allowed vlan 10,20
   switchport mode trunk
!
interface Ethernet6
   description Link to Management OpenSwitch-Acc-II
   no switchport
   ip address 10.1.1.14/30
!
interface Ethernet7
   description Unused
   shutdown
   no lldp transmit
   no lldp receive
!
interface Loopback0
   ip address 10.1.1.7/32
!
interface Vlan10
   ip address 192.168.10.252/24
   ip helper-address 172.16.50.1
   vrrp 10 authentication ietf-md5 key-string 7 yqR5KJBqI+v/QzlmfBfPZQ==
   vrrp 10 ip 192.168.10.254
!
interface Vlan20
   ip address 192.168.20.252/24
   ip helper-address 172.16.50.1
   vrrp 20 authentication ietf-md5 key-string 7 FBqWt0HgqJrI16piy59Scw==
   vrrp 20 ip 192.168.20.254
!
interface Vlan30
   ip address 192.168.30.252/24
   ip helper-address 172.16.50.1
   vrrp 30 priority 150
   vrrp 30 authentication ietf-md5 key-string 7 FBqWt0HgqJrI16piy59Scw==
   vrrp 30 ip 192.168.30.254
!
interface Vlan40
   ip address 192.168.40.252/24
   vrrp 40 priority 150
   vrrp 40 authentication ietf-md5 key-string 7 puOyeqkMgX3Ql1U7YaAQGg==
   vrrp 40 ip 192.168.40.254
!
ip routing
!
ip radius source-interface Loopback0
!
router ospf 1
   router-id 10.1.1.7
   passive-interface Ethernet4
   passive-interface Ethernet5
   passive-interface Ethernet6
   passive-interface Vlan10
   passive-interface Vlan20
   passive-interface Vlan30
   passive-interface Vlan40
   network 10.0.0.0/30 area 0.0.0.0
   network 10.0.0.12/30 area 0.0.0.0
   network 10.0.0.16/30 area 0.0.0.0
   network 10.1.1.7/32 area 0.0.0.0
   network 10.1.1.12/30 area 0.0.0.0
   network 192.168.10.0/24 area 0.0.0.0
   network 192.168.20.0/24 area 0.0.0.0
   network 192.168.30.0/24 area 0.0.0.0
   network 192.168.40.0/24 area 0.0.0.0
   max-lsa 12000
!
end
!
```