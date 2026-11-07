---
title: "Network Interface FAQ"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Network-interface-FAQ"
---

<span id="ySDKKC5E"></span>
## How many IP addresses can be assigned to a network interface (ENI)?


* An unmounted secondary ENI can be assigned up to 10 private IPv4 addresses and 10 private IPv6 addresses.

* The number of IPv4 and IPv6 addresses assignable to a primary ENI or a secondary ENI attached to an Elastic Compute Service (ECS) is determined by the per\-ENI private IP quota for that specific [instance type](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).


For more details, see [Adding/Releasing a private IP](https://docs.byteplus.com/en/docs/vpc/Adding-or-releasing-a-private-IP-address).

<span id=".5LiA5Y-w5LqR5pyN5Yqh5Zmo5a6e5L6L5pSv5oyB5oyC6L295aSa5bCR5byg572R5Y2h77yf"></span>
## How many ENIs can be attached to a single ECS instance?

An ECS instance has only one primary ENI, but multiple secondary ENIs can be attached as needed. The maximum number of ENIs is determined by the Elastic Network Interfaces (including one primary ENI) metric in the ECS instance types documentation. For details, see [Instance type list](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

<span id=".5Li7572R5Y2h5ZKM6L6F5Yqp572R5Y2h5pyJ5LuA5LmI5Yy65Yir77yf"></span>
## What is the difference between a primary ENI and a secondary ENI?

The main differences are:


* Primary ENI: Created automatically with the ECS instance and bound to its lifecycle. It cannot be manually detached.

* Secondary ENI: Added to an ECS instance to meet specific needs. It can be manually detached and subsequently attached to other instances.


General\-purpose operating systems route default traffic through the primary ENI by design. If network connectivity issues occur when using a secondary ENI, this is usually due to a routing configuration problem; see [Modifying a network interface route](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances) to adjust the routing configuration.

<span id=".5LqR5pyN5Yqh5Zmo5a6e5L6L5oyC6L296L6F5Yqp572R5Y2h5ZCO77yM5Li65LuA5LmI5peg5rOV5L2_55So6L6F5Yqp572R5Y2h77yf"></span>
## Why is my secondary ENI unusable after attaching it to an ECS instance?

After mounting a secondary ENI to your ECS instance, most operating system images (with limited exceptions) cannot automatically recognize the secondary interface's primary private IP address, and add corresponding routes to the routing table. This will render the secondary ENI non\-functional. You must manually configure both the interface and its routes. For detailed steps, please see [ network interface](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances)[ network interface](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances)[ network interface](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances).


|Operating System Types |Version |
|---|---|
|CentOS |CentOS 8.x, CentOS Stream |
|Fedora |Fedora 37 64\-bit |
|Windows Server |All versions |


<span id=".5Li66L6F5Yqp572R5Y2h57uR5a6a5YWs572RSVDvvIzkuLrku4DkuYjku43nhLbml6Dms5Xorr_pl67lpJbnvZHvvJ8="></span>
## Why can't I access the Internet after binding an EIP to a secondary ENI?

Possible causes include:


|Cause |Notes |
|---|---|
|Resource status abnormal |EIP or ECS malfunction, such as service suspension due to expiration. |
|Not mounted to an ECS |Secondary network interface not mounted to an ECS |
|Network interface not recognized |ECS failed to recognize the network interface. |
|Issues with secondary network interface routing |Routes not taking effect on secondary network interface. Manual configuration required. See [Modifying a network interface route](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances). |


<span id=".54Gr5bGx5byV5pOO572R5Y2h5piv5YWo5Y-M5bel6L-Y5piv5Y2K5Y-M5bel5qih5byP77yf"></span>
## Is the BytePlus network interface full\-duplex or half\-duplex?

The default mode is full\-duplex.

<span id="87SguJit"></span>
## How to view the ENI corresponding to an IP address?


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation tree, select **Network Interface**.

3. Click the search bar in the upper left, choose **Private IP**, then select **Equal to**.

4. Enter the IP address and press the Enter key to view the ENI that matches the IP address.


&nbsp;

&nbsp;

&nbsp;

&nbsp;
