---
title: "Releasing public network access"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/release-public-address"
---

Compared with private network access, internet access has a higher latency and involves certain security risks. We recommend that you only use it in testing environments, while private network access is recommended for production environments. When devices outside the VPC no longer need to access Redis instances, promptly disable public network access. This topic describes how to disable public network access.

## Prerequisites

Public network access is enabled for instance. For specific procedures, refer to [Applying for public network address](https://docs.byteplus.com/en/docs/redis/apply-public-address).

## Precautions

* To ensure the security of database data, after releasing the public network address, it is recommended that you delete the relevant public network IP address in the IP whitelist in a timely manner. For more information on how to set allowlist, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/redis/set-allowlist).

* After disabling public network access, the public network address is released, and applications can no longer access the Redis instance through the public network address. Ensure that the public network address configured by the application has been modified to another type of address, such as a private network address.

* After the public address is released, the EIP is automatically disassociated. However, the EIP will not be released and will still be retained and continue to be billed. If you no longer use the EIP, release it yourself. For specific operation, refer to [Releasing EIP](https://docs.byteplus.com/en/docs/eip/Releasing-an-EIP).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click on the **Connectivity** tab.

5. On the **Connectivity** tab, in the **Public network access \> Proxy public network access** area, click **Disable public network access**.

   > **danger**

   > After disabling internet access, clients cannot access Redis instances through their original public domain names and ports. Confirm your services are not using the public address to avoid unnecessary losses.

6. In the pop\-up dialog box, click **Disable**.

## Relevant APIs

|API |Description |
|---|---|
|[DeleteDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/redis/deletedbendpointpublicaddress) |Call the DeleteDBEndpointPublicAddress API to delete the public address for a specified Redis instance, that is, disable its internet access. |
