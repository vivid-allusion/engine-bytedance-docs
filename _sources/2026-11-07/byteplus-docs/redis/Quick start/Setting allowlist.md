---
title: "Setting allowlist"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/set-allowlist"
---

After creating a Redis instance, all IP addresses are denied access to the instance by default. This topic explains how to manually add client IP addresses or CIDR blocks to the allowlist to permit access to the Redis instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* Whether accessed over a private network (i.e., VPC) or a public network, you will need to configure the instance's allowlist in order to connect to the instance.

* Regularly maintain the allowlist by removing the IP addresses of devices that no longer need to access the Redis instance to ensure the security of database connections.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Each BytePlus account can create up to 1,000 allowlists per region.

* Each BytePlus account can allow up to one default allowlist per region. A newly created default allowlist will automatically override the existing default allowlist. That is, the existing default allowlist will automatically become a non\-default allowlist.

* Each allowlist can be associated with up to 200 instances at a time, and there is no limit to the total number of instances that can be associated.

* Each allowlist can be associated with up to 300 IP addresses or IP address segments in CIDR format.

* Each allowlist can be associated with up to 10 ECS security groups.

* Each instance can be associated with a maximum of 100 allowlists. A maximum of 100 allowlists can be associated at a time.

* Each instance can be associated with up to 1,000 IP addresses or IP address segments in CIDR format.

* If no allowlist is associated with an instance, its access is denied to all addresses.


<span id=".5a6e5L6L5Yib5bu65pe257uR5a6a55m95ZCN5Y2V"></span>
## Associate allowlist during instance creation

You can associate Redis instances with allowlists during instance creation, so that clients in the allowlist can access the instance. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).

<span id=".5a6e5L6L5Yib5bu65ZCO57uR5a6a55m95ZCN5Y2V"></span>
## Associate allowlist to existing instance

For specific procedures, refer to [Associating allowlist to current instance](https://docs.byteplus.com/en/docs/redis/associate-allowlist#.5pa55rOV5LqM77ya57uR5a6a55m95ZCN5Y2V6Iez5b2T5YmN5a6e5L6L).

<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/redis/createallowlist) |Call the CreateAllowList API to create a new IP address allowlist. |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) |Call the DescribeAllowLists API to query all IP address allowlists in the specified region under the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/redis/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of a target allowlist, including IP addresses and details of associated instance. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/redis/modifyallowlist) |Call the ModifyAllowList API to modify the setting of a target allowlist (allowlist name, allowlist IP address, etc.). |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/redis/associateallowlist) |Call the AssociateAllowList API to associate the target instance to the specified IP address allowlist. |
