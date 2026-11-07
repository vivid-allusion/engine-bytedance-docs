---
title: "Migrating Alibaba Redis to BytePlus"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Migrating_Alibaba_Redis_to_Volcengine"
---

This topic describes how to use the Database Transmission Service (DTS) to migrate the Alibaba Redis to BytePlus Redis.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* DTS will occupy certain resources on the source end and the destination end when performing full data migration, which may cause the database server load to increase. If the database service volume is large or the server specification is low, it may increase the pressure on the database or even cause the database service to be unavailable. It is recommended to evaluate business pressure before performing data migration, and perform data migration during the off\-peak period of the business.

* For tasks that fail to migrate, DTS automatically recovers based on the error retry time. When you need to switch services to the target instance, be sure to end or release the task immediately to prevent the task from automatically recovering and causing the source database data to overwrite the target database data.

* In multi\-DB migration scenarios, pay attention to DB mapping between the source and target databases to avoid unintended data overwrites.

* Currently, only database migration of Redis 5 and Redis 6 versions of Alibaba cloud standard edition is supported.


<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations


|**Database type** |**Preparations** |**Description** |
|---|---|---|
|**Source** |Create an account with copy permissions |1. Log in to the Redis console of Alibaba Cloud.<br><br>2. On the left navigation bar of the **Instance information** page, click **Account management**.<br><br>3. On the **Account management** page, click **Create account**.<br><br>4. On the **Create account** panel, set the **Account**, **Permission settings**, and  **<assword**.<br><br>   The **Permission settings** must be selected as **Copy**. |
||Associate with an allowlist |1. Log in to the Redis console of Alibaba Cloud.<br><br>2. On the left navigation bar of the **Instance information** page, click **Allowlist settings**.<br><br>3. In the allowlist settings tab, click + Add allowlist group.<br><br>4. In the add allowlist group panel, add the following type of IP address as needed.<br><br>   1. (Recommended) If you only need to perform data migration, you need to add the DTS server IP address to the allowlist or security group of the database instance. DTS server IP addresses vary by region, as detailed below:<br><br>      * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.<br><br>      * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27`.<br><br>   2. If you need any address to access the instance, you can add the address `0.0.0.0/0`. Adding this address is risky and requires caution. |
||Applying for public connection address |1. Log in to the Redis console of Alibaba Cloud.<br><br>2. On the **Instance information** page, in the **Connection information** area, click **Apply for connection address** in the public network access **Action** column.<br><br>3. In the **Apply for connection address** panel, set the **Connection address** and **Port number** as required, and then click **OK**. |
||Verify that you can ping the domain name |Run the following command to verify that the domain name can be successfully pinged:<br><br>```json```<br>```ping <域名>```<br> |
||Install the CLI tool |1. Execute the following command to install the CLI:<br><br>   ```json```<br>```   wget https://download.redis.io/releases/redis-6.0.9.tar.gz```<br>```   ```<br>   <br><br>2. Run the following command to decompress the CLI:<br><br>   ```json```<br>```   tar xzf redis-6.0.9.tar.gz```<br>```   ```<br>   <br><br>3. Run the following command to enter the file for installing the CLI:<br><br>   ```json```<br>```   cd redis-6.0.9/src```<br>```   ```<br>   <br><br>4. Run the following command to compile the CLI:<br><br>   ```json```<br>```   make```<br>```   ```<br>   <br><br>5. Run the following command to install the CLI dependencies:<br><br>   ```json```<br>```   make install```<br>```   ```<br>    |
||Verifying that you can connect to the instance |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Before using CLI to verify whether the instance is successfully connected, you need to add the client IP to the instance allowlist, otherwise you will not be able to connect to the instance.</div><br><br><br><br>1. Run the following command to verify whether you can successfully connect to the instance:<br><br>   ```json```<br>```   redis-cli -h <域名> -p <端口号>```<br>```   ```<br>   <br><br>2. Run the following command for authentication:<br><br>   ```json```<br>```   auth <username> <password>```<br>```   ```<br>   <br><br>3. Run the following command to verify that the instance can receive the command:<br><br>   ```json```<br>```   dbsize```<br>```   ```<br>    |
|**Target** |* Create instance<br><br>* Set the default account and password |A database for Cache for Redis has been created, and the default account password has been set. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) and Setting the [default account password](https://docs.byteplus.com/en/docs/redis/create-manage-account). |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

Refer to [Migrating Redis connected over public network to BytePlus Cache for Redis](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_cache_for_redis_publicredis#.5pON5L2c5q2l6aqk) for the specific parameter configuration.

<span id=".57uT5p6c6aqM6K-B"></span>
## Verifying results

After the migration task is complete, select the command as needed to verify that the data has been migrated:


* Verifying full data

   You can execute the following command to verify that all data has been migrated to the target instance as required:

   ```json
   redis-cli -h <域名> -p <端口号> -a <password> info keyspace
   ```
   

* Verifying incremental data

   * Add data at the source.

   * Run the following command to verify:

      ```json
      redis-cli -h <域名> -p <端口号> -a <password> info keyspace
      ```
      

      If the newly added data from the source has been migrated to the target, the incremental migration is successfully completed.
