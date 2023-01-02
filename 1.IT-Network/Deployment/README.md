# Deployment of Experimental IT Network on GNS3

- This is the generic guide for deployment of experimental IT network.

## Configuring GNS3 Client

- It's advised to enable `Show the grid`, `Snap to grid`, and `Show interface labels` in the view section of GNS3 client menu bar. You can get a better workspace from them.

![image](/img/11.png)

## Mapping Devices to Appliances

- Drag appliances from sidebar to workspace according to the image and table below.
- Rename devices according to the image.

![image](https://user-images.githubusercontent.com/69375071/210197317-12a7553f-9dea-4a2c-9336-2f2b721b06b8.png)

| Devices | Appliances |
| --- | --- |
| PC1 - PC4 | VPCS |
| OpenSwitch-Acc-I & II | OpenSwitch 0.4.0 |
| vEOS-Dis-I & II | |
| vIOS-Core-I & II, vIOS-Ser-I, vIOS-DMZ-I | |
| ASAv-I, ASAv-DMZ-I | |
| vIOS-Edge-I | |
| ISP1 & 2 | 7200 |
| Server1, Serv-DMZ-I | |
| Internet | Cloud |

### Renaming a Device

- The device must be powered off.
- **Double click** the device to show the config window. Edit the `Name` of the device and click `Apply` and then `OK`.

![image](/img/13.png)

## Connecting Devices

- Click `Add a link` from sidebar to enter linking mode.
- Click on a device and select an interface for one side, and click on another device and select an interface for another side. This forms a connection between them.
- Right click on a wrong connection to delete it.

|||
|-|-|
|![image](/img/15.png)|![image](/img/16.png)|

- Follow the image below to connect all devices. It's very simple and strightforward.
> Notice that some devices has port `mgmt` which is an alternative name for eth0 / e0. That's because port 0 is usually used as management port.

![image](https://user-images.githubusercontent.com/69375071/210197317-12a7553f-9dea-4a2c-9336-2f2b721b06b8.png)
