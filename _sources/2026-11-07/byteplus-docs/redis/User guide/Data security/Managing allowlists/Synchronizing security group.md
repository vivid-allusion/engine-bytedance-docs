---
title: "Synchronizing security group"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/synchronizing_the_security_group"
---

Cache for Redis supports associating ECS security groups in the allowlist. If the associated ECS security group has been updated, you can manually synchronize the ECS security group in the Redis allowlist to obtain the latest IP list in the ECS security group. This topic describes the procedure for synchronizing the security group.

## Prerequisites

* The ECS security group has been created. For specific procedure, refer to [Creating security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

* The ECS security group has been associated with the Redis allowlist. You can associate the ECS security group when creating or editing the allowlist. For specific procedure, refer to [Creating allowlist](https://docs.byteplus.com/en/docs/redis/create-allowlist) or [Editing allowlist](https://docs.byteplus.com/en/docs/redis/edit-allowlist).

* If the allowlist associated with the security group has been bound to an instance, the status of all instances in the allowlist needs to be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* After confirming the synchronization of the security group, the Cache for Redis will automatically identify the IP changes in the security group associated with the allowlist and update the IP information in the allowlist (such as adding or reducing IPs). Confirm whether the removal of the reduced IPs from the allowlist affects the business.

* An allowlist supports a maximum of 300 IPs or IP segments. If the IPs or IP segments involved in the associated security group exceed the limit, the synchronization will fail (that is, none of the IPs involved in this task will be synchronized). You can adjust the IPs in the security group and resynchronize.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left navigation bar, choose **NoSQL Database\> Redis \> Allowlists**.

4. On the **Allowlists** page, find the target allowlist and click  **... \> Sync security group** in the **Actions** column of the target allowlist.

5. In the popped\-up dialog box, confirm the IP changes before and after synchronization (such as added or reduced IPs or IP segments), and click **OK** after confirming that there are no errors.

## Relevant APIs

|API |Description |
|---|---|
|[CreateAllowList](https://docs.byteplus.com/en/docs/redis/createallowlist) |Call the CreateAllowList API to create a new IP address allowlist. |
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) |Call the DescribeAllowLists API to query all IP address allowlists in the specified region under the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/redis/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of a target allowlist, including IP addresses and details of associated instance. |
|[ModifyAllowList](https://docs.byteplus.com/en/docs/redis/modifyallowlist) |Call the ModifyAllowList interface to modify the target allowlist information (such as allowlist name, IP address, whether it is set as the default allowlist). |
