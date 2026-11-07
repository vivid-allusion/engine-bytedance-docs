---
title: "Usage process"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/usage-process"
---

Cache for Redis is a database compatible with Redis 5.0, 6.0, and 7.0. This topic introduces you to the overall process for creating, configuring, and connecting to BytePlus Cache for Redis instances. It will help you quickly get started using Cache for Redis instances.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparation


* A BytePlus account has been registered with real name authentication completed. For account registration and real name authentication, refer to [Create account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account) and [Verify account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* You have already created a VPC and subnets. To create a VPC and subnets, refer to [Create VPC and subnet](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC#.5q2l6aqk5LiA77ya5Yib5bu6VlBD5Y-K5a2Q572R).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


|Procedure |Description |
|---|---|
|[1. Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance) |The first step for using Cache for Redis is to determine the instance architecture, instance specification, instance version, and configuration. |
|[2. Setting account](https://docs.byteplus.com/en/docs/redis/create-manage-account) |Set the account and password used to connect to the instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Cache for Redis supports password\-free access in a VPC. After enabling password\-free access, you can directly access the Redis instance via a private address or direct address without entering a password. To enable password\-free access, refer to <a href="https://docs.byteplus.com/en/docs/redis/pwd-free-access">Password\-free access</a>.</div><br> |
|[3. Setting allowlist](https://docs.byteplus.com/en/docs/redis/set-allowlist) |Add the IP addresses of external devices that need to connect to the instance to the allowlist. Only devices in the allowlist can access the instance. |
|[4. Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-instance-via-private-address) |Select the private network or internet access mode to connect to the instance. You can connect via VPC, direct address, or public address.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Cache for Redis provides a private address by default. To connect instances through private networks, refer to <a href="https://docs.byteplus.com/en/docs/redis/connect-instance-via-private-address">Connecting to instance via private address</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Cache for Redis also supports connecting to instances via a direct address or public address. To connect to an instance, refer to <a href="https://docs.byteplus.com/en/docs/redis/connect-instance-via-public-address">Connecting to instance via public address</a> and <a href="https://docs.byteplus.com/en/docs/redis/connect-instance-through-direct-connection-address">Connecting to instance through direct connection address</a>.</div><br> |
