---
title: "Change the network type of an ALB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Associating-and-disassociating-an-elastic-IP"
---

This article explains how to change the network type of an ALB instance. The network type change involves attaching or detaching a public IP address.

<span id="717270d3"></span>
## Background

<span id="ab2aa2a8"></span>
### Network type

The network types of an ALB instance include “public network” and “VPC.”


* **Public network**: A public network ALB instance has both public and private IP addresses. A public network ALB instance can be accessed from the internet and resources within the instance’s VPC.

* **VPC**: A VPC ALB instance has only private IP addresses and can only be accessed by resources within the instance’s VPC.


<span id="7b681414"></span>
### Change network type

The network type of an ALB instance can change from VPC to Internet\-facing instance or from Internet\-facing instance to VPC.

Dual\-stack ALB instances do not support network type changes. The table below shows the impact of changing the network type of an IPv4 ALB instance.


|**Change Actions** |**change impact** |
|---|---|
|Change private instance to Internet\-facing instance |The instance domain name will resolve to the public IP address.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The public IP address will incur billing. For billing details, see <a href="https://docs.byteplus.com/docs/eip/Pay-as-you-go">public network IP billing</a>.</div><br> |
|Internet\-facing instance changes to private instance |* All public IP addresses associated with the instance will be automatically detached.<br><br>   * If the public IP addresses were created synchronously with the instance, these public IP addresses will be deleted.<br><br>   * If the public IP addresses were created manually, these public IP addresses will not be deleted. If you no longer need them, you can delete them manually to avoid fees.<br><br>* The instance domain name will resolve to the private IP address.<br><br>* Access to the instance from the internet will not be possible. |


<span id="4d220136"></span>
### Internet\-facing IP type

When changing a VPC ALB instance to an Internet\-facing instance, you must attach an Elastic IP Address (EIP) to the instance. Elastic IP addresses can come from the following BytePlus cloud services:


* [Elastic IP Address (EIP)](https://docs.byteplus.com/docs/eip/What-is-EIP): An EIP is a public IP resource that can be purchased independently.


<span id=".YWxi56eB572R5a6e5L6L57uR5a6a5YWs572RaXA="></span>
## Changing a VPC instance to an Internet\-facing instance

<span id="d5077be3"></span>
### Before you begin

You have created the required Elastic IP address.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Application Load Balancer console](https://console.byteplus.com/alb).

2. In the left navigation pane, click **Instance management** to enter the **Instance management** page.

3. On the **Instance management** page, click the name of the private instance to be configured.

4. On the **Basic Information** tab, in the **Network configuration** section, click **Change network type**.

5. In the **Change network type** dialog box, set the Elastic IP type and select the Elastic IP address to bind to the instance. Each instance requires an Elastic IP address in every availability zone it belongs to.

   * **Elastic Public IP**: select the EIP to bind to the instance.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After binding an Internet\-facing instance of the private ALB, the public IP type cannot be changed. Select the public IP type based on your actual usage scenario.</div>


6. After configuration, click **Confirm**.


<span id=".YWxi5YWs572R5a6e5L6L6Kej57uR5YWs572RaXA="></span>
## Change the Internet\-facing instance to a private instance

<span id="e55d6e9b"></span>
### Precautions

After changing your Internet\-facing ALB instance to a private instance, all its Elastic IP addresses will be detached and it will no longer be accessible from the internet. Exercise caution when performing this operation.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Application Load Balancer console](https://console.byteplus.com/alb).

2. In the left navigation pane, click **Instance management** to open the **Instance management** page.

3. On the **Instance management** page, click the name of the Internet\-facing instance to configure.

4. In the **Basic Information** tab, under the **Network configuration** section, click **Change network type**.

5. In the pop\-up dialog box, confirm the prompt and then click **Confirm**.
