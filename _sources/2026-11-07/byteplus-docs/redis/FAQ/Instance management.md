---
title: "Instance management"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/instance-management-faq"
---

This topic summarizes the FAQs related to the instances of Cache for Redis.

### Why does the instance display "Closing"?

When a subscription instance expires or the account of a pay\-as\-you\-go instance is in arrears, the instance enters the **Closing** state. After the system handles the event, the instance enters the **Closed** status. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

### What should I do after the instance displays "Closed"?

When a subscription instance expires or the account of a pay\-as\-you\-go instance has arrears, the instance enters the **Closed** status. The instance is out of service now. Perform the following operations promptly for the **Closed** instance:

* Enable automatic renewal or manually renew the instance for an instance closed upon expiration. For specific procedures, refer to [Automatic and manual renewal](https://docs.byteplus.com/en/docs/redis/automatic-manual-renewal).

* To recharge an instance closed because the account is in arrears, visit the [Billing center](https://console.byteplus.com/finance/account-overview/) to recharge the account.

### Can I change the database version of the Redis instance? For example, can I upgrade Redis 5.0 to Redis 6.0?

Yes. You can upgrade or migrate lower version instances to higher versions using any of the following methods:

* Method 1

   You can upgrade the database version of instances using the blue\-green deployment feature, for example, upgrading Redis 5.0 to Redis 6.0. For specific procedures, refer to [Upgrading major version using blue-green deployment](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment).

   > **tip**

   > To use the major version upgrade feature, [submit a ticket](https://console.byteplus.com/workorder/create/) to technical support to apply for usage.

* Method 2

Migrate data from a low\-version instance (for example, Redis 5.0) to a high\-version instance (for example, Redis 6.0) using the DTS tool to achieve the upgrade. The specific procedures are as follows:

   1. Create a new Redis instance of the target version (such as a Redis 6.0 instance). For specific procedures, refer to [Creating instance](https://vsop-online.bytedance.net/doc/manage/detail/6293/6293/71107).

   2. Migrate the source Redis 5.0 instance to the new Redis 6.0 instance through the DTS. For specific procedures, refer to [Migrate data to a BytePlus Cache for Redis instance](https://vsop-online.bytedance.net/doc/manage/detail/6293/6390/172035).

### Why does a new instance display that some memory space is used before inserting any data?

After successfully creating Cache for Redis, some memory space must be used to maintain its own meta data.

### Why can't I delete Redis instances?

To avoid accidental instance deletion, Redis provides instance deletion protection. When the feature is enabled, the instances cannot be deleted. To delete instances, disable the instance deletion protection first. For more details, refer to [Instance deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection). For specific procedures of deleting or unsubscribing instances, refer to [Deleting instance](https://docs.byteplus.com/en/docs/redis/delete-instance) and [Unsubscribing instance](https://docs.byteplus.com/en/docs/redis/unsubscribe-instance).

### Why can't I see the instance I just created on the Redis console?

Maybe because the project of the new instance created by you is different from the project you choose to enter on the console.

When viewing an instance on the [Redis console](https://console.byteplus.com/db/region:db+cn-beijing/redis), specify the project and region of the target instance first. You can select the project and region of the instance from the drop\-down list of projects and regions in the upper\-right corner of the console.

> **tip**

* > For more information on how to specify the project of instance when creating it, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).

* > You can also change the project of the instance after it is created. For specific procedures for modifying projects, refer to [Editing project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project).

### Why doesn't the sum of the read QPS and write QPS of an instance equal the total QPS in the monitoring metrics?

Because the total QPS of Redis instances includes not only the read and write operations sent by the client to the Proxy node, but also other operations sent by the client, such as AUTH, INFO, and SELECT. They are all recorded in total QPS.

### Why is an account available after the instance is created?

To ensure data security, a default account is automatically created after creating the instance. You can directly set the default account and password when [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance). You can set a password for the default account after the instance is created. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password).

### Why are the QPS reference values of Redis instances of different specifications the same?

The data in the [product specifications](https://docs.byteplus.com/en/docs/redis/product-specification) table of Cache for Redis are all specification or performance reference values of a **single shard**. Due to the native single\-threaded mechanism of Redis, there is little difference in the read and write performance of QPS of normal keys in a single shard. Therefore, the QPS reference values of single shards of Redis instances of different specifications are the same.

### Why does an insufficient permission error still occur when the IAM user uses the allowlist, parameter template, event center, and operation log functions of Redis under a project, even if the IAM user has been granted the RedisFullAccess policy under such project?

Some cloud resources are only effective globally and not within a specified project. Since some cloud resources only take effect at the global level and do not support taking effect within specified projects. Therefore, when IAM users use the Redis cloud service and the scope of the `RedisFullAccess` or `RedisReadOnlyAccess` policy granted to the IAM user is **project permissions**. To ensure that the IAM user can use the corresponding Redis functions normally, you also need to grant the IAM user the relevant permissions at the global level. For more details, refer to [Using Redis with IAM user](https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers).

### Why can't the subnets under this private network be found when creating a Redis instance after modifying the project to which a private network belongs?

You can specify a project when you create a VPC, but you cannot specify a project when you create a subnet, which is by default under the same project as the VPC to which it belongs. The project changes of the VPC and the subnet are independent, that is, modifying the project to which the VPC belongs will not modify the project of the subnet under the current VPC at the same time. For more details, refer to [Managing projects](https://docs.byteplus.com/en/docs/vpc/Managing-projects).

Therefore, if the project to which a VPC belongs is modified, you also need to change the project of the subnets under the VPC accordingly to ensure the consistency of the projects to which they belong. Otherwise, when IAM user with non\-global privileges creates a cloud resource (such as Cache for Redis), it will not be able to select a subnet or anomalies will be reported. For specific procedures for modifying projects, refer to [Editing project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project).
