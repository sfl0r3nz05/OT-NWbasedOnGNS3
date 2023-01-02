# Importing Appliances to GNS3 Server

- This is the generic guide for importing an appliance to GNS3 server.
- Download all required templates [here](./gns3-appliances.zip).

## Procedures

1. Select `Import appliance` from the menu bar of GNS3 client to open a `.gns3a` file.

![image](/img/1.png)

2. Click `Next` twice for default options and then enter the `Install XXX appliance` window.

![image](/img/4.png)

3. Click on the subdirectory and notice that two buttons `Import` and `Download` appear at the bottom of the window. Click `Download` to open a download link for the image in your web browser.

> Some appliances require multiple images. Make sure to download and import all of them.

![image](/img/5.png)

4. After you download the image, click `Import` to upload it to GNS3 server. On success, the appliance status will be `Ready to install`. Select the root directory `XXX verion X.X.X` and then click `Next` to complete the importing process.

> `Next` button will not work if you do not select the root directory.

![image](/img/7.png)

5. Read the `Usage` carefully before configuring the network.

![image](/img/8.png)

> You can review the `Usage` by right clicking the appliance from the sidebar, selecting `Configure template`, and navigating to `Usage` section.

|||
|-|-|
|![image](/img/9.png)|![image](/img/10.png)|