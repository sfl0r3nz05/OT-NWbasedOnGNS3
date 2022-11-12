# Simple PC Configuration

The PC is used for administration of network devices in the topology therefore it has statically configured IP address. All PCs are Core LInux Qemu appliances, running Core Linux 6.3. They have assigned 64MB RAM by GNS3. Below is a static IP address configuration for PC. For example, if it is used only PC4:

```console
vim /opt/bootlocal.sh

hostname PC4
ifconfig eth0 192.168.40.1 netmask 255.255.255.0
route add default gw 192.168.40.254
echo "nameserver 172.16.50.1" > /etc/resolv.conf
```

To save configuration we need to enter the command below.

```console
/usr/bin/filetool.sh -b
```
