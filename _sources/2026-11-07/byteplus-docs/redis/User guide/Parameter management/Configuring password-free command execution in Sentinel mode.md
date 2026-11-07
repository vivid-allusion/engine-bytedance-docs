---
title: "Configuring password-free command execution in Sentinel mode"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/password-free_execution_in_sentinel_mode"
---

Sentinel mode is a high\-availability (HA) solution provided by native Redis. Cache for Redis supports Sentinel compatible mode and password\-free command execution in Sentinel compatible mode. This topic describes how to configure password\-free command execution in Sentinel mode.

## Prerequisites

When using `SENTINEL SENTINELS` and `SENTINEL GET-MASTER-ADDR-BY-NAME` commands, the instance's proxy minor version must be greater than or equal to `1.507.1`. When using `SENTINEL SLAVES` and `SENTINEL REPLICAS` commands, the instance's proxy minor version must be greater than or equal to `1.606.1`. If your instance's proxy minor version does not meet the above requirements, first [Upgrading minor version](https://docs.byteplus.com/en/docs/redis/upgrade-minor-version).

You can view the instance's database version and minor version information under the **Summary** tab. For specific procedures, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).

## Introduction to Sentinel

Sentinel provides services such as primary\-replica node status monitoring, fault alarming, automatic failover, and providing the latest primary node address to clients, to improve system availability and reliability. Typically, Sentinel is widely used in on\-premises Redis databases with high reliability requirements. Cache for Redis supports Sentinel compatible mode, improving the convenience of database migration to the cloud in such scenarios.

> **tip**

> Cache for Redis achieves high availability through solutions such as primary\-secondary switching and multi\-availability zone deployment, without the need for Sentinel. For more details, refer to [High availability](https://docs.byteplus.com/en/docs/redis/high-availability).

## Sentinel\-related commands

Cache for Redis supports the following Sentinel\-related commands. For more details, refer to [Sentinel](https://docs.byteplus.com/en/docs/redis/Sentinel).

> **tip**

> When using the following Sentinel\-related commands in Cache for Redis, set `<master name>` as the instance ID of your Redis instance. You can view the instance ID information on the **Summary** tab. For specific procedures, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).

|**command** |**Description** |
|---|---|
|[SENTINEL SENTINELS](https://redis.io/docs/latest/operate/oss_and_stack/management/sentinel/#:~:text=SENTINEL%20SENTINELS%20%3Cmaster%20name%3E%20Show%20a%20list%20of%20sentinel%20instances%20for%20this%20master%2C%20and%20their%20state.)<br><br> |Query the Sentinel instance list of the specified Master and the status of these Sentinel instances. The command syntax is as follows.<br><br>```JSON```<br>```SENTINEL SENTINELS <master name>```<br> |
|[SENTINEL GET-MASTER-ADDR-BY-NAME](https://redis.io/docs/latest/operate/oss_and_stack/management/sentinel/#:~:text=SENTINEL%20GET%2DMASTER%2DADDR%2DBY%2DNAME%20%3Cmaster%20name%3E%20Return%20the%20ip%20and%20port%20number%20of%20the%20master%20with%20that%20name.%20If%20a%20failover%20is%20in%20progress%20or%20terminated%20successfully%20for%20this%20master%20it%20returns%20the%20address%20and%20port%20of%20the%20promoted%20replica.) |Query the IP address and port number of the specified Master. The command syntax is as follows.<br><br>```JSON```<br>```SENTINEL GET-MASTER-ADDR-BY-NAME <master name>```<br> |
|[SENTINEL SLAVES](https://redis.io/docs/latest/operate/oss_and_stack/management/sentinel/) |Retrieve the list of secondary nodes (replicas) for the specified master.<br><br>```Plain Text```<br>```SENTINEL SLAVES <master name>```<br> |
|[SENTINEL REPLICAS](https://redis.io/docs/latest/operate/oss_and_stack/management/sentinel/) |Retrieve the list of secondary nodes (replicas) for the specified master. `SENTINEL REPLICAS` is an alias for `SENTINEL SLAVES`.<br><br> <br><br>```Plain Text```<br>```SENTINEL REPLICAS <master name>```<br> |

> **warning**

## > Support for `SENTINEL SLAVES` and `SENTINEL REPLICAS` is for compatibility, aiming to ensure correct client SDK initialization. Returned results (e.g., slave addresses) may differ from native Redis Sentinel commands.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Parameters** tab.

5. On the **Parameter** sub\-tab, click **Batch modification of parameters**, find the `sentinel-passwordless-auth` parameter in the parameter list, and modify its value according to business requirements.

   You can enter the parameter name in the search bar on the right to filter.

   > **tip**

   > After setting it to `yes`, you can execute the following commands **without password** on any connection:

   * > Execute Sentinel\-related commands, including the `SENTINEL SENTINELS`, `SENTINEL GET-MASTER-ADDR-BY-NAME`, `SENTINEL SLAVES`, and `SENTINEL REPLICAS` subcommands. For more details about sentinel\-related commands, refer to [Sentinel](https://docs.byteplus.com/en/docs/redis/Sentinel).

   * > Execute the PING command.

   * > Execute the HELLO command without the `auth` parameter.

   * > Use the SENTINELcommand to listen to the `+switch-master` channel.

6. After completing the modification, click **Submit** in the upper\-left corner of the parameter list.

7. In the popped\-up dialog box, confirm the modified parameters and parameter values, and click **OK**.

## Subsequent operations

* After setting the `sentinel-passwordless-auth` parameter to `yes`, you can connect to the instance and run the `SENTINEL SENTINELS <master name>` command without password to test it. A successful execution indicates that the instance allows password\-free execution of Sentinel\-related commands.

* To use more password\-free commands, enable the aforementioned password\-free parameter and then add an additional list of password\-free commands by setting the `extra-passwordless-auth-command` parameter. For more details, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter).

* Sentinel compatibility mode does not provide additional connection addresses; you can connect using Redis public and private network access addresses. For specific procedures, refer to [Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance).

## Relevant APIs

|API |Description |
|---|---|
|[DescribeDBInstanceParams](https://docs.byteplus.com/en/docs/redis/describedbinstanceparams) |Call the DescribeDBInstanceParams API to query the list of supported parameters for target Redis instance. |
|[ModifyDBInstanceParams](https://docs.byteplus.com/en/docs/redis/modifydbinstanceparams) |Call the ModifyDBInstanceParams API to modify the parameter configuration of target Redis instance. |
