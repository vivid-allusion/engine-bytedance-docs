---
title: "Creating an allowlist"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/create-allowlist"
---

After the Cache for Redis instance is created successfully, you can set allowlist for the instance to allow devices to access the instance. This topic describes how to create allowlist via the console.

## Background information

To ensure the security and stability of the Redis database, accessing Redis instances from any IP address is not allowed by default in the system. Before using Redis instances, you need to create an allowlist and add the client's IP address or CIDR block to the allowlist of the Redis instance to allow the client to access the Redis instance. We recommend that you regularly maintain and manage the allowlist to ensure the security of accessing Redis instances.

## Precautions

* Each BytePlus account can create up to 1,000 allowlists per region.

* Each BytePlus account can allow up to one default allowlist per region. A newly created default allowlist will automatically override the existing default allowlist. That is, the existing default allowlist will automatically become a non\-default allowlist.

* Each allowlist can be associated with up to 200 instances at a time, and there is no limit to the total number of instances that can be associated.

* Each allowlist can be associated with up to 300 IP addresses or IP address segments in CIDR format.

* Each allowlist can be associated with up to 10 ECS security groups.

* Each instance can be associated with a maximum of 100 allowlists. A maximum of 100 allowlists can be associated at a time.

* Each instance can be associated with up to 1,000 IP addresses or IP address segments in CIDR format.

* If no allowlist is associated with an instance, its access is denied to all addresses.

* For data security reasons, it is not allowed to add the address `0.0.0.0/0` to the allowlist of the instance while enabling the password\-free access function. If you need to set address `0.0.0.0/0` in the allowlist, disable the instance's password\-free access feature first. To enable password\-free access, refer to [Password-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left navigation bar, choose **NoSQL Database\> Redis \> Allowlists**.

4. On the **Allowlists** page, click **Create allowlist**.

5. In the **Create allowlist** panel, set the following parameters.

   |Parameters |Description |
   |---|---|
   |Project |Select the project to be added to the allowlist from the drop\-down list. By default, the **default** project will be added.<br><br>> **tip**<br><br><br>> If you use the Redis cloud service through IAM user, you can only see the allowlist information under the projects that have been authorized for the current IAM user. For more details, refer to [Using Redis with IAM user](https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers).<br> |
   |Allowlist name |Enter the name of the allowlist, which must meet all the following requirements:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 1 to 128 characters. |
   |Description |Enter remarks on the allowlist, which must not exceed 200 characters. |
   |IP address |Enter IP addresses or IP address segments in CIDR format.<br><br>> **tip**<br><br><br><br>* > If you enter or paste an incorrect IP address or address segment, you can double\-click the IP address or address segment that needs to be modified, and then modify it to the correct IP address or address segment in the Edit IP pop\-up window.<br><br><br>* > Duplicate addresses are not allowed. Separate multiple addresses with commas (,).<br><br><br>* > Setting `0.0.0.0/0` indicates that all addresses are allowed to access. Setting `127.0.0.1` indicates that all addresses are denied access. If set both `0.0.0.0/0` and `127.0.0.1`, all addresses are allowed to access.<br><br><br>* > Setting CIDR `192.168.1.0/24` indicates that IP addresses within this network segment are allowed to access. If set `192.168.1.1`, only this IP address is allowed to access.<br> |
   |Default allowlist |Select whether to set the new creation allowlist to the default allowlist. If set as the default allowlist, it is automatically selected when creating new instances.<br><br>> **tip**<br><br><br>> Each BytePlus account can allow up to one default allowlist per region. A newly created default allowlist will automatically override the existing default allowlist. That is, the existing default allowlist will automatically become a non\-default allowlist. For more details, refer to [Constraints and limits](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2).<br> |
   |Security groups |Cache for Redis does not associate any ECS security groups with a new allowlist by default.<br><br>You can refer to the following steps to associate an ECS security group with the current allowlist:<br><br><br>1. Click **Select security group**.<br><br>2. In the pop\-up dialog box, select a security group to associate according to business needs from any security group association mode.<br><br>   Redis allowlists support the following two association modes:<br><br>   * **Associated ECS IP**: Allows cloud servers within the security group to access the database. Currently, only the IP information of the primary network card is supported for import.<br><br>   * **Inbound IP**: Allows IP addresses involved in the TCP protocol and ALL protocol in the source addresses of the inbound direction of the security group to access the database. If the source address is configured as a security group, it will be ignored.<br><br>   > **tip**<br>   <br><br>   * > When associating with a security group, you can select any one of the association modes or both of the above association modes simultaneously, but it is required to ensure that there is at least one IP or IP address segment in the associated ECS security group.<br>   <br><br>   * > Each allowlist can be associated with at most 10 ECS security groups.<br>   <br><br>   * > An allowlist supports at most 300 IPs or IP segments. If the number of IPs or IP segments involved in associating with a security group exceeds the limit, the association will fail. You can adjust the IPs in the security group and then re\-associate.<br>   <br><br>3. Click **OK**.<br><br>   > **tip**<br>   <br><br>   * > To remove selected ECS Security groups from the current allowlist, click **Disassociate** in the **Actions** column on the right side of the Security group list.<br>   <br><br>   * > After associating ECS Security groups, if the associated ECS Security groups are updated, you need to manually sync the ECS Security groups in the Redis allowlist to retrieve the latest IP list from the ECS Security groups. For specific procedures, refer to [Synchronizing security group](https://docs.byteplus.com/en/docs/redis/synchronizing_the_security_group).<br>    |

6. Click **OK**.

## Subsequent operations

After creating the allowlist, you can associate the group to the target instance. For more information on how to associate allowlists, refer to [Associating instances and allowlists](https://docs.byteplus.com/en/docs/redis/associate-allowlist).

## Relevant APIs

|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/redis/createallowlist) |Call the CreateAllowList API to create a new IP address allowlist. |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) |Call the DescribeAllowLists API to query all IP address allowlists in specified region under current account. |
