---
title: "Migrating Huawei cloud distributed cache service DCS standalone or primary/standby instance data to BytePlus using DTS"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Migrating_Huawei_cloud_distributed_cache_service_DCS_standalone_"
---

This topic describes how to use BytePlus's Database Transmission Service (DTS) to migrate instance data from Huawei Cloud's Distributed Cache Service (DCS) standalone or primary/standby instances to BytePlus.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* This topic is only applicable to migrating Huawei Cloud instances of the standalone and primary/standby instance types.

* DTS will occupy certain resources on the source end and the destination end when performing full data migration, which may cause the database server load to increase. If the database service volume is large or the server specification is low, it may increase the pressure on the database or even cause the database service to be unavailable. It is recommended to evaluate business pressure before performing data migration, and perform data migration during the off\-peak period of the business.

* For tasks that fail to migrate, DTS automatically recovers based on the error retry time. When you need to switch services to the target instance, be sure to end or release the task immediately to prevent the task from automatically recovering and causing the source database data to overwrite the target database data.

* In multi\-DB migration scenarios, pay attention to DB mapping between the source and target databases to avoid unintended data overwrites.

* Huawei Cloud DCS's Redis 4.0, Redis 5.0, and Redis 6.0 versions do not support binding elastic IPs, so they can not be directly accessed through the public network.


<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations


