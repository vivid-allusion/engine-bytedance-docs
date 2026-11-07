---
title: "Disabling/Enabling an IPv4 Gateway"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Disabling-Enabling-an-IPv4-Gateway"
---

## Disable IPv4 gateway

### Action description

Once the IPv4 Gateway is disabled, public IPv4 traffic entering or leaving the VPC will no longer be restricted by it, and routes pointing to the IPv4 Gateway in the route table will become invalid.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation tree, select **IPv4 Gateway**.

3. In the top menu bar, select your target Region.

4. Click **Disable** to the right of the target IPv4 Gateway.

5. Click **Migrate** to complete the action.

## Enable IPv4 Gateway

### Action description

Once enabled, all inbound and outbound IPv4 internet traffic for the VPC will be restricted by the IPv4 gateway.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation tree, select **IPv4 Gateway**.

3. In the top menu bar, select your target Region.

4. Click **Enable** on the right side of the target IPv4 Gateway.

5. Click **Migrate** to complete the action.

## Related documents

* [EnableIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/EnableIpv4Gateway)

* [DisableIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/DisableIpv4Gateway)
