---
title: "Deleting parameter template"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/delete-parameter-template"
---

This topic describes how to delete parameter templates that are no longer in use.

## Limits

Only **Customized templates** can be deleted; **System templates** cannot be deleted.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left\-side navigation pane, select **NoSQL Database \> Redis \> Parameter templates**.

4. On the **Customized templates** tab, locate the target template to be deleted, and in the **Actions** column on the right, select  **... \> Delete**.

5. In the pop\-up dialog box, click **Delete**.

   > **warning**

   > The template cannot be recovered after deletion. Proceed with caution.

## Relevant APIs

|API |Description |
|---|---|
|[DescribeParameterGroups](https://docs.byteplus.com/en/docs/redis/describeparametergroups) |Call the DescribeParameterGroups API to query the basic information of parameter templates under the current account and region. |
|[DescribeParameterGroupDetail](https://docs.byteplus.com/en/docs/redis/describeparametergroupdetail) |Call the DescribeParameterGroupDetail API to query the detailed information of the target parameter group. |
|[DeleteParameterGroup](https://docs.byteplus.com/en/docs/redis/deleteparametergroup) |Call the DeleteParameterGroup API to delete the target parameter template. |
