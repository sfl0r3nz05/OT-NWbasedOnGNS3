# Deployment of Experimental IT Network on GNS3

- This is the generic guide for deployment of experimental IT network.

## Configuring GNS3 Client

- It's advised to enable `Show the grid`, `Snap to grid`, and `Show interface labels` in the view section of GNS3 client menu bar.
- Use `Fit in view` to automatically zoom the workspace to display all devices.

![image](https://user-images.githubusercontent.com/69375071/210214869-4f799ce6-8802-4d91-9067-09c19aedb078.png)

## Mapping Devices to Appliances

1. Drag appliances from sidebar to workspace according to the image and table below.
2. [Rename devices](#renaming-a-device) according to the image below.
3. [Configure network adapters](#configuring-network-adapters-for-server1) for `Server1`.
4. [Check the host for available NICs](#checking-nics-of-the-host) to be used in `Cloud` devices.

![image](https://user-images.githubusercontent.com/69375071/210197317-12a7553f-9dea-4a2c-9336-2f2b721b06b8.png)

| Devices | Appliances |
| --- | --- |
| PC1 - 4 | VPCS |
| OpenSwitch-Acc-I & II | OpenSwitch 0.4.0 |
| vEOS-Dis-I & II | vEOS 4.17.10M |
| vIOS-Core-I & II, vIOS-Ser-I, vIOS-DMZ-I | vIOS 15.2(20170321:233949) |
| ASAv-I, ASAv-DMZ-I | ASAv 9.6.1 |
| vIOS-Edge-I | vIOS 15.6(2)T |
| ISP1 & 2 | 7200 152-4.S5 |
| Server1, Serv-DMZ-I | Server 22.04 LTS |
| Internet | Cloud |

### Renaming a Device

- The device must be powered off.
- **Double click** the device to show the config window. Edit the `Name` of the device and click `Apply` and then `OK`.

![image](https://user-images.githubusercontent.com/69375071/210249045-e5e70657-af20-414f-89ce-3a11b2bf9a28.png)

### Configuring Network Adapters for Server1

- The device must be powered off and **unlinked**.
- **Double click** the device to show the config window. Navigate to `Network` section and change the number of `Adapters` to `2`, and then `Apply` and `OK`.

![image](https://user-images.githubusercontent.com/69375071/210222657-c5b86044-892c-4361-bd01-bb292984a7bb.png)

### Checking NICs of the Host

- Open a SSH terminal for the host where GNS3 server runs.
- Use `ip a` to check all available NICs. Note the `state UP` of `enp5s0` and its IPv4 address `inet 192.168.0.2/24`, which means the NIC `enp5s0` has valid Internet connection.
- Also, note the `state DOWN` of `wlo1` and its empty address, which means the NIC `wlo1` is not connected to the Internet.

> The condition varies among different hosts, but the naming convention remains the same. Pay attention to NICs with names `ens?`, `enp?s0`, `wlo?`, `wlp?s0` and so on.

> You can ignore the localhost `lo` and docker-created NICs `virbr0` and `docker0`.

![image](https://user-images.githubusercontent.com/69375071/211830581-df3713bd-9f7a-4ec9-a21e-3d53e3891d1a.png)


- Select an interface with access to the Internet when connecting `Cloud` devices in GNS3. In this example, select `enp5s0` instead of `wlo1`.

![image](https://user-images.githubusercontent.com/69375071/211830746-93452061-241f-418a-9aa3-fb83e0048ce5.png)

## Connecting Devices

- Click `Add a link` from sidebar to enter linking mode.
- Click on a device and select an interface for one side, and click on another device and select an interface for another side. This forms a connection between them.
- Right click on a wrong connection to delete it.

|||
|-|-|
|![image](https://user-images.githubusercontent.com/69375071/210214930-29754228-799d-4b3f-82c0-2c9ed049e078.png)|![image](https://user-images.githubusercontent.com/69375071/210214939-7ba60df6-5270-4294-9799-7b48161fa01b.png)|

- Follow the image below to connect all devices. It's very simple and straightforward.
> Notice that some devices have port `mgmt` which is an alternative name for eth0 / e0. That's because port 0 is usually used as management port.

![image](https://user-images.githubusercontent.com/69375071/210222682-ff2e0d4b-101a-4ed2-b300-6f1c98e9e1c8.png)
