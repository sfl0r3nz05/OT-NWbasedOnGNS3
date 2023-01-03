# OpenSwitch-Acc-I & II Configuration

![image](https://user-images.githubusercontent.com/69375071/210249340-0f4eab71-cb6c-41c2-b9e4-4e8c8be6caa5.png)

## OpenSwitch-Acc-I

1. Power on `OpenSwitch-Acc-I` and then double click it to enter its console.
2. Login with username `netop` and password `netop`. The password won't display by default.
3. Enter enable mode and then enter terminal config mode.

```
en
conf t
```

> Notice the difference between enable mode and terminal config mode. The terminal config mode must have the header appended by `(config)#`

![image](https://user-images.githubusercontent.com/69375071/210293414-ca1baf79-ec91-413e-aea1-e922cc6e0b85.png)

4. Copy and paste the following commands directly into the console. The console will exit to **enable mode** after these commands.

```
hostname OpenSwitch-Acc-I
timezone set europe/bratislava
ntp server 172.16.50.1
!
logging 172.16.50.1 severity notice
!
vlan 10
    no shutdown
vlan 20
    no shutdown
vlan 999
    no shutdown
spanning-tree config-name 70:72:cf:03:e5:3f
interface eth1 
    no shutdown
    no routing
    vlan trunk native 1
    vlan trunk allowed 20
    vlan trunk allowed 10
interface eth2 
    no shutdown
    no routing
    vlan trunk native 1
    vlan trunk allowed 20
    vlan trunk allowed 10
interface eth3 
    no shutdown
    no routing
    vlan access 10
interface eth4 
    no shutdown
    no routing
    vlan access 20
interface eth5
    no lldp transmit
    no lldp receive
interface eth6
    no lldp transmit
    no lldp receive
    no routing
    vlan access 999
interface eth7
    no lldp transmit
    no lldp receive
    no routing
    vlan access 999
interface vlan20 
    no shutdown
    ip address 192.168.20.250/24
interface mgmt
    ip static 10.1.1.9/30
    default-gateway 10.1.1.10
    nameserver 172.16.50.1
ip route 0.0.0.0/0 192.168.20.254
end
!
```

5. Copy running-config to startup-config.

```
copy running-config startup-config
```

6. Logout and close the console.

```
exit
```

## OpenSwitch-Acc-II

- Use the following configuration for `OpenSwitch-Acc-II`.

```
hostname OpenSwitch-Acc-II
timezone set europe/bratislava
ntp server 172.16.50.1
!
logging 172.16.50.1 severity notice
!
vlan 30
    no shutdown
vlan 40
    no shutdown
vlan 999
    no shutdown
spanning-tree config-name 70:72:cf:2c:42:28
interface eth1 
    no shutdown
    no routing
    vlan trunk native 1
    vlan trunk allowed 30
    vlan trunk allowed 40
interface eth2 
    no shutdown
    no routing
    vlan trunk native 1
    vlan trunk allowed 30
    vlan trunk allowed 40
interface eth3 
    no shutdown
    no routing
    vlan access 30
interface eth4 
    no shutdown
    no routing
    vlan access 40
interface eth5
    no routing
    vlan access 999
interface eth6
    no routing
    vlan access 999
interface eth7
    no routing
    vlan access 999
interface vlan40 
    no shutdown
    ip address 192.168.40.250/24
interface mgmt
    ip static 10.1.1.13/30
    default-gateway 10.1.1.14
    nameserver 172.16.50.1
ip route 0.0.0.0/0 192.168.40.254
end
!
```
