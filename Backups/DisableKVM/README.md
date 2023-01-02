# Turn off KVM support in the gns3_server.conf

When this error appear:

```console
=> error while starting appdconsole-1: KVM acceleration cannot be used (/dev/kvm doesn't exist). It is possible to turn off KVM support in the gns3_server.conf by adding enable_kvm = false to the [Qemu] section.
```

   <img src="./img/img-1.png" width=75% height=75%>

1. Create a `gns3_server.conf` in `~/.config/GNS3/2.2/gns3_server.conf`
2. Include next configs in the file:

```console
[Qemu]
enable_hardware_acceleration = False
require_hardware_acceleration = False
```
