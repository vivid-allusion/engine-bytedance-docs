---
title: "Associating instances and allowlists"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/associate-allowlist"
---

After the Cache for Redis instance is created successfully, you can set allowlist for the instance to allow devices to access the instance. This topic describes how to associate instances and allowlists through the console.

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

* During instance and whitelist associate, the instance status changes from **Network maintaining** to **Running**. After the instance becomes **Running**, the system needs some time (about 10s) to send the modified configuration to the Proxy, and the allowlist associated with the instance will take effect.

## Procedure

### Associate instances to current allowlist

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left navigation bar, choose **NoSQL Database\> Redis \> Allowlists**.

4. You can choose any of the following methods to associate instances with a specified allowlist.

   **Association mode 1**

1. On the **Allowlists** page, click **Associate instance** in the **Actions** column on the right side of the target allowlist.

      > tip

      > You can quickly filter out the target allowlist in the search box in the upper right corner of the allowlist list by allowlist name, ID, description, security group, IP or IP segment.

   2. In the pop\-up panel, check the instances that need to be added to the current allowlist.

      > **tip**

      > You can first select the project to which the instance belongs from the **Affiliated project** drop\-down list above the instance list, and then quickly filter out the target instance by instance name or ID in the search box on the right.

   3. Click **OK**.

   **Association mode 2**

1. On the **Allowlists** page, click the name of the target allowlist.

      > tip

      > You can quickly filter out the target allowlist in the search box in the upper right corner of the allowlist list by allowlist name, ID, description, security group, IP or IP segment.

   2. In the pop\-up panel, in the **List of associated instances** area, click **Associate instance**.

   3. In the pop\-up panel, check the instances that need to be added to the current allowlist.

      > **tip**

      > You can first select the project to which the instance belongs from the **Affiliated project** drop\-down list above the instance list, and then quickly filter out the target instance by instance name or ID in the search box on the right.

   4. Click **OK**.

### Associated allowlist to current instance

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Security** tab.

5. Under the **Allowlist settings** sub\-tab, click **Associate allowlist**.

6. In the control panel pop\-up, complete the following steps based on the selected association method.

   **Association method: Existing allowlist**

1. In the **Existing allowlist** list, select the allowlists to be associated with.

      > **tip**

      > You can first select the project to which the instance belongs from the **Affiliated project** drop\-down list above the instance list, and then quickly filter out the target instance by instance name or ID in the search box on the right.

   2. Click **OK**.

   **Association method: New allowlist**

1. Select the project to be added to the allowlist from the **Affiliated project** drop\-down list. By default, the **default** project will be added.

   2. Enter a new allowlist name, description (optional), and IP address.

   3. Click **OK**.

      > **tip**

      * > For more information on configuring the name, description, and IP address when creating an allowlist, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist).

      * > If you use the Redis cloud service through IAM user, you can only see the allowlist information under the projects that have been authorized for the current IAM user. For more details, refer to [Using Redis with IAM user](https://docs.byteplus.com/en/docs/redis/using_redis_with_subusers).

## Relevant APIs

|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) |Call the DescribeAllowLists API to query all IP address allowlists in the specified region under the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/redis/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of the target allowlist group, including the IP addresses and the details of associated instances. |
|[AssociateAllowList](https://docs.byteplus.com/en/docs/redis/associateallowlist) |Call the AssociateAllowList API to associate the target instance to the specified IP address allowlist. |
