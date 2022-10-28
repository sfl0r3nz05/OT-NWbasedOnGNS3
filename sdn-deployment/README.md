# Laboratorio de SDN

- [Laboratorio de SDN](#laboratorio-de-sdn)
  - [Prerequisitos](#prerequisitos)
  - [Despliegue de la GNS3-Network](#despliegue-de-la-gns3-network)
  - [Despliegue del controlador SDN](#despliegue-del-controlador-sdn)
  - [Integración de la GNS3-Network con el SDN-Controller](#integración-de-la-gns3-network-con-el-sdn-controller)

## Prerequisitos

1. Crear 2 instancias *EC2* en *AWS* una `t2.medium` y una `t2.large`:
   1. Renombrar la instancia `t2.medium` como *SDN-Controller*.
   2. Renombrar la instancia `t2.large` como *GNS3-Server*.
2. Desplegar el servidor GNS3 en la instancia `t2.large`(*GNS3-Server*) siguiendo la siguiente [documentación](../GNS3ServerDeployment/README.md).

## Despliegue de la GNS3-Network

- Desplegar la Red correspondiente en la instancia `t2.large`(*GNS3-Server*) siguiendo la siguiente [documentación](./RedGNS3/REDGNS3.md)

## Despliegue del controlador SDN

- Desplegar el *Controlador SDN* en la instancia `t2.medium` siguiendo la siguiente [documentación](./Controller-SDN/controller.md).

## Integración de la GNS3-Network con el SDN-Controller

- Integrar la *GNS3-Network* y el *SDN-Controller* siguiendo la siguiente [documentación](./Integration-GNS3_Network-Controller-SDN/integration.md).
