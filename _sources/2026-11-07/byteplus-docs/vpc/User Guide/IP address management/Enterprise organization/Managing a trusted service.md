---
title: "Managing a trusted service"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Enabling-trusted-service"
---

## Scenarios

A trusted service refers to a cloud service that, upon authorization from an enterprise organization integration, can access the account structure within the organization. After IPAM is enabled as a trusted service for the enterprise organization, the Resource Discovery created by the IPAM delegated admin account can leverage the enterprise organization's authorization to automatically obtain VPC resources from member accounts, enabling centralized CIDR planning and allocation management.

## Enable trusted service

### Prerequisites

The enterprise organization is enabled. Procedures

1. Use the enterprise organization admin account to log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the left\-side navigation pane, select **Trusted service management**.

3. Click **Enable trusted service**.

4. Click **Enable** to complete the action.

Once IPAM is configured as a trusted service for the enterprise organization, the system automatically creates the role [ServiceRoleForVPC](https://console.byteplus.com/iam/identitymanage/role/ServiceRoleForVPC) under all member accounts within the organization. This role is used by Resource Discovery to access VPC resources from those member accounts.

## Specify IPAM delegated admin

1. Use the enterprise organization admin account to log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the left\-side navigation pane, select **Trusted service management**.

3. Click **Configure** to the right side of **IPAM delegated admin**.

4. Click **Undelegate** on the right side of the IPAM delegated admin account.

5. Click **Undelegate** to complete the action.

## Remove IPAM delegated admin

1. Use the enterprise organization admin account to log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the left\-side navigation pane, select **Trusted service management**.

3. Click **Configure** next to **IPAM delegated admin**.

4. Click **Add proxy account**, then select the target member account as the IPAM delegated admin.

5. Click **Submit** to complete the action.

## Disable trusted service

### Prerequisites

IPAM delegated administrator has been removed, and the change has been confirmed to take effect.

### Action notes

After IPAM is de\-authorized as a trusted service for the enterprise organization, Resource Discovery will no longer be able to obtain VPC resources from member accounts.

### Procedures

1. Use the enterprise organization admin account to log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the left\-side navigation pane, select **Trusted service management**.

3. Click **Disable trusted service** to complete this action.
