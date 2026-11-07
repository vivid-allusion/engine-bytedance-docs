---
title: "Enabling or disabling public network resolution"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/set-public-network-resolution"
---

Cache for Redis supports resolving private domain addresses to private IP addresses in a public network environment. This topic describes the procedure for enabling and disabling public network resolution.

## Background information

Cache for Redis provides various addresses for you to access instances. When accessing Redis instance using private network address, private domains must be resolved. By default, private domains can only be successfully resolved to private IP addresses within the BytePlus private network environment. However, in certain non\-production scenarios (such as directly connecting to Cache for Redis instances in a test environment, or personal devices accessing private domains), it may be necessary to resolve private domains via a public network. In such cases, you can enable the public network resolution feature for the instance. Once enabled, private domains can be successfully resolved to private IP addresses, even in a public network environment.

## Prerequisites

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* Due to the complex public network environment, the accuracy and timeliness of domain name resolution cannot be guaranteed, so this function is limited to non\-production environments. For production environments, it is strongly recommended to use a DNS Forward solution by configuring your local DNS server to forward to BytePlus DNS, where 100.96.0.2 and 100.96.0.3 are the DNS servers used by BytePlus, to achieve domain name resolution in a private network environment.

* If the error `The prefix of address already existed` occurs when enabling public network resolution, you need to modify the private address for the current instance before enabling public network resolution. For specific procedures, refer to [Modifying address](https://docs.byteplus.com/en/docs/redis/modify-address).

## Enable public network resolution

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click on the **Connectivity** tab.

5. In the **Private network Access \> Proxy private network access** card under the **Connectivity** tab, click **Enable public network resolution**.

   > **tip**

   * > After enabling public network resolution, only private addresses will be resolved to private IPs in the internet environment, and direct addresses will not be resolved.

   * > If the error `The prefix of address already existed` occurs when enabling public network resolution, you need to modify the private address for the current instance before enabling public network resolution. For specific procedures, refer to [Modifying address](https://docs.byteplus.com/en/docs/redis/modify-address).

6. In the pop\-up dialog box, confirm the private network domain name that requires public network resolution, and click **OK**.

## Disable public network resolution

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click on the **Connectivity** tab.

5. Under the **Connectivity** tab, in the **Private network access \> Proxy private network access** card, click **Disable public network resolution**.

6. In the pop\-up dialog box, click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[ModifyDBInstancePrivateDNSVisibility](https://docs.byteplus.com/en/docs/redis/modifydbinstanceprivatednsvisibility) |Call the ModifyDBEndpointPrivateDNSVisibility interface to enable or disable the public network resolution function for the target Redis instance. |
