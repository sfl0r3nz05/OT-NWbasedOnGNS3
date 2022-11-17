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

# VPCS Configuration

GNS3 has built-in end device VPCS that is simple to configure. The pictures below detail the name, IP, and gateway configuration.

<img width="348" alt-"Screenshot 2022-11-17 at 22 07 23" src="https://user-images.githubusercontent.com/69375071/202468500-1180a829-810b-45f8-8be1-d675e1acf720. png">

In the IP line, '192.168.10.1/24 indicates the IP address and subnet mask, and '192.168.10.254' is the gateway.

<ima width="772" alt="Screenshot 2022-11-17 at 22 07 37" src="https://user-images.githubusercontent.com/69375071/202468542-79819814-868b-456-a307-268aa6fda249. png">
  