|**Database type** |**Preparations** |**Description** |
|---|---|---|
|**Source** |Enable `psync` and `sync` commands |You need to submit a ticket to the Huawei Cloud console to enable the `psync` and `sync` commands for the target instance. |
||Release the `0.0.0.0/0` CIDR block |1. Log in to the ECS console of Huawei Cloud.<br><br>2. On the top menu bar, select the region.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The region must be consistent with the region of the target instance to be migrated on Huawei Cloud.   </div><br>   <br><br>3. In the left navigation pane, click **Security group**.<br><br>4. On the **Security group** page, click **Create security group**.<br><br>5. In the **Create security group** panel, configure the following parameter information:<br><br>   * **Name**: Custom security group name.<br><br>   * **Enterprise project**: It is recommended that the project be consistent with the project of the target instance to be migrated on Huawei Cloud.<br><br>   * **Template**: Select **Open all ports** from the drop\-down list.<br><br>6. Click **OK**. |
||Creating ECS |1. Log in to the ECS console of Huawei Cloud.<br><br>2. On the top menu bar, select the region.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The region must be consistent with the region of the target instance to be migrated on Huawei Cloud.   </div><br>   <br><br>3. In the left navigation pane, click **Elastic Cloud Server**.<br><br>4. On the **Elastic Cloud Server** page, create a cloud server. Some parameters are as follows:<br><br>   * **Availability zone**: It is recommended that the availability zone be consistent with that of the target instance to be migrated on Huawei Cloud.<br><br>   * **Image**: We recommend that you select **Public image Centos**, and we recommend that you select **Centos 7.9 64bit(40GiB)**  for the version.<br><br>5. Click **Next: Network configuration**.<br><br>6. On the network configuration wizard page, configure the parameters. Some parameters are as follows:<br><br>   * **Network**: Select the virtual private cloud where the instance is located from the drop\-down list; otherwise, the network will not be connected.<br><br>   * **Security group**: The security group must select the security group created when the `0.0.0.0/0` network segment is open.<br><br>   * **Bandwidth**: Set the bandwidth based on actual conditions.<br><br>7. Click **Next: Advanced configuration**.<br><br>8. On the **Advanced configuration** configuration wizard page, configure the parameters.<br><br>9. Click **Next: Confirm configuration**.<br><br>10. On the **Confirm configuration** configuration wizard page, configure the parameters, and then click **Buy now**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Enterprise project proposal selection and instance under the same project.</div><br> |
||Log in to ECS |1. After successfully creating Cloud as a Service, obtain the public IP and confirm whether the public IP address of ECS can be pinged.<br><br>2. After pinging the public network IP of the ECS, log in to the ECS. |
||Install the CLI tool |1. Execute the following command to install the CLI:<br><br>   ```json```<br>```   wget https://download.redis.io/releases/redis-6.0.9.tar.gz```<br>```   ```<br>   <br><br>2. Run the following command to decompress the CLI:<br><br>   ```json```<br>```   tar xzf redis-6.0.9.tar.gz```<br>```   ```<br>   <br><br>3. Run the following command to enter the file for installing the CLI:<br><br>   ```json```<br>```   cd redis-6.0.9/src```<br>```   ```<br>   <br><br>4. Run the following command to compile the CLI:<br><br>   ```json```<br>```   make```<br>```   ```<br>   <br><br>5. Run the following command to install the CLI dependencies:<br><br>   ```json```<br>```   make install```<br>```   ```<br>    |
||Install and configure Nginx on ECS |**Install Nginx**<br><br><br>1. Execute the following command to add Nginx to the yum source.<br><br>   ```plain```<br>```   sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm```<br>```   ```<br>   <br><br>2. Execute the following command to check whether Nginx is successfully added.<br><br>   ```plain```<br>```   yum search nginx```<br>```   ```<br>   <br><br>3. Execute the following command to install Nginx.<br><br>   ```plain```<br>```   sudo yum install -y nginx```<br>```   ```<br>   <br><br>4. Execute the following command to install the stream module.<br><br>   ```plain```<br>```   yum install nginx-mod-stream --skip-broken```<br>```   ```<br>   <br><br>5. Execute the following command to start Nginx.<br><br>   ```plain```<br>```   sudo systemctl start nginx.service```<br>```   ```<br>   <br><br>6. Execute the following command to set Nginx to run automatically at startup.<br><br>   ```plain```<br>```   sudo systemctl enable nginx.service```<br>```   ```<br>   <br><br>7. Enter the server address (ECS public IP address) in the local browser to check whether the installation is successful.<br><br>   If displayed as **Welcome to nginx!**  , it indicates that Nginx is installed successfully. |
|||**Configuring nginx**<br><br><br>1. Run the following command to open the configuration file.<br><br>   ```plain```<br>```   cd /etc/nginx```<br>```   ```<br>   <br><br>2. Run the following command to modify configuration the configuration file.<br><br>   ```plain```<br>```   vi nginx.conf```<br>```   ```<br>   <br><br>   Add the following content to the configuration file, if there are multiple Redis instances that require a public network connection, you can configure multiple servers, using the connection address proxy_pass as the instance.<br><br>   ```plain```<br>```   stream {```<br>```       server {```<br>```           listen 8081;// 监听端口```<br>```           proxy_pass redis-900ae****-a9e3-45ec-804d-17f2******.cn-north-1.dcs.myhuaweicloyd.com:6379;// Redis 实例的连接地址。```<br>```           proxy_socket_keepalive on;```<br>```           proxy_timeout 60m;```<br>```           proxy_connect_timeout 60s;```<br>```       }```<br>```   }```<br>```   ```<br>   <br><br>3. Run the following command to restart Nginx.<br><br>   ```plain```<br>```   service nginx restart```<br>```   ```<br>   <br><br>4. Execute the following command to see if the startup was successful.<br><br>   ```plain```<br>```   netstat -an```<br>```   ```<br>   <br><br>   If both ports 8080 and 8081 are listening, Nginx is successfully started.<br><br>5. Run the following command to verify that the Redis instance is connected successfully.<br><br>   ```plain```<br>```   redis-cli -h <ECS 的公网 IP> -p <监听端口号> -a <redis 实例密码>```<br>```   ```<br>   <br><br>6. Execute the following command to see the number of keys present at the source.<br><br>   ```plain```<br>```   info keyspace```<br>```   ```<br>    |
||Modify the security group of the source instance |* If the instance supports security group settings: If the instance supports security groups, the inbound and outbound rules of the security group must allow the `0.0.0.0/0` CIDR block.<br><br>* The instance does not support security group settings:<br><br>   * If no allowlist is configured, it means that all machines can access the instance.<br><br>   * If an allowlist is configured, you need to add the private and public IP addresses of the ECS to the allowlist. |
|**Target** |* Create instance<br><br>* Set the default account and password |A database for Cache for Redis has been created, and the default account password has been set. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) and [Setting a default account password](https://docs.byteplus.com/en/docs/redis/create-manage-account). |
||Connect to the instance and view the amount of data in the source database |1. Connecting to an instance. Refer to [Connecting to an instance over virtual private cloud](https://docs.byteplus.com/en/docs/redis/connect-instance-via-private-address) for detailed operations.<br><br>2. Run the following command to view the number of keys in the target.<br><br>   ```plain```<br>```   info keyspace```<br>```   ```<br>    |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

Refer to [Migrating Redis connected over public network to BytePlus Cache for Redis](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_cache_for_redis_publicredis) for the specific parameter configuration.

<span id=".57uT5p6c6aqM6K-B"></span>
## Result verification

Execute the following command to check the number of keys in the target. If all the data from the source is migrated to the target as required, the migration is successful.

```plain
info keyspace
```
