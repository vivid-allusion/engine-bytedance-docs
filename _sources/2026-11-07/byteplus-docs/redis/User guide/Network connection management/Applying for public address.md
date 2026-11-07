---
title: "Applying for public address"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/apply-public-address"
---

You can enable public network access for your Redis instance on the console, allowing devices outside the VPC to access it. This topic describes how to apply for public network access for Redis instance.

## Prerequisites

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* If you use an IAM user to apply for a public address, you need to configure the permission policies `EIPReadOnlyAccess` and `EIPFullAccess` for the IAM user. For policy configuration methods, refer to [About policies](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).

* Compared with private network access, internet access has a higher latency and involves certain security risks. We recommend that you only use it in testing environments, while private network access is recommended for production environments. When devices outside the VPC no longer need to access Redis instances, promptly disable Internet access. For instructions on how to disable internet access, refer to [Releasing public network address](https://docs.byteplus.com/en/docs/redis/release-public-address).

* Instances with the shard cluster feature disabled and direct connection mode selected can only enable public network access if proxy connection private network access is enabled.

## Billing information

* The public network address will be associated with your Elastic IP address (EIP) and charged by EIP. For more details, refer to [EIP billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

* Pay\-as\-you\-go EIPs enter the **Closed** state 2 hours after overdue payment, stopping services and restricting bandwidth. The public network address of the Redis instance will not be automatically disassociated by the system. Instead, it will be retained and follow the EIP's own lifecycle. The instance's public IP address will only be deleted when the EIP is released or manually disassociated by you. The public IP address is typically retained for more than 24 hours. If your Redis instance is associated with a Pay\-as\-you\-go EIP, you should pay close attention to your account balance and recharge in time when your balance is low, so that the public address of the instance will not be unavailable due to arrears. For more details, refer to [EIP arrears](https://docs.byteplus.com/en/docs/eip/Arrears).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click on the **Connectivity** tab.

5. In the **Connectivity** tab's **Public network access \> Proxy public network access** area, click **Enable public network access**.

6. In the **Enable public network access** pop\-up panel, select the EIPs to be associated first, and then enter the public network port number.

   > **tip**

   * > If you have not applied for any public IP yet, click **Apply for EIP** above the list. For the specific procedures, refer to [Apply for EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).

   * > Public network addresses support port numbers ranging from 1024 to 65535.

7. Click **OK**.

   > **tip**

   * > After enabling public network access, you can use the public network address to access the Redis instance. For the specific procedures, refer to [Connecting to instance via public address](https://docs.byteplus.com/en/docs/redis/connect-instance-via-public-address).

   * > Redis supports modifying connection addresses. After enabling public access, you can modify the domain name or port number of the public address. For specific procedures, refer to [Modifying connection address](https://docs.byteplus.com/en/docs/redis/modify-address) and [Modifying port number](https://docs.byteplus.com/en/docs/redis/modify-port).

## Relevant APIs

|API |Description |
|---|---|
|[CreateDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/redis/createdbendpointpublicaddress) |Call the CreateDBEndpointPublicAddress API to create the public address for target Redis instance (enable Internet access for an instance). |
