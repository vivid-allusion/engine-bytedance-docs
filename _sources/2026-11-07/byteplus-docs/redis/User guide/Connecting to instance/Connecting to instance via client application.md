---
title: "Connecting to instance via client application"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/connect-instance-via-client"
---

Cache for Redis is fully compatible with the community native Redis, and the database connection method is basically the same. You can choose any client program compatible with the Redis protocol to connect. This article describes the relevant operations for connecting to a Redis instance through a client program.

<span id="准备工作"></span>
## Preparation

Complete the relevant preparations based on the deployment location of the client program.


|**Installation location of Redis\-cli** |**Actions to be executed** |
|---|---|
|[ECS instance](https://console.byteplus.com/ecs/instance) (recommended)<br><br> |1. Make sure the ECS instance and the Redis instance belong to the same VPC network.<br><br>2. Obtain the private IP address of the ECS instance.<br><br>3. Add the private IP address of the ECS instance to the allowlist of the Redis instance. For more information on how to set an allowlist, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist). |
|Local |1. Cache for Redis only provides private addresses by default. Before accessing the Redis instance from a local application, you need to enable internet access for the Redis instance. For more information on how to enable internet access, refer to [Enabling public network access](https://docs.byteplus.com/en/docs/redis/apply-public-address).<br><br>2. Open the command prompt or terminal window on your local device and use one of the following methods to obtain the public address of your local device:<br><br>   * Linux: Execute the curl ifconfig.me command in the terminal window.<br><br>   * Windows: Execute the curl ip.me command in the command prompt window.<br><br>   * MacOS:Execute the curl ifconfig.me command in the terminal window.<br><br>3. Add the public address of the local client to the allowlist of the Redis instance. For more information on how to set an allowlist, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist). |


<span id="获取连接信息"></span>
## Obtain connection information

Generally, when connecting to a Redis instance through a client program, you need to obtain the following connection information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For specific steps to view the connection address, see <a href="https://docs.byteplus.com/en/docs/redis/view-address#%E6%93%8D%E4%BD%9C%E6%AD%A5%E9%AA%A4">View connection address</a>.</div>



|Information to be obtained |How to obtain |
|---|---|
|Instance connection address |Cache for Redis supports multiple types of connection addresses. It is recommended to use a private network address for connection. For more information about connection address types, see [Connection address types](https://docs.byteplus.com/en/docs/redis/view-address). |
|Port number |Redis instances use port 6379 by default. |
|Instance account |A default administrator account named 'default' is automatically created when you create a new Redis instance. You can also create a new account and grant permissions. For more information about instance accounts, see [Create and manage accounts](https://docs.byteplus.com/en/docs/redis/manage-account). |
|Account password |You can choose any of the following methods to complete password verification:<br><br><br>* Enter both the account and password for verification. The command is as follows.<br><br>   ```Bash```<br>```   AUTH <username> <password>```<br>```   ```<br>   <br><br>   Or<br><br>   ```Bash```<br>```   AUTH <username>:<password>```<br>```   ```<br>   <br><br>* Directly enter the password for verification. The command is as follows.<br><br>   ```Bash```<br>```   AUTH <password>```<br>```   ```<br>   <br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Direct password verification is supported only when using the default account.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you forget your password, you can reset it. For specific actions, see <a href="https://docs.byteplus.com/en/docs/redis/reset-password">Reset password</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After completing verification, you can first <a href="https://docs.byteplus.com/en/docs/redis/set-read-write-splitting#%E8%AF%BB%E5%86%99%E5%88%86%E7%A6%BB%E7%AD%96%E7%95%A5%E8%AF%B4%E6%98%8E%E5%8F%8A%E8%AE%BE%E7%BD%AE%E5%BB%BA%E8%AE%AE">set connection\-level read\-write classification policies</a> for the current connection, and then execute Redis\-related commands as needed, e.g., run the <code>DBSIZE</code> command to query the number of keys in the current database. For details on commands supported by Cache for Redis, see <a href="https://docs.byteplus.com/en/docs/redis/supported-command">Command support</a>.</div><br> |


<span id="常见客户端程序"></span>
## Common client programs

For client programs supported by Redis, see [Redis Clients](https://redis.io/clients).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about the third\-party SDK client program usage instructions, see <a href="https://docs.byteplus.com/en/docs/redis/instructions-for-third-party-sdk-clients">Third\-party SDK client program usage instructions</a>.</div>


<span id="6fovXyED"></span>
## FAQs

**Q: How to troubleshoot when Redis instance connection fails?** 

A: When encountering issues connecting to a Redis instance, you can try the following troubleshooting steps:


   1. Use the [Connection diagnostics](https://docs.byteplus.com/en/docs/redis/Connection_diagnostics) feature to check if the client IP address has been correctly added to the Redis allowlist.

   2. If the diagnosis passes but the connection still cannot be established, further troubleshooting is required. For specific steps, please refer to [What should I do if Redis connection fails](https://docs.byteplus.com/en/docs/redis/what-should-I-do-if-Redis-connection-fails).
