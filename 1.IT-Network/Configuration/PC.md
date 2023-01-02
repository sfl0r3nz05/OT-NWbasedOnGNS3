# PC1 - 4 Configuration

- I assume you have completed the deployment of IT network according to the image below. Now, let's start the configuration of IT network.

![image](https://user-images.githubusercontent.com/69375071/210222682-ff2e0d4b-101a-4ed2-b300-6f1c98e9e1c8.png)

- We take `PC1` for example, because they share the same configuration process.

![image](/img/1.png)

- Right click `PC1` and select `Edit config` from the menu. This opens a txt file for PC1 startup-config.
- Append the txt with the following line and then `Save` it. This assigns PC1 with IP address 192.168.10.1, subnet mask 255.255.255.0, and gateway 192.168.10.254

```
ip 192.168.10.1/24 192.168.10.254
```

|||
|-|-|
|![image](/img/2.png)|![image](/img/3.png)|

- Replicate the process in PC2, PC3, and PC4. Change the IP address and gateway according to the second image in this article.