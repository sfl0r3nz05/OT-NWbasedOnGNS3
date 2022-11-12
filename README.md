# Adaptive Countermeasure based on Software-Defined Networking for Industrial Control Systems

- [Adaptive Countermeasure based on Software-Defined Networking for Industrial Control Systems](#adaptive-countermeasure-based-on-software-defined-networking-for-industrial-control-systems)
  - [Prerequisites](#prerequisites)
  - [GNS3 network](#gns3-network)
    - [How to deploy GNS3 server](#how-to-deploy-gns3-server)
    - [How to start with the GNS3 Network](#how-to-start-with-the-gns3-network)
  - [SDN Deployment](#sdn-deployment)

> **Note:** This repo is under development ⛏.
> > It is maintained by [Ziyao Wang](ziyao.wang@se19.qmul.ac.uk), [Mikel Dean](mdeanoses@ceit.es) and [Santiago Figueroa](sfigueroa@ceit.es) as part of the project: *Adaptive Countermeasure based on Software-Defined Networking for Industrial Control Systems*.

> **Note:** Check the meeting minutes ✏.
> > [Meeting minutes](./minutes)

## Prerequisites

This repo requires the deployment of 2 instances (e.g. EC2 on AWS).

1. Dedicated to the installation of the GNS3 server which will contain the experimental base network.
2. Dedicated to SDN controller deployment.

## Experimental Base Network on GNS3

### How to deploy GNS3 server

1. Follow this instructions to [deploy the *GNS3 server* on an EC2 instance](./GNS3ServerDeployment/README.md).

### How to start with the Experimental Base Network on GNS3.

1. Follow this instructions to [start with the deployment of the *Experimental base Network* on the GNS3 Server*](./GNS3Network/README.md).

## SDN Deployment

1. Follow this instructions to deploy the [SDN-Controller connected to the Experimental Base Network](./SDNDeployment/README.md).
