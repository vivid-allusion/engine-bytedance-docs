---
title: "Deleting allowlist"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/delete-allowlist"
---

You can delete allowlists that are no longer needed. This article describes how to delete allowlist via the console.

## Prerequisites

All instances in the allowlist are disassociated from that allowlist. For specific procedures on how to disassociate instances from allowlists, refer to [Disassociating instances from allowlists](https://docs.byteplus.com/en/docs/redis/disassociate-allowlist).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left navigation bar, choose **NoSQL Database\> Redis \> Allowlists**.

4. On the **Allowlists** page, click **Delete** in the **Actions** column on the right side of the target allowlist.

5. In the pop\-up dialog box, click **OK**.

## Relevant APIs

|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/redis/describeallowlists) |Call the DescribeAllowLists API to query all IP address allowlists in the specified region under the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/redis/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of a target allowlist, including IP addresses and details of associated instance. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/redis/deleteallowlist) |Call the DeleteAllowList API to delete the target allowlist. |
