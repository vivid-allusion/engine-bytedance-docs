---
title: "Connect to the instance via redis-cli"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/connect-instances-through-redis-cli"
---

redis\-cli is the command\-line tool that comes with the community\-native Redis. You can connect to Cache for Redis through redis\-cli on an ECS instance or local device for data management.

<span id="连接-redis-使用的网络类型"></span>
## Network type used to connect to Redis


|Network type |Description |
|---|---|
|Virtual Private Cloud |Virtual Private Cloud (VPC) is an exclusive private network. When redis\-cli is deployed on [ECS instances](https://console.byteplus.com/ecs/instance), connecting to the Redis instance through a private network provides higher security and better performance. |
|Public network |The public network refers to the internet. You can deploy redis\-cli on your local device and connect to the Redis instance via the public network for testing.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Public network access does not incur traffic fees, but compared to private network access, it has higher latency and certain security risks. It is recommended to use public network access only in testing environments, while private network access is recommended for production environments. When devices outside the VPC no longer need to access the Redis instance, it is recommended that you promptly turn off the public network access function.</div><br> |


<span id="准备工作"></span>
## Preparations

Complete relevant preparations based on the installation location of redis\-cli.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Since redis\-cli is the command\-line tool that comes with native Redis, you usually need to install Redis service on an <a href="https://console.byteplus.com/ecs/instance">ECS instance</a> or local device to complete the installation of redis\-cli. For specific installation methods, see <a href="https://docs.byteplus.com/en/docs/redis/connect-instances-through-redis-cli#%E9%99%84%E5%BD%95%EF%BC%9A%E5%AE%89%E8%A3%85-redis-cli">Appendix: Install redis\-cli</a>.</div>


* <div data-tips="true" data-tips-type="tip">The version of redis\-cli can be different from that of the Redis instance.</div>




|**Installation location of Redis\-cli** |**Actions to be executed** |
|---|---|
|[ECS instance](https://console.byteplus.com/ecs/instance) (recommended)<br><br> |1. Make sure the ECS instance and the Redis instance belong to the same VPC network.<br><br>2. Obtain the private IP address of the ECS instance.<br><br>3. Add the private IP address of the ECS instance to the allowlist of the Redis instance. For more information on how to set an allowlist, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist). |
|Local |1. Cache for Redis only provides private addresses by default. Before accessing the Redis instance from a local application, you need to enable internet access for the Redis instance. For more information on how to enable internet access, refer to [Enabling public network access](https://docs.byteplus.com/en/docs/redis/apply-public-address).<br><br>2. Open the command prompt or terminal window on your local device and use one of the following methods to obtain the public address of your local device:<br><br>   * Linux: Execute the curl ifconfig.me command in the terminal window.<br><br>   * Windows: Execute the curl ip.me command in the command prompt window.<br><br>   * MacOS:Execute the curl ifconfig.me command in the terminal window.<br><br>3. Add the public address of the local client to the allowlist of the Redis instance. For more information on how to set an allowlist, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist). |


<span id="注意事项"></span>
## Precautions

If you need to use the redis\-cli client to connect to the instance after turning on Secure sockets layer encryption, then:


* Redis\-cli versions below 6 do not support certificate verification during connection. Please use redis\-cli version 6 or above.

* Before connecting to the instance, you need to execute the `make BUILD_TLS=yes` command to compile the redis\-cli client file.

   For the method to set up Secure sockets layer encryption, see [Set up Secure sockets layer encryption](https://docs.byteplus.com/en/docs/redis/setup-ssl).


<span id="操作步骤"></span>
## Procedure


1. Log in to the device where redis\-cli is installed, e.g. [ECS instance](https://console.byteplus.com/ecs/instance) or local device.

   If redis\-cli is not installed, see [Appendix: Install redis-cli](https://docs.byteplus.com/en/docs/redis/connect-instances-through-redis-cli#%E9%99%84%E5%BD%95%EF%BC%9A%E5%AE%89%E8%A3%85-redis-cli) for installation.

2. Open the command line window or terminal tool on the local device and navigate to the redis\-cli installation directory.

   Commands to navigate to the installation directory on different operating systems are as follows:

   * Windows OS: `cd /d <redis-cli directory>`, e.g. `cd /d D:redis-6.2.13`.

   * Linux OS: `cd ../<redis-cli directory>`, e.g. `cd root/redis-6.2.13`.

   * macOS operating system: `cd ../<directory where redis-cli is located>`, e.g. `cd home/redis-6.2.13`.

3. Get the connection information and execute the following command to connect to the Redis instance. For specific methods to obtain the connection address, see [View connection address](https://docs.byteplus.com/en/docs/redis/view-address#%E6%93%8D%E4%BD%9C%E6%AD%A5%E9%AA%A4).

   ```Bash
   src/redis-cli -h <hostname> -p <port> [-c]
   ```
   

   
   |Parameter |Description |Acquisition method |
   |---|---|---|
   |`<hostname>` |Redis instance connection address |* ECS instance connects via Virtual Private Cloud: You need to obtain the private network connection address of the Redis instance.<br><br>* Local device connects via public network: You need to turn on public network access to obtain the public network connection address of the Redis instance. For the method to turn on public network access, see [Enable public network access](https://docs.byteplus.com/en/docs/redis/apply-public-address). |
   |`<port>` |Port number of the Redis instance |The default port number is 6379. |
   |`-c` |Enable cluster mode |Only Redis instances with sharding cluster enabled use this parameter. When you need to connect using a direct address, add `-c` when connecting to the instance. For more information about direct connection addresses, see [Apply for direct connection address](https://docs.byteplus.com/en/docs/redis/apply-direct-connection-address). |
   

   Examples of connection codes for different types of connection addresses are as follows. For more information about connection address types, see [Connection address type](https://docs.byteplus.com/en/docs/redis/view-address).

   * Private network address connection example

      ```Bash
      src/redis-cli -h redis-cng6qap*****.redis.ibytepluses.com -p 6379
      ```
      

   * Public network address connection example

      ```Bash
      src/redis-cli -h redis-cng6qap*****.redis.bytepluses.com -p 6379
      ```
      

   * Direct connection address connection example

      ```Bash
      src/redis-cli -h redis-cng6qap*****.redis.ibytepluses.com -p 6379 -c
      ```
      

4. Execute the `AUTH` command to complete account and password verification.

   You can choose any of the following methods to complete account and password verification:

   * Verify by entering both the account and password. The command is as follows.

      ```Bash
      AUTH <username> <password>
      ```
      

      Or

      ```Bash
      AUTH <username>:<password>
      ```
      

   * Directly enter the password for verification with the following command.

      ```Bash
      AUTH <password>
      ```
      

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only when using the default account can you directly enter the password for verification.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you forget your password, you can reset it. For specific steps, see <a href="https://docs.byteplus.com/en/docs/redis/reset-password">Reset password</a>.   </div>
   

   Example below.

   ```Bash
   AUTH testuser Test@Password
   ```
   

   After successful verification, **OK** will be returned.


<span id="后续操作"></span>
## Subsequent procedure

After completing the verification, you can first [set connection-level read/write classification policies](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting#%E8%AF%BB%E5%86%99%E5%88%86%E7%A6%BB%E7%AD%96%E7%95%A5%E8%AF%B4%E6%98%8E%E5%8F%8A%E8%AE%BE%E7%BD%AE%E5%BB%BA%E8%AE%AE) for the current connection, and then execute Redis\-related commands as needed, such as using the `DBSIZE` command to query the number of keys in the current database. For details on commands supported by Cache for Redis, see [Command support](https://docs.byteplus.com/en/docs/redis/supported-command).

<span id="附录：安装-redis-cli"></span>
## Appendix: Install redis\-cli

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When installing Redis on an ECS instance or local device, redis\-cli will be installed simultaneously. When connecting through redis\-cli, the version of redis\-cli does not need to match the version of the Cache for Redis instance.</div>


* <div data-tips="true" data-tips-type="tip">This article uses redis\-6.2.13 as an example, but you can install other versions based on your business needs. For more information, see <a href="https://redis.io/download">Redis downloads</a>.</div>


1. Log in to the device where redis\-cli will be installed, such as an ECS instance or local device.

2. Depending on the operating system of the device, choose the corresponding method to download and install redis\-cli.

   1. Linux

      * Run the following command to download the Redis source code file.

         ```Bash
         wget https://download.redis.io/releases/redis-6.2.13.tar.gz
         ```
         

      * Run the following command to extract the Redis source code file.

         ```Bash
         tar xzf redis-6.2.13.tar.gz
         ```
         

      * Execute the following commands to enter the decompressed directory and compile and install the Redis source files.

         ```Bash
         cd redis-6.2.13 && make
         ```
         

   2. Windows

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Currently only 64\-bit Windows systems are supported.      </div>
      

      1. Download the [Redis-x64-3.0.zip](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b9e98804aa55051a40add9b0df3a82bb.zip) file.

      2. Extract Redis\-x64\-3.0.zip to the target installation directory.


<span id="OWvknRI3"></span>
## FAQs

**Q: How to troubleshoot when Redis instance connection fails?** 

A: When encountering issues connecting to a Redis instance, you can try the following troubleshooting steps:


   1. Use the [Connection diagnostics](https://docs.byteplus.com/en/docs/redis/Connection_diagnostics) feature to check if the client IP address has been correctly added to the Redis allowlist.

   2. If the diagnosis passes but the connection still cannot be established, further troubleshooting is required. For specific steps, please refer to [What should I do if Redis connection fails](https://docs.byteplus.com/en/docs/redis/what-should-I-do-if-Redis-connection-fails).
