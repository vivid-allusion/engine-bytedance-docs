---
title: "Disassociating instances from allowlists"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/disassociate-allowlist"
---

If you no longer need to access the instance using devices included in the allowlist, you can disassociate the instance and the allowlist. This topic describes how to disassociate instances and allowlists through the console.

## Precautions

After instances and allowlists are disassociated, all IP addresses in the original allowlist cannot access the instances. Ensure that the IP addresses of devices that still require access to the current instance are added to other allowlists first. For more information about how to set IP allowlists, refer to [Editing allowlist](https://docs.byteplus.com/en/docs/redis/edit-allowlist).

## Procedure

### Disassociate instance from allowlist

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left navigation bar, choose **NoSQL Database\> Redis \> Allowlists**.

4. You can choose any of the following methods to disassociate the instances from a specified allowlist.

   **Disassociation method 1**

1. On the **Allowlists** page, click  **... \> Disassociate instance** in the **Actions** column on the right side of the target allowlist.

      > **tip**

      > You can quickly filter out the target allowlist in the search box in the upper right corner of the allowlist list by allowlist name, ID, description, security group, IP or IP segment.

   3. In the pop\-up panel, find the instances that need to be disassociated from the instance list, and click **Disassociate instance** in the **Actions** column on the right side.

      > **tip**

      > To disassociate multiple instances, select the instances to be disassociated from the list, and then click **Disassociate instance** in the lower\-left corner of the list.

   3. In the pop\-up dialog box, click **OK**.

   **Disassociation method 2**

1. On the **Allowlists** page, click the name of the target allowlist.

      > **tip**

      > You can quickly filter out the target allowlist in the search box in the upper right corner of the allowlist list by allowlist name, ID, description, security group, IP or IP segment.

   2. In the **List of associated instances** area of the pop\-up panel, click **Disassociate instance**.

   3. In the pop\-up panel, find the instances that need to be disassociated from the instance list, and click **Disassociate instance** in the **Actions** column on the right side.

      > **tip**

      > To disassociate multiple instances, select the instances to be disassociated from the list, and then click **Disassociate instance** in the lower\-left corner of the list.

   4. In the pop\-up dialog box, click **OK**.

### Disassociate allowlist from instance

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Security** tab.

5. Under the **Allowlist settings** sub\-tab, click **Disassociate allowlist** in the **Actions** column.

6. In the pop\-up dialog box, click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) |Call the DescribeAllowLists API to query all IP address allowlists in the specified region under the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/redis/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of a target allowlist, including IP addresses and details of associated instance. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/redis/disassociateallowlist) |Call the DisassociateAllowList API to disassociate the target instance from the specified IP address allowlist. |
