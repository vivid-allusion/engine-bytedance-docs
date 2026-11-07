---
title: "Configuring SNAT server"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Configuring-an-SNAT-server"
---

This topic shows you how to build a SNAT server to enable multiple servers to access the public network through a specified Elastic Compute Service instance.

## Background

A company builds its own SNAT server to enable all Elastic Compute Service instances without an associated public IP to access the public network through this SNAT server.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3374a37b9e08a044d5a948ab4bf5747f.png)

> **tip**

> Besides building your own SNAT server, you can also use an Internet NAT Gateway, which offers advantages such as cross\-Availability Zone disaster recovery, visualization, and easier management. For more details, see [What is an Internet NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/What-is-NAT-Gateway).

## Prerequisites

A VPC has been created with two subnets, each containing one Linux Elastic Compute Service instance. The information for the VPC, subnets, and instances matches the diagram above.

> **tip**

> Do not enable source/destination address check on the primary network interface of ECS\-A. If enabled, it cannot forward traffic for ECS\-B. For more details, see [Configuring source/destination address check](https://docs.byteplus.com/en/docs/vpc/Configuring-source-and-destination-address-check).

## Procedures

### Configure VPC route

1. Log in to the [Route Table console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/routeTable?projectName=default).

2. In the top menu bar, select the target region and project. In this example, they are China (Beijing) and default.

3. In the route table list, click the target system route table name to enter the route table details page.

4. Select the **Route Entry \> Custom route** tab, click **Add route** to open the add route entry window.

5. Add a custom route with destination CIDR block 0.0.0.0/0 and next hop as ECS\-A.

6. Click **Add** to complete configuration.

### Configure SNAT server

#### Configure IP forwarding

1. Log in to the ECS\-A. For details, see [Logging into an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the following command to open the configuration file sysctl.conf.

   `vi /etc/sysctl.conf`

3. Press `i` to enter edit mode, then add the following content to enable IP forwarding.

   `net.ipv4.ip_forward = 1`

4. Press the Esc key to exit edit mode, then press :wq to save changes and exit.

5. Run the following command to apply the configuration.

   `sysctl -p /etc/sysctl.conf`

#### Configure SNAT rule

1. On the ECS\-A command line, run the following command to open the configuration file rc.local.

   `vi /etc/rc.local`

2. Press `i` to enter edit mode, then add the following content to configure the SNAT rule.

   `iptables -t nat -A POSTROUTING -o <network interface> -s <SNAT CIDR block> -j SNAT --to <main private IP of SNAT server>`

   Example text:

   `iptables -t nat -A POSTROUTING -o eth0 -s 192.168.2.0/24 -j SNAT --to 192.168.1.11`

3. Press esc key to exit edit mode, then press :wq to save changes and exit.

4. Run the following command to grant execution permission for the rc.local file.

   `chmod +x /etc/rc.local`

5. Run a reboot command to restart the ECS instance.

6. Run the following command to verify that the SNAT configuration succeeded.

   `iptables -t nat --list`

   If the echo output contains SNAT\-related information, it indicates that the SNAT configuration succeeded, as shown below.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2149cd311568162109aabc18593f86b5.png)

### Verification

1. Log in remotely to the Elastic Compute Service (ECS\-B). For details, see [Logging into an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the following command to test whether you can access the public network.

   `ping 8.8.8.8`

   The echo output is shown below. This indicates that ECS\-B can access the public network through the SNAT service deployed on ECS\-A.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1ca11f58e33dcb6889c57099b92b7f67.png)

3. If the network is still unreachable after configuration, check whether your security group and network ACL allow the corresponding traffic.
