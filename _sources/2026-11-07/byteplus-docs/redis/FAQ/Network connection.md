---
title: "Network connection"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/network-connection"
---

This topic summarizes the FAQs related to the network connection of Cache for Redis.

<span id=".56eB572R5Zyw5Z2A5ZKM55u06L-e5Zyw5Z2A5pyJ5LuA5LmI5Yy65Yir77yf"></span>
### What is the difference between private network address and direct connection address?

The similarities and differences between private network addresses and direct connection addresses are shown in the table below.


|Comparison items |Private network address |Direct connection address |
|---|---|---|
|Differences |* Accessing the Redis instance through a private network address maximizes security and performance.<br><br>* A Private Link address is automatically generated when creating a Redis instance, requiring no manual application.<br><br>* Private network addresses cannot be released.<br><br>* All instance types support private network addresses. |* Direct access addresses save time by bypassing proxy request processing, theoretically reducing server response time to clients. However, this approach sacrifices advanced features like automatic load balancing and read\-write separation.<br><br>* Manual application is required before using direct access addresses to connect to instances. For application methods, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address).<br><br>* Direct access addresses can be released. For release methods, refer to [Releasing direct connection address](https://docs.byteplus.com/en/docs/redis/release-direct-connection-address).<br><br>* Only Redis instances with sharing cluster enabled support direct connection addresses. For more details about sharding cluster enabled, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture). |
|Similarities |* Both belong to private network access methods. For specific procedures, refer to [Connection address types](https://docs.byteplus.com/en/docs/redis/view-address).<br><br>* Both support modifying the port number. For specific procedures, refer to [Modifying port](https://docs.byteplus.com/en/docs/redis/modify-port). ||


<span id=".5aaC5L2V5LiL6L29LXJlZGlzLeWuouaIt-err--8nw=="></span>
### How to download Redis client?

You can go to [Redis clients](https://redis.io/clients) to select and download the client that meets your business needs.

<span id=".5Li65L2V6L-e5o6lLXJlZGlzLeWunuS-i-WQju-8jOWIm-W7uumUrueahOaXtuWAmeaPkOekuuayoeacieiupOivge-8nw=="></span>
### Why does it prompt for no authentication when creating a key after connecting to the Redis instance?

Cache for Redis uses account and password verification by default. You need to execute the `AUTH <account> <password>` command to complete the verification. For specific procedures, refer to [Connecting to instance via private network address](https://docs.byteplus.com/en/docs/redis/connect-instance-via-private-address), [Connecting to instance via direct connection address](https://docs.byteplus.com/en/docs/redis/connect-instance-through-direct-connection-address), and [Connecting to instance via public network address](https://docs.byteplus.com/en/docs/redis/connect-instance-via-public-address).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cache for Redis supports password\-free access within VPC. After enabling password\-free access, you can directly access the Redis instance without entering a password when connecting via private address or direct connection address. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/pwd-free-access">Password\-free access</a>.</div>


<span id=".5piv5ZCm5pSv5oyB5L-u5pS5LXJlZGlzLei_nuaOpeWcsOWdgOeahOWfn-WQje-8nw=="></span>
### Is it supported to modify the domain name of Redis connection address?

Yes. You can modify the domain name of Redis instance connection address (including public network connection address, private network connection address, and direct connection address). For specific procedures, refer to [Modifying address](https://docs.byteplus.com/en/docs/redis/modify-address).

<span id=".5YWs572R6K6_6Zeu55qE6buY6K6k5bim5a695LiK6ZmQ5piv5aSa5bCR77yf"></span>
### What is the default bandwidth limit for public network access?

The default bandwidth limit for public network access varies depending on the instance creation time:


* For instance created on or after May 17, 2022, the bandwidth limit for public network access will be affected by the bandwidth limit of the public IP (that is, EIP) and the shard bandwidth limit of the Redis instance. The specific rules are as follows:

   * If the EIP bandwidth limit is greater than the shard bandwidth limit of the Redis instance, the bandwidth limit for public network access will be the shard bandwidth limit of the Redis instance.

   * If the EIP bandwidth limit is less than the shard bandwidth limit of the Redis instance, the bandwidth limit for public network access will be the EIP bandwidth limit.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you are using a Redis instance with a sharding cluster enabled, the overall bandwidth limit of the instance = number of shards x single shard bandwidth limit. For more details about the single shard bandwidth limit of Redis instances, see <a href="https://docs.byteplus.com/en/docs/redis/product-specification">Instance specifications</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more details about the EIP bandwidth limit, see <a href="https://docs.byteplus.com/en/docs/eip/Limits">EIP performance limits</a>.   </div>
   

* For instance created before May 17, 2022, EIP association is not supported when enabling public network access, so the default bandwidth limit for public network access is 1Mbps.

   If you need to increase the bandwidth limit, you can choose to bind an EIP with a higher bandwidth limit when enabling public network access. Before associating an EIP, you must first associate a subnet. 


<span id=".5aaC5L2V5p-l55yLLXJlZGlzLei_nuaOpeWcsOWdgOWvueW6lOeahC1pcC3lnLDlnYA="></span>
### How to view the IP address corresponding to the Redis connection address?

You can select any of the following methods to view the IP address corresponding to the Redis connection address:


<Tabs>
<Tab zoneid="kjBmEX6CXS" title="Method 1: View through the Redis console">
<TabTitle>Method 1: View through the Redis console</TabTitle>

You can view the IP information of the instance's corresponding address on the **Instances** page or **Connection Management** tab of the Redis console (displayed by grouping **Private network access** \> **Proxy private network access**/**Direct private network access**, **Public network access** \> **Proxy public network access**).


* Instances

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_094ec987e037402dd71fc51aaf60bb1c.png) </span>

* Connectivity tab

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3bd82162fee6b1a2a9518ec95b421b8d.png) </span>


&nbsp;

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">Currently, only the private network access connection address can be viewed on the Redis console. To view the corresponding IP address of a direct connection or public network address, refer to the instructions in Method 2 or Method 3.</div>



</Tab>
<Tab zoneid="L6rtxT15Fp" title="Method 2: Query through API interface">
<TabTitle>Method 2: Query through API interface</TabTitle>

You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/redis/describedbinstancedetail) interface to query the detailed information of a specified Redis instance, including the IP address information corresponding to different connection addresses of the instance, which is the `VIP` information in the `VisitAddrs` structure of the response result.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_50a0e6ae54bdff50a5ec796bb224d0af.png) </span>


</Tab>
<Tab zoneid="oGzeXjBW6r" title="Method 3: Query through PING command">
<TabTitle>Method 3: Query through PING command</TabTitle>

You can refer to the following steps to view the IP address corresponding to the Redis connection address:


1. Get the connection address of the Redis instance. For specific procedures, refer to [Viewing address](https://docs.byteplus.com/en/docs/redis/view-address#.5pON5L2c5q2l6aqk).

2. Log in to the ECS instance where the client is located and execute the PING command in the command line.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This topic uses the redis\-cli client as an example. For redis\-cli client installation and usage, refer to <a href="https://docs.byteplus.com/en/docs/redis/connect-instances-through-redis-cli#.6ZmE5b2V77ya5a6J6KOFLXJlZGlzLWNsaQ==">Install redis\-cli</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The PING command can be used in both Windows and Linux systems.   </div>
   

   Example is as follows.

   ```Bash
   PING redis-cnlfhy3d4def5****.redis.bytepluses.com
   ```
   

   Example of return results is as follows.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_05231a045fd3e6f34fb1a3efa9a52949.png) </span>


</Tab>
</Tabs>


<span id=".cmVkaXMt6L-e5o6l5Zyw5Z2A55qE5Z-f5ZCN5oiW5a-55bqU55qELWlwLeWcsOWdgOaYr-WQpuS8muaUueWPmO-8nw=="></span>
### Will the domain name or corresponding IP address of the Redis connection address change?

Cache for Redis currently supports connecting to instances through private network addresses, direct connection addresses, or public network addresses. In some scenarios, the domain name or corresponding IP address of the instance connection address may change. Specific scenarios are shown in the table below.


|Connection address type ||Scenarios where the domain name or IP address may change |
|---|---|---|
|Private network access |Private network address |* When modifying VPC or subnet, the IP address corresponding to the private network or direct connection address will automatically change (but the domain name of the private network address or direct connection address will not change). For more details, refer to [Modify VPC or subnet](https://docs.byteplus.com/en/docs/redis/modify-vpc-or-subnet).<br><br>* If you release the direct connection address and then apply for a new one, the IP address corresponding to the newly applied direct connection address may be different from the previous one. For more details, refer to [Applying for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address).<br><br>* Manually modify the domain name and port number of the private network address or direct connection address. For specific procedures, refer to [Modifying address](https://docs.byteplus.com/en/docs/redis/modify-address) and [Modifying port number](https://docs.byteplus.com/en/docs/redis/modify-port). |
||Direct connection address ||
|Public network access |Public network address |Manually modify the domain of the public IP address. For specific procedures, refer to [Modifying address](https://docs.byteplus.com/en/docs/redis/modify-address). |


<span id=".5piv5ZCm5pSv5oyB5Li65aSa5LiqLXJlZGlzLeWunuS-i-iuvue9ruebuOWQjOeahOWfn-WQjeaIluiAhS1pcC3lnLDlnYDvvJ8="></span>
### Is it supported to set the same domain name or IP address for multiple Redis instances?

No. The domain names of different types of Redis connection addresses and the associated IP address information are explained in the table below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about Redis instance connection address types, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-address#.6L-e5o6l5Zyw5Z2A57G75Z6L">Connection address types</a>.</div>



|Connection address type |Private network address |Direct connection address |Public network address |
|---|---|---|---|
|Domain |The domain name of any connection address must be globally unique.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Redis supports modifying the connection address domain name, but the modified domain name must also be globally unique and cannot duplicate any connection address in any region of BytePlus. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/redis/modify-address">Modifying address</a>.</div><br> |||
|IP address associated with the domain |The IP address associated with the domain name must be within the IP address range allowed by the VPC to which the instance belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The system will automatically find an available IP address from the IP address range allowed by the VPC to which the instance belongs and associate it with the private or direct connection address domain name of the instance, without requiring manual setup.</div><br> ||The public IP (EIP) address associated with the domain name is unique across all regions.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can specify the EIP to be associated when turning on public network access. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/redis/apply-public-address">Applying for public address</a>.</div><br> |


<span id=".5Li65L2VLXJlZGlzLeWunuS-i-e9kee7nOWzsOWAvOi-k-WFpeOAgei-k-WHuumAn-eOh-acieaXtuS8mui2hei_h-WunuS-i-W9k-WJjeeahOm7mOiupOW4puWuve-8nw=="></span>
### Why does the network peak input/output rate of Redis instances sometimes exceed the current default bandwidth?

When your business involves writing or reading big keys, the network peak input/output rate of the instance may exceed the default bandwidth.

Assume your instance's default bandwidth is 24MB/s. If a client needs to read a 48MB key, the instance will immediately return 48MB of data (instead of splitting it into 2 seconds). The network peak output rate on the Redis monitoring alerts page will show the actual bandwidth at that moment (i.e., 48MB/s).

In the above scenario (where some requests exceed the bandwidth limit), Redis will not restrict the current big key read request but will trigger bandwidth throttling, affecting subsequent read/write requests. To help you fully understand bandwidth usage by instance, quickly locate issues related to bandwidth utilization, and avoid performance issues caused by bandwidth throttling, we recommend that you pay close attention to two performance metrics **Inbound bandwidth utilization** and **Outbound bandwidth utilization**. For more details, refer to [Efficient bandwidth usage guide](https://docs.byteplus.com/en/docs/redis/bandwidth-suggestion).

<span id="rr13XtoM"></span>
### How to troubleshoot Redis instance connection failures?

When encountering issues like inability to connect to Redis instance or temporary disconnection after connection, you can refer to the handling suggestions in [What should I do if Redis connection fails to try to resolve the issues](https://docs.byteplus.com/en/docs/redis/what-should-I-do-if-Redis-connection-fails).
