# Server1 & Server-DMZ-I Network Issue

This is the problem when you run `ip a` or `ifconfig -a` or `ip addr` in Server1, it only prints `lo` interface, but `ens*`-like interfaces are missing.

It's mainly a "-nic none" issue which is the default launch configuration of GNS3 QEMU images. The simple solution is to add "-net nic -net user" options in additional settings, as shown in picture below.



After that, start the Server1 and run `ip a`, you will see the additional `ens3` and `ens4` interfaces. Then `vim /etc/netplan/*.yaml` to change the network config according to identified interfaces name. Pay attention that YAML files are strictly structured by indentation. Finally, run `sudo netplan apply` to update the network config.