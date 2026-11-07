---
title: "Viewing IPv4/IPv6 addresses"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Viewing-IPv4-or-IPv6-addresses"
---

This topic describes how to view the IP addresses of ECS instances.

<span id=".5p-l55yL5YiG6YWN57uZ5LqR5pyN5Yqh5Zmo55qESVDlnLDlnYA="></span>
## View the IP address assigned to an ECS instance


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the target ECS instance.

4. On the Instances page, click the name of the target ECS instance.

5. On the "Network Interface" tab, click the name of the target network interface.

6. View the IPv4/IPv6 addresses of multiple network interfaces of the ECS instance as shown in the following figure.


<span id=".5p-l55yL5LqR5pyN5Yqh5Zmo6K-G5Yir55qESVDlnLDlnYA="></span>
## View the IP address identified by an ECS instance


1. Log in to an ECS instance via remote connection.

2. Enter the IP address viewing command in the command line. For CentOS systems, execute the `ip address show` command. Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f08c60210f8f335c089fc2af9d820efc.png) </span>

3. If an IP address exception is detected, you can handle it based on the following scenarios. 

   * If the ECS instance fails to identify the mounted secondary network interface, refer to [Configuring secondary network interfaces for ECS instances](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances) for configuration.

   * If the ECS instance fails to identify the assigned IPv4 address, refer to [Configuring IPv4 addresses for ECS Instances](https://docs.byteplus.com/en/docs/ecs/Configuring-secondary-private-IPv4-addresses-for-ECS-instances) for configuration.

   * If the ECS instance fails to identify the assigned IPv6 address, refer to [Configuring IPv6 addresses for ECS Instances](https://docs.byteplus.com/en/docs/ecs/Configuring-private-IPv6-addresses-for-ECS-instances) for configuration.
