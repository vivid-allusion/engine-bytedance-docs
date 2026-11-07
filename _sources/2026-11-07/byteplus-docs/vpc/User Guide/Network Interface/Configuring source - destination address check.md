---
title: "Configuring source/destination address check"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Configuring-source-and-destination-address-check"
---

## Scenarios

The source/destination check feature for network interfaces is disabled by default.

You can enable source/destination check on Network Interfaces to prevent spoofed packets. After enabling source/destination check for a network interface:

* The network interface denies **sending** packets with source addresses that do not match its own address.

* The network interface denies **receiving** packets with destination addresses that do not match its own address.

> **warning**

> If the ECS instance is used for services such as NAT gateways, routers, or firewalls, do not enable source/destination check on the corresponding Network Interface. Reason: These services receive, process, and forward packets based on their functionality. The destination address of received packets or the source address of forwarded packets may not match the IP address of the Network Interface itself. If source/destination check is enabled, the service will fail to operate correctly.

## Configuring source/destination address check

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top menu bar, select the target project and region.

4. Click the name of target Network Interface.

5. On the **Overview** tab in the **Basic Information** section:

   * Turn on: enable the **Source/Destination Check** switch to complete the operation.

   * Turn off: disable the **Source/Destination Check** switch to complete the operation.

## Related documents

[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes)
