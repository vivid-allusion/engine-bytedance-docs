---
title: "Why does it prompt \"ClusterAllFailedError: Failed to refresh slots cache\" when connecting Redis?"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/err-unknown-command-readonly"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Problem phenomenon

When connecting to the Cache for Redis through the Node.js client, such error message as `ClusterAllFailedError:Failed to refresh slots cache` appears. 

<span id=".5Y-v6IO95Y6f5Zug"></span>
## Possible cause

When starting a Redis instance, the system retrieves information about all slots from the primary node and caches it. If one or more nodes in the instance fail now, or if the network connection between nodes is interrupted, the slot cache may become expired or invalid, resulting in this error `ClusterAllFailedError:Failed to refresh slots cache`. You cannot enquire about the instance.

<span id=".5aSE55CG5pa55rOV"></span>
## Solution

Refer to the solution below to deal with this error `ClusterAllFailedError:Failed to refresh slots cache`:


1. Check whether the client\-related settings meet the requirements for accessing Redis instances. Focus on the key points below:

   * Whether the client IP address or ECS IP address is added to the Redis IP address allowlist. For specific procedures, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist).

   * To access a Redis instance with a private address, make sure that the ECS instance of the client is on the same VPC as the target Redis instance. To modify the VPC, refer to [Modifying VPC or subnet](https://docs.byteplus.com/en/docs/redis/modify-vpc-or-subnet).

2. Check whether the connection code settings of a client are correct. Pay special attention to the following points:

   * Domain name and port number of address. To modify the address or its port number, refer to [Modifying address](https://docs.byteplus.com/en/docs/redis/modify-address) and [Modifying port number](https://docs.byteplus.com/en/docs/redis/modify-port).

   * Database account and password. To reset the password, refer to [Resetting Password](https://docs.byteplus.com/en/docs/redis/reset-password).

3. If the problem cannot be solved after the above check and modification, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.
