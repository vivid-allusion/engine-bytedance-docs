---
title: "Recoverying from a backup set"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set"
---

Cache for Redis supports restoring instances to a specified point in time through backup files. You can restore instance data to a new instance or the source instance according to service requirements.

## Prerequisites

The instance type is the **Primary\-secondary** instance. Single\-node instances do not support backup and restore functionality. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

## Precautions

During data recovery (either to a new instance or to an original instance), do not perform any read or write operations on the instance. Otherwise, the recovery may fail or the recovered data may not meet expectations.

## Billing instructions

Fees are incurred when restoring data to a new instance based on a backup set. For instance billing details, refer to [Billing overview](https://docs.byteplus.com/en/docs/redis/billing-overview).

## Restore to new instance (recommended)

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. You can choose any of the following methods to access the **Data recovery** page.

   * **Method 1**

      1. On the **Instances** page, click the target instance.

      2. On the **Summary** page, click **Backups** tab.

      3. On the **Backups** tab, under the **Basic backups** sub\-tab, click **Data recovery**.

   * **Method 2**

      1. In the left navigation bar, select **NoSQL Database \> Redis \> Backups**.

      2. On the **Backups** page, under the **Basic backups** tab, click **Restore** in the **Actions** column on the right side of the target backup.

      > **tip**

      > You can filter the target backup by the filter conditions in the upper\-right corner of the list, as well as by fields such as **Backup status**, **Instance status**, and so on in the list. For more information about backup filter conditions or fields, refer to [Viewing basic backups](https://docs.byteplus.com/en/docs/redis/view-backup#.5p-l55yL5Z-656GA5aSH5Lu9).

4. On the **Data recovery** page, configure the following parameters.

   1. First configure the following **Restore settings** related parameters.

      |Parameters |Description |
      |---|---|
      |Restore to |Select **Restore to new instance (Recommend)** . |
      |Restore method |Select **By backup set**. |
      |Backup set |1. Click![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ecf57a947f60f3a46338fe6195188449.png)icon on the right side of the text box.<br><br>2. In the **Select backup set** panel that pops up on the right, select the backup set that needs to be restored.select<br><br>   > **tip**<br>   <br><br>   > In the backup set list, backups with a backup status of **Available** are displayed by default.<br>   <br><br>3. In the lower right corner of control panel, click **OK**. |

   2. Configure the following parameters for the newly restored instance.

      |Parameters ||Description |
      |---|---|---|
      |Basic information |Instance name |Enter the instance name. Optional. If left blank, the instance ID will be used as the instance name by default. The name must meet the following requirements:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 1 to 128 characters. |
      ||Database version |Select the Redis database version. The database version of the new instance needs to be greater than or equal to the database version of the original instance in the backup file. |
      |Specification configuration |Instance type |The instance type for the new instance. The instance type of the new instance defaults to the same as the original instance, no need to select. For more details about instance types, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture). |
      ||Sharding cluster |Whether the new instance has sharding cluster enabled. The sharding cluster status of the new instance is the same as the original instance in the backup file by default, no need to select. For more details about sharding cluster enabled, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture). |
      ||Number of shard(s) |Select the number of shards for the instance with sharding cluster enabled. The number of shards for the new instance needs to be greater than or equal to the number of shards for the original instance in the backup file.<br><br>> **tip**<br><br><br>> This configuration is supported only when the **Sharding cluster** status is **Enable**.<br> |
      ||Node(s) per shard |Choose the number of nodes in each shard, where:<br><br><br>* This configuration is supported only for the Redis instances whose **Instance type** is **Primary\-secondary**. A single node instance contains 1 node fixed in each shard and there is no need to set this parameter.<br><br>* Each shard of a primary\-secondary instance contains by default 2 nodes (1 primary node and 1 secondary node), and up to 6 nodes (1 primary node and 5 secondary nodes).<br><br><br>> **tip**<br><br><br>> For nodes with a memory capacity of 256 MiB, you can create up to four nodes per account in each region by default. To adjust the purchase quota of 256 MiB nodes (maximum is 10), refer to [Account quota](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.6LSm5Y-36YWN6aKd).<br> |
      ||Node specification |Select node specification. The node specification of the new instance needs to be greater than or equal to that of the original instance in the backup file.<br><br>Cache for Redis supports various node specifications with different performance parameters such as memory and bandwidth. You can choose the specification that suits your business needs. For more details, refer to [Instance specifications](https://docs.byteplus.com/en/docs/redis/product-specification). |
      ||Specifications preview |Review and confirm the performance details of the selected specification, including total memory capacity, number of shards, number of nodes per shard, bandwidth estimation and total connections.<br><br>> **tip**<br><br><br>> It is necessary to ensure that the total memory capacity of the new instance (total capacity = single sharding capacity x number of shardings) is not less than 150% of the total memory capacity of the original instance in the backup file.<br> |
      |Availability zone and network configuration |Deployment plan |Complete the following actions based on the desired availability zone deployment scenario:<br><br><br>* Set up single availability zone deployment<br><br>   1. Select the Deployment plan as **Single availability zone deployment**.<br><br>   2. Select the required availability zone from the **Availability zone** drop\-down list.<br><br>* Set up multiple availability zone deployment<br><br>   1. Select the deployment plan as **Multiple availability zone deployment**.<br><br>   2. From the **Availability zone** drop\-down list, set the required availability zones for the primary node and each secondary node respectively.<br><br>   > **tip**<br>   <br><br>   * > If you select multiple identical availability zones, indicating that both the primary and secondary nodes are in the same availability zone, then during the instance creation, the system will automatically switch the deployment scheme to the **Single availability zone deployment** plan.<br>   <br><br>   * > Multiple availability zone deployment can improve availability, and at the same time, there may be a network delay of 2ms to 3ms.<br>   <br><br><br>For more details, refer to [Multi-availability-zone disaster recovery solution](https://docs.byteplus.com/en/docs/redis/multi-az-solution). |
      ||Virtual private cloud |Select the VPC where the instance is located from the drop\-down list.<br><br>We recommend that you connect Redis instances to ECS instances in the same VPC. Otherwise, they cannot achieve optimal communication performance. For more details, refer to [What is VPC](https://docs.byteplus.com/en/docs/vpc/What-is-VPC).<br><br>> **tip**<br><br><br><br>* > If you have not created any VPCs yet, please click **Create VPC** on the right side of the drop\-down list first. For specific procedures, refer to [Creating VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).<br><br><br>* > After the instance is successfully created, you can modify the VPC and subnet to which the instance belongs. For specific procedures, refer to [Modifying VPC or subnet](https://docs.byteplus.com/en/docs/redis/modify-vpc-or-subnet).<br><br><br>* > When you log on to the console with IAM user, you only see VPC information under the project that the IAM user belongs to. If you can't see the target VPC, confirm that IAM user is used and that IAM user has permissions on the target project resources. For more details, refer to [Using Redis with IAM user](https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers).<br> |
      ||Subnet |Select an available subnet in the current VPC from the drop\-down list.<br><br>A subnet is an IP address block within a VPC. All cloud resources in the VPC must be deployed within a subnet. The subnet allocates private IP addresses to cloud resources.<br><br>> **tip**<br><br><br><br>* > If you have not created any subnet, click **Create subnet** on the right of the drop\-down list to create a subnet. For specific procedures, refer to [Creating subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).<br><br><br>* > Subnets possess availability zone properties. The drop\-down list only shows subnets that belong to the same availability zone as the instance in the current VPC.<br><br><br>* > You can specify a project when you create a VPC, but you cannot specify a project when you create a subnet, which is by default under the same project as the VPC to which it belongs. The project changes of the VPC and the subnet are independent, that is, modifying the project to which the VPC belongs will not modify the project of the subnet under the current VPC at the same time. For more details, refer to [Managing projects](https://docs.byteplus.com/en/docs/vpc/Managing-projects).<br><br><br>* > If you change the project to which the VPC belongs, you also need to change the project of the subnets under the VPC to ensure the consistency of the projects to which they belong. Otherwise, when IAM user with non\-global privileges creates a cloud resource (such as Cache for Redis), it will not be able to select a subnet or anomalies will be reported. For specific procedures, refer to [Editing project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project).<br> |
      ||Port |You can customize the port number for private addresses. The default port is 6379. Value range: 1024 to 65535.<br><br>After creating the instance successfully, you can modify the port number of the private address. For specific procedures, refer to [Modifying port](https://docs.byteplus.com/en/docs/redis/modify-port). |
      |Account configuration |Set password |Set the `default` account password for instance. You can select **Set up now** or **Set up later** to set the account password for instance.<br><br><br>* If you select **Set up now**, you need to enter the instance password and confirm it. The password must meet the following conditions:<br><br>   * The length is 8~64 characters.<br><br>   * It contains at least two of the following: uppercase letters, lowercase letters, digits, and special characters.<br><br>   * It supports the following special characters:<br><br>      ```Plain Text```<br>```      ()`~!@#$%^&*-+=_\|{}[];<>,.?```<br>```      ```<br>      <br><br>* If you select **Set up later**, you can set the password for the root account after the instance is created. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password). You can also set a new account and password based on business requirements. For specific procedures, refer to [Creating and managing account](https://docs.byteplus.com/en/docs/redis/manage-account). |
      ||Password\-free access |Select whether to turn on the **Password\-free access** switch for the new instance.<br><br>After enabling password\-free access, when connecting to an instance through a private address or a direct connection address, there is no need to enter a password.<br><br>> **tip**<br><br><br>> After the instance is created successfully, you can also turn off the **Password\-free access** switch at any time. After turning it off, the client connections that originally used the password\-free access function will be disconnected. It is recommended that you first connect to the Redis instance using account password verification on the client before turning off the password\-free access function. For specific procedures, refer to [Password\-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).<br> |
      |Advanced configuration |Allowlist |If a default allowlist already exists when a new instance is created, the default allowlist is automatically selected for the new instance.<br><br>If the default allowlist does not exist when you create a new instance, or you need to add the new instance to another allowlist, refer to the following steps to complete the operation:<br><br><br>1. Click on the allowlists input box.<br><br>2. In the control panel pop\-up, complete the following steps based on the selected association method.<br><br>   * If you select **New allowlist**, that is, create a new allowlist and automatically associate it to the current instance, you need to:<br><br>      1. From the drop\-down list of **Affiliated project**, select the projects to be added for the new allowlist. By default, the **default** project will be added.<br><br>      2. Enter a new allowlist name, description (optional), and IP address. You can also choose to set the newly created allowlist as the default allowlist.<br><br>      3. Click **OK**.<br><br>   * If you select **Existing allowlist**, that is, associate an existing allowlist to the current instance, you need to:<br><br>      1. In the **Existing allowlist** list, select the allowlists to be associated.<br><br>         > **tip**<br>         <br><br>         > You can quickly filter out the target allowlist through the dropdown list of **Affiliated project** and the search box of **Allowlist name** above the allowlist list.<br>         <br><br>      2. Click **OK**.<br><br><br>> **tip**<br><br><br><br>* > For more information on configuring the name, description, and IP address when creating an allowlist, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist).<br><br><br>* > If you use the Redis cloud service through IAM user, you can only see the allowlist information under the projects that have been authorized for the current IAM user. For more details, refer to [Using Redis with IAM user](https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers).<br> |
      ||Project |Set the project to which the instance belongs according to your business needs. Depending on the project you have selected in the upper\-left corner of the [Redis console](https://console.byteplus.com/db/redis), perform the corresponding actions:<br><br><br>* If you select **All resources**, the **default** (**Default project**) item will be added by default to the new instance.<br><br>* If you select a specific project (for example, one you created yourself) instead of **All resources**, then the new instance will join the project by default.<br><br><br>> **tip**<br><br><br><br>* > After the instance is successfully created, you can also change the project to which the instance belongs. For example, move the instance from the current project to the target project, or move cloud resources that are not part of the project to the target project. For specific procedures, refer to [Editing project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project).<br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources. For more details, refer to [Resource management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects).<br> |
      ||Tag |Click **Add tag** and enter the tag key and tag value to add a tag to the instance. For the tag key and tag value setting rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/redis/associate-tag#.5qCH562-6K6-572u6KeE5YiZ).<br><br>A tag consists of a key\-value object that identifies cloud resources. It can help you classify cloud resources with the same characteristics (such as use, owner, or environment) for easy filtering and aggregation, so that you can easily manage cloud resources. For more details, refer to [Tag management](https://docs.byteplus.com/en/docs/redis/tag-management). |
      ||Deletion protection |You can choose to enable or disable **Deletion protection**.<br><br>Once deletion protection is enabled, the instance cannot be deleted. This is done to prevent accidental deletion. For more details, refer to [Instance deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection). |
      ||Parameter configuration |Select a parameter template for the new instance from the drop\-down list.<br><br>A default system parameter template is created for each Cache for Redis **primary\-secondary** and **single\-node** instance of each database version respectively. The template contains all the parameters and default parameter values supported by that version. You can select and apply the corresponding parameter template from the drop\-down list according to the selected database version and instance type.<br><br>> **tip**<br><br><br><br>* > The drop\-down list will only display the parameter templates with the same database version as the current instance under the current account and region. For example, if you select the database version as Redis 6.0 when creating an instance, then the drop\-down list will only display the parameter template information of all database versions of Redis 6.0 under the current account and region. For more details, refer to [Parameter template management](https://docs.byteplus.com/en/docs/redis/parameter-template-overview).<br><br><br>* > If you haven't created any customized templates yet, you can click **View parameter templates** on the right side of the drop\-down list to enter the parameter template list page for creation. For specific procedures, refer to [Creating parameter template](https://docs.byteplus.com/en/docs/redis/create-parameter-template).<br> |
      |Billing information |Billing method |You can choose between **Pay\-as\-you\-go** or **Subscription**.<br><br>If you select the billing method as **Subscription**, you need to confirm the **Purchase duration**. You can also select **Automatic renewal**, and the system will automatically renew the instance before its expiration. |

5. In the lower\-right corner of the page, click **Confirm order**.

6. Complete the subsequent steps according to the billing method you selected.

   > Description

   * > It takes about a few minutes to create an instance. You can view the newly created instance in the instance list.

   * > You can go to **Tasks** to view the corresponding task of the newly created instance (the **Task name/ID** is `CreateInstanceInner`), and check the stage and progress details of the current task. For specific procedures, refer to [Task management](https://docs.byteplus.com/en/docs/redis/task-management).

   * > Before the **Task status** of a newly created instance enters **Task success 100%**, do not perform any read or write operations on the new instance. Otherwise, it may lead to instance recovery failure or data not meeting expectations after recovery.

## Restore to original instance

> **tip**

* > If the instance has been downgraded, make sure that the **specifications** of the single shard node and the **number of shards** of the recovered instance are greater than or equal to the node specification and the number of shards of the instance in the backup file, otherwise an error will be reported when recovering.

* > Before the restoration initiates, the system will perform a full backup by default.

* > Upon initiation of the restoration, the current instance will be cleared, and the instance cannot be read or written during the restoration process.

* > After enabling data flashback, restoring to the original instance results in **automatic shut\-off and restart of data flashback**. After enabling data flashback again, recoverable point in times start from the time when the original instance is restored. For more details, refer to [Setting data flashback](https://docs.byteplus.com/en/docs/redis/set-data-flashback).

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. You can choose any of the following methods to access the **Data recovery** page.

   * Method 1

      1. On the **Instances** page, click the target instance.

      2. On the **Summary** page, click **Backups** tab.

      3. On the **Backups** tab, under the **Basic backups** sub\-tab, click **Data recovery**.

   * Method 2

      1. In the left navigation bar, select **NoSQL Database \> Redis \> Backups**.

      2. On the **Backups** page, under the **Basic backups** tab, click **Restore** in the **Actions** column on the right side of the target backup.

      > **tip**

      > You can filter the target backup by the filter conditions in the upper\-right corner of the list, as well as by fields such as **Backup status**, **Instance status**, and so on in the list. For more information about backup filter conditions or fields, refer to [Viewing basic backups](https://docs.byteplus.com/en/docs/redis/view-backup#.5p-l55yL5Z-656GA5aSH5Lu9).

4. On the **Data recovery** page, configure the following parameters.

   |Parameters ||Description |
   |---|---|---|
   |Recovery settings |Restore to |Select **Restore to original instance**. |
   ||Restore method |Select **By backup set**. |
   ||Backup set |1. Click![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ecf57a947f60f3a46338fe6195188449.png)icon on the right side of the text box.<br><br>2. In the **Select backup set** panel that pops up on the right, select the backup set that needs to be restored.<br><br>   > **tip**<br>   <br><br>   > In the backup set list, backups with a backup status of **Available** under the current instance are displayed by default.<br>   <br><br>3. In the lower right corner of control panel, click **OK**. |
   |Configuration at the backup point of the instance ||View and confirm the configuration information of the instance **at the time point of the selected backup set**, such as instance name/ID, availability zone, instance specification (including node specification, number of nodes in a single\-shard, number of shards), whether the sharding cluster has been enabled, total capacity, billing method, database version, etc. |
   |Current configuration of the instance ||View and confirm the configuration information of the instance **currently**, such as instance name/ID, availability zone, instance specification (including node specification, number of nodes in a single\-shard, number of shards), whether the sharding cluster has been enabled, total capacity, billing method, database version, etc. |

5. Click **OK** in the lower right corner of the page.

## Relevant APIs

|API |Description |
|---|---|
|[DescribeBackups](https://docs.byteplus.com/en/docs/redis/describebackups) |Call the DescribeBackups API to query the list of backup sets for target Redis instance. |
|[RestoreDBInstance](https://docs.byteplus.com/en/docs/redis/restoredbinstance) |Call the RestoreDBInstance API to restore the data in a backup set to the original Redis instance. |
