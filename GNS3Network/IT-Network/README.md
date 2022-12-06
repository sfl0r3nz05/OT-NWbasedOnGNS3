# Experimental Base Network on GNS3

- [Download current project status to be imported into GNS3](./ITNetwork.gns3project).

## Network Description

  <img src="./img/architecture.png"  width=75% height=75%>

1. This network consists of 3 layers: *access*, *distribution* and *core*.
2. The *data center (DC)* is composed of the layer 3 Cisco switch and the server. The design of the DC is very simplified as the network tiers are squeezed to a single switch layer 3 switch. The aim is to show configuration of the services running on the Server1 instead of discussing the complete DC design.
3. The company *edge router* is connected to the Internet using two *Internet Service Providers (ISPs)*.
4. The *Cisco ASA firewall* connects a campus network, data Center and the *edge router*.
5. The *edge router* connected *DMZ* to the rest of the enterprise network and to the Internet. The DMZ consists of the *Cisco ASA firewall*, layer 3 Cisco switch and the *DMZ* server.
6. The enterprise is connected to the ISP1 and ISP2 routers via enterprise *edge router*. Both *ISP* routers  are bridged via *GNS3 clouds* to the server Ethernet Card in order to simulate connection to the Internet.

## Building Layers

  The strategy for building the GNS3 network is to go from the bottom layer to the top layer.

### End devices

- To deploy only simple PC follows this [documentation](./../Devices-Configurations/devices_images/SimplePCs/README.md)

### Access Layer

#### Download and deploy images

- **Access Layer Switches** ares based on [Open Switch 0.4.0](./../Devices-Configurations/devices_images/Open_Switch_0.4.0/README.md) image.

#### Configuration files

- [Open Switch Access I](./../Devices-Configurations/config_files/OpenSwitch-Acc-I.txt)

- [Open Switch Access II](./../Devices-Configurations/config_files/OpenSwitch-Acc-II.txt)

### Distribution Layer

#### Download and deploy images

- **Distribution Layer Switches** are based on [Arista vEOS version 4.17.2F](./../Devices-Configurations/devices_images/Arista_vEOS_v4.17.2F/README.md) image.

#### Configuration files

- [Switch Distribution I](./../Devices-Configurations/config_files/vEOS-DIS-I.txt)
- [Switch Distribution II](./../Devices-Configurations/config_files/vEOS-DIS-II.txt)

### Core Layer

#### Download and deploy images

#### Configuration files

- [Switch Core I](./../Devices-Configurations/config_files/vIOS-Core-I-1.txt)
- [Switch Core II](./../Devices-Configurations/config_files/vIOS-Core-II-1.txt)



## Other Layers

1. [Firewall CISCO ASA](./../Devices-Configurations/config_files/vASA-I.txt)
2. [Switch Datacentre](./../Devices-Configurations/config_files/vIOS-Serv-I.txt)
3. [Router Edge](./../Devices-Configurations/config_files/vIOS-EDGE-U.txt)
4. [Router ISP1](./../Devices-Configurations/config_files/ISP1.txt)
5. [Router ISP2](./../Devices-Configurations/config_files/ISP2.txt)
6. [Firewall CISCO ASA DMZ](./../Devices-Configurations/config_files/ASAv-DMZ-I.txt)
7. [Switch DMZ](./../Devices-Configurations/config_files/vIOS-DMZ-I.txt)
