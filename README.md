# Adaptive Countermeasure based on SDN for ICS

- [Adaptive Countermeasure based on SDN for ICS](#adaptive-countermeasure-based-on-sdn-for-ics)
  - [Terminologies](#terminologies)
  - [Prerequisites](#prerequisites)
  - [Deployment of Experimental Base Network on GNS3 Server](#deployment-of-experimental-base-network-on-gns3-server)
  - [Deployment of SDN Controller](#deployment-of-sdn-controller)
  - [Troubleshootings](#troubleshootings)

> **Note:** This repo is under development ⛏ and maintained by [Ziyao Wang](ziyao.wang@se19.qmul.ac.uk), [Mikel Dean](mdeanoses@ceit.es) and [Santiago Figueroa](sfigueroa@ceit.es) as part of the project: *Adaptive Countermeasure based on Software-Defined Networking for Industrial Control Systems*.

> **Note:** Check the [Meeting minutes](./Meeting%20Minutes/) ✏.

## Terminologies

- SDN = Software Defined Networking
- ICS = Industrial Control System

## Prerequisites

This repo requires the deployment of 2 AWS EC2 instances. One instance hosts the GNS3 server which runs the experimental base network, the other hosts the SDN controller.

## Deployment of Experimental Base Network on GNS3 Server

1. [Deploy the GNS3 server](./GNS3ServerDeployment/README.md) on an EC2 instance.

2. [Deploy the Experimental base Network](./GNS3Network/README.md) on the GNS3 Server.

## Deployment of SDN Controller

1. [Deploy the SDN-Controller](./SDNDeployment/README.md) connected to the Experimental Base Network.

## [Troubleshootings](./Troubleshootings/README.md)
