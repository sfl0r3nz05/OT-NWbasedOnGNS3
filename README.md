# Adaptive Countermeasure based on SDN for ICS

> **Note:** This repo is under development ⛏ and maintained by [Ziyao Wang](ziyao.wang@se19.qmul.ac.uk), [Mikel Dean](mdeanoses@ceit.es) and [Santiago Figueroa](sfigueroa@ceit.es) as part of the project: *Adaptive Countermeasure based on Software-Defined Networking for Industrial Control Systems*.

>> Check the [Meeting minutes](./Meeting%20Minutes/) ✏.

## Terminologies

- SDN = Software Defined Networking
- ICS = Industrial Control System

![image](https://user-images.githubusercontent.com/69375071/210196870-f1af4548-1d5f-4c7f-9654-5174ff9f5f75.png)

## Prerequisites

This repo requires the deployment of 2 AWS EC2 instances:

- The first instance hosts the GNS3 server running the experimental IT-Network/OT-Network.
  - [Deploy the GNS3 server](./GNS3ServerDeployment/README.md) on an EC2 instance.
- Second hosts the SDN controller.

## Deployment of Experimental IT Network on GNS3 Server

1. [Deploy the Experimental IT Network](./IT-Network/README.md) on the GNS3 Server.
2. [Deploy the Experimental OT Network](./OT-Network/README.md) on the GNS3 Server.

## Deployment of SDN Controller

1. [Deploy the SDN-Controller](./SDNDeployment/README.md) connected to the Experimental Base Network.

## Troubleshooting

- [Examines the main troubleshooting](./Troubleshootings/README.md)
