# ISP1 & 2 Configuration

![image](/img/11.png)

## ISP1

- No need to login. No username and no password by default.

> After configuration and logout, username becomes `admin`, password becomes `cisco`

- Use the following configuration for `ISP1`.

```
hostname ISP1
!
ip name-server 8.8.8.8
ip name-server 8.8.4.4
!
interface GigabitEthernet0/0
 no shutdown
 description Link to Simulated Internet
 ip address dhcp
 ip nat outside
 media-type gbic
 no cdp enable
!
interface GigabitEthernet1/0
 no shutdown
 description Link to Company Inc.
 ip address 198.10.10.1 255.255.255.252
 ip nat inside
!
router bgp 64501
 bgp log-neighbor-changes
 network 0.0.0.0
 neighbor 198.10.10.2 remote-as 64500
 neighbor 198.10.10.2 password isp1md5pass
 neighbor 198.10.10.2 ttl-security hops 1
 neighbor 198.10.10.2 route-map static_default out
!
ip nat inside source list 1 interface GigabitEthernet0/0 overload
!
ip prefix-list static_default seq 5 permit 0.0.0.0/0
access-list 1 permit 195.1.1.0 0.0.0.255
access-list 1 permit 198.10.10.0 0.0.0.3
access-list 1 deny   any
!
route-map static_default permit 10
 match ip address prefix-list static_default
!
end
!
```

## ISP2

- Use the following configuration for `ISP2`.

```
hostname ISP2      
!
ip name-server 8.8.8.8
ip name-server 8.8.4.4
!
interface GigabitEthernet0/0
 no shutdown
 description Link to Simulated Internet
 ip address dhcp
 ip nat outside
 media-type gbic
!
interface GigabitEthernet1/0
 no shutdown
 description Link to Company Inc.
 ip address 197.10.10.1 255.255.255.252
 ip nat inside
!
router bgp 64502
 bgp log-neighbor-changes
 network 0.0.0.0
 neighbor 197.10.10.2 remote-as 64500
 neighbor 197.10.10.2 password isp2md5pass
 neighbor 197.10.10.2 ttl-security hops 1
 neighbor 197.10.10.2 route-map static_default out
!
ip nat inside source list 1 interface GigabitEthernet0/0 overload
!
ip prefix-list static_default seq 5 permit 0.0.0.0/0
access-list 1 permit 195.1.1.0 0.0.0.255
access-list 1 permit 197.10.10.0 0.0.0.3
access-list 1 deny   any
!
route-map static_default permit 10
 match ip address prefix-list static_default
!
end
!
```
