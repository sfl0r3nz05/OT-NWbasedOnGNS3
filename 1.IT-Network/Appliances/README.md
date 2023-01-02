# Importing Appliances to GNS3 Server

- This is the generic guide for importing an appliance to GNS3 server.
- Download all required templates [here](./gns3-appliances.zip).

## Procedures

1. Select `Import appliance` from the menu bar of GNS3 client to open a `.gns3a` file.

![image](https://user-images.githubusercontent.com/69375071/210214639-95e7f455-faed-462c-9c72-3b93b19976d5.png)

2. Click `Next` twice for default options and then enter the `Install XXX appliance` window.

![image](https://user-images.githubusercontent.com/69375071/210214665-8bb7eddf-150a-4985-9130-d12d971f02d0.png)

3. Click on the subdirectory and notice that two buttons `Import` and `Download` appear at the bottom of the window. Click `Download` to open a download link for the image in your web browser.

> Some appliances require multiple images. Make sure to download and import all of them.

![image](https://user-images.githubusercontent.com/69375071/210214700-58abe174-740a-4b47-aa70-5b639d8cb842.png)

4. After you download the image, click `Import` to upload it to GNS3 server. On success, the appliance status will be `Ready to install`. Select the root directory `XXX verion X.X.X` and then click `Next` to complete the importing process.

> `Next` button will not work if you do not select the root directory.

![image](https://user-images.githubusercontent.com/69375071/210248364-4164a55a-89d3-4f92-824b-28e33ceeb104.png)

5. Read the `Usage` carefully before configuring the network.

![image](https://user-images.githubusercontent.com/69375071/210248483-dfee17c9-ea86-4c1b-bee8-db25e9a9fc45.png)

> You can review the `Usage` by right clicking the appliance from the sidebar, selecting `Configure template`, and navigating to `Usage` section.

|||
|-|-|
|![image](https://user-images.githubusercontent.com/69375071/210214741-14ee5e60-fc58-4088-ac05-1784571e8b23.png)|![image](https://user-images.githubusercontent.com/69375071/210248600-baa8416d-2215-4327-830c-b4ddf691f657.png)|
