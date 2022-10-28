# Controller installation

- [Controller installation](#controller-installation)
  - [Prerequisitos](#prerequisitos)
  - [Desplegar OpenDayLight](#desplegar-opendaylight)

Esta sección establece los procedimientos para descargar y configurar el controlador.

## Prerequisitos

- Tener la instancia `t2.medium` (*SDN-Controller*) desplegada
- Conexión a dicha instancia vía `ssh`.
- [Instalar Docker sobre Ubuntu](https://docs.docker.com/engine/install/ubuntu/).

## Desplegar OpenDayLight

> *Note:* The OpenDaylight Project is a collaborative open-source project hosted by the Linux Foundation. The project serves as a platform for software-defined networking for open, centralized, computer network device monitoring.

1. Lanzar el contenedor:

    ```console
     docker run -d --network host --name=opendaylight stephanfuhrmannionos/opendaylight:0.8.4
    ```

2. Conectarse al contenedor:

    ```console
    docker exec -ti opendaylight bin/client
    ```

   - Output:
  
     ```console
     Apache Karaf starting up. Press Enter to open the shell now...
     100% [========================================================================]
     Karaf started in 3s. Bundle stats: 54 active, 55 total

          ________                       ________                .__  .__       .__     __
          \_____  \ ______   ____   ____ \______ \ _____  ___.__.|  | |__| ____ |  |___/  |_
           /   |   \\____ \_/ __ \ /    \ |    |  \\__  \<   |  ||  | |  |/ ___\|  |  \   __\
          /    |    \  |_> >  ___/|   |  \|    `   \/ __ \\___  ||  |_|  / /_/  >   Y  \  |
          \_______  /   __/ \___  >___|  /_______  (____  / ____||____/__\___  /|___|  /__|
                  \/|__|        \/     \/        \/     \/\/            /_____/      \/


     Hit '<tab>' for a list of available commands
     and '[cmd] --help' for help on a specific command.
     Hit '<ctrl-d>' or type 'system:shutdown' or 'logout' to shutdown OpenDaylight.

     opendaylight-user@root> 
     ```

3. Refresh Karaf features

     ```console
     feature:repo-refresh
     ```

4. Install Karaf features:

     - To install a feature, use the following command, where feature1 is the feature name listed in the table below:

          ```console
          feature:install <feature1>
          ```

     - You can install multiple features using the following command:

          ```console
          feature:install <feature1> <feature2> ... <featureN-name>
          ```

     1. odl-l2switch-switch
     2. odl-l2switch-all
     3. odl-dlux-core
     4. odl-dluxapps-yangutils
     5. features-dlux
     6. odl-dluxapps-applications
     7. odl-dluxapps-yangvisualizer
     8. odl-dluxapps-topology
     9. odl-dluxapps-nodes
     10. odl-restconf-all
     11. odl-netconf-topology
     13. odl-yanglib
     14. odl-mdsal-all
     15. odl-openflowplugin-southbound

          ```console
          feature:install odl-l2switch-switch odl-dlux-core odl-dluxapps-yangutils features-dlux odl-dluxapps-applications odl-dluxapps-yangvisualizer odl-dluxapps-topology odl-dluxapps-nodes odl-restconf-all odl-openflowplugin-southbound odl-l2switch-all odl-netconf-topology odl-yanglib odl-mdsal-all
          ```  

5. Para verificar la lista de las features:

    ```console
    feature:list
    ```

6. `OpenDaylight` exposed TCP ports in AWS inbound rules:
   - `6633` Openflow,
   - `8101` Karaf CLI via SSH (see below),
   - `8181` RESTCONF / HTTP

7. A través del navegador, y usando la IP pública de la instancia (e.g.: `http://35.174.155.88:8181/index.html#/login`) podremos ver la interfaz web del controller.

    1. Pero, en primer lugar, hay que introducir las credenciales que por defecto son:

          ```console
          Username: admin
          Password: admin
          ```

          ![image](./img/OpenDaylight.png)
