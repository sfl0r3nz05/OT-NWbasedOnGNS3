# Server1 Configuration

> You should complete all other configuration before configuring `Server1` and `Serv-DMZ-I` to ensure that they can have access to the Internet.

![image](https://user-images.githubusercontent.com/69375071/210246893-35e9d051-41e5-4f23-b967-3cb49b5035d0.png)

1. Login with username `ubuntu` and password `ubuntu`.
2. Check the network status. We find that both `ens3` and `ens4` are in `state DOWN`, which means no Internet connection.

```console
ip a
```
![image](https://user-images.githubusercontent.com/69375071/211831061-3ac6b5f7-334f-46c8-99c7-ec2fd07bf2ad.png)

3. Switch to root user and load a bonding module to Linux kernel.

```console
sudo su
modprobe bonding
echo "bonding" >> /etc/modules
```

4. Edit netplan to establish valid Internet connection.

> I assume you know how to use vim editor. Use `i` to enter `INSERT` mode, `ESC` to back to default mode, and `:wq` to save and exit.

```console
vim /etc/netplan/50-cloud-init.yaml
```

```yaml
network:
    ethernets:
        ens3:
            dhcp4: false
        ens4:
            dhcp4: false
    bonds:
        bond0:
            addresses:
                - 172.16.50.1/24
            routes:
                - to: default
                  via: 172.16.50.254
            nameservers:
                addresses:
                    - 172.16.50.1
            interfaces:
                - ens3
                - ens4
            parameters:
                mode: balance-rr
                mii-monitor-interval: 100
    version: 2
```

5. Apply the netplan. You can check by `ip a` that both `ens3` and `ens4` are `UP` and have a master `bond0`.

```console
netplan apply
```

6. 
