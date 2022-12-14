# Cisco Adaptive Security Virtual Appliance (ASAv)

- The **Fiwewall Layer** consists of the firewall ASAv-I.
- The *Cisco ASAv 9.9.1 Qemu* image can be downloaded as zip file which will be unzipped as [QEMU](https://drive.google.com/file/d/1oRBEiPqFOT9Ta_2QEB3U-SByy5k2PZ1d/view?usp=sharing).
- The *cisco-asav.gns3a* appliance also must be downloaded from [here](https://drive.google.com/file/d/1HoL0Ssser9Yl29s05jsRDl18L4ADqT0b/view?usp=share_link).
- The official *cisco-asav.gns3a* can be downloaded [here](https://www.gns3.com/gns3/appliance/download?url=https%3A%2F%2Fraw.githubusercontent.com%2FGNS3%2Fgns3-registry%2Fmaster%2Fappliances%2Fcisco-asav.gns3a). This not include *Cisco ASAv 9.9.1* version. The following section discusses how to add a new image to the appliance:

## How to add an image to appliance file 

1. Open the appliance file *cisco-asav.gns3a* with a text editor.

2. The *Cisco ASAv 9.9.1* zip file contains next three files:

    <img src="./img/vm0.PNG" width=75% height=75%>

3. Add the next configuration into `images` array:

    ```console
    {
        "filename": "asav991.qcow2",
        "version": "9.9.1",
        "md5sum": "40373fda0704d9272f89fd0bcbe4c69a",
        "filesize": 229871616,
        "download_url": "https://software.cisco.com/download/home/286119613/type/280775065/release/9.9.1"
    }
    ```

4. Add the next configuration into `versions` array:

    ```console
    {
        "name": "9.9.1",
        "images": {
            "hda_disk_image": "asav991.qcow2"
        }
    }
    ```

5. Save the appliance file *cisco-asav.gns3a*.

## How to add the appliance file

1. Select import appliance:

    <img src="./img/vm1.png" width=50% height=50%>

2. Select the appliance:

    <img src="./img/vm2.PNG" width=50% height=50%>

3. Select install the appliance on the main server:

    <img src="./img/vm3.PNG" width=75% height=75%>

4. Select the qemu binary:

    <img src="./img/vm4.PNG" width=75% height=75%>

5. Select the ASAv version to be imported:

    <img src="./img/vm5.PNG" width=75% height=75%>

6. Select the ASAv version to be imported:

    <img src="./img/vm6.PNG" width=75% height=75%>

7. Select the *ASAv image qcow2* to be imported:

    <img src="./img/vm7.PNG" width=75% height=75%>

8. Start image importation:

    <img src="./img/vm8.PNG" width=75% height=75%>

9. Continue image importation:

    <img src="./img/vm9.PNG" width=75% height=75%>

10. Continue image importation:

    <img src="./img/vm10.PNG" width=75% height=75%>

11. Imported *ASAv image qcow2*:

    <img src="./img/vm11.PNG" width=75% height=75%>

12. Accept installation of the *ASAv image qcow2*:

    <img src="./img/vm12.PNG" width=75% height=75%>

13. Make a description for the *ASAv image qcow2*:

    <img src="./img/vm13.PNG" width=75% height=75%>

14. Receive a message when the *ASAv image qcow2* be installed:

    <img src="./img/vm14.PNG" width=75% height=75%>

15. Verify the *ASAv firewall*:

    <img src="./img/vm15.PNG" width=75% height=75%>

16. Add the *ASAv firewall*:

    <img src="./img/vm16.PNG" width=75% height=75%>
