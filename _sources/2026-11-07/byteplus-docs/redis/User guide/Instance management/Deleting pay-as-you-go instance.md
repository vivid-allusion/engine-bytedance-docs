---
title: "Deleting pay-as-you-go instance"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/delete-instance"
---

On the Redis console, you can delete unused Pay\-as\-you\-go Redis instances at any time to save resources and costs. This topic describes how to delete Pay\-as\-you\-go Redis instance.

## Prerequisite

* The instance billing method is Pay\-as\-you\-go.

* Instance deletion protection is disabled. For specific procedures, refer to [Instance deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection).

## Billing instructions

Billing for Pay\-as\-you\-go Redis instances stops immediately upon deletion. For more information about the Pay\-as\-you\-go billing type, refer to [Pay-as-you-go](https://docs.byteplus.com/en/docs/redis/pay-as-you-go).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, find the target instance, and in the **Actions** column on the right, select  **... \> Delete instance**.

   > **tip**

   > If the **Delete instance** button is grayed out and a prompt **Instance deletion protection is turned on and cannot be deleted. Click to modify** pops up, it indicates that instance deletion protection is enabled for this instance. You need to disable the deletion protection function first according to the console prompt before you can delete the instance. For specific procedures, refer to [Disable deletion protection](https://docs.byteplus.com/en/docs/redis/deletion-protection#.5YWz6Zet5a6e5L6L5Yig6Zmk5L-d5oqk).

4. In the pop\-up dialog box, confirm the instance information (such as instance ID and name) to be deleted, and set the following parameters.

   |Parameter |Description |
   |---|---|
   |Backup policy |Different types of Redis instances support different backup policies. Among them:<br><br><br>* Primary\-secondary instances: The default backup policy is **Create a final backup**, so no selection is required.<br><br>   > **danger**<br>   <br><br>   > A final backup will be created by default before deleting the instance, and it will be retained for 7 days after successful creation. We recommend that you download and save it locally, because the data will be **completely cleared** after the instance is deleted, and cannot be recovered. Please proceed with caution.<br>   <br><br>* Single\-node instances: The default backup policy is **Not create final backup**, so no selection is required.<br><br>   > **danger**<br>   <br><br>   > A single\-node instance does not support persistence and backup. No backup is created when deleting data by default. The instance data is **completely cleared** after being deleted. Please proceed with caution. For more details about single\-node instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).<br>    |
   |Backup name |Set a backup name for the final backup of the instance to be deleted Optional field. If you don't set a backup name, the backup ID will be used as the name by default.<br><br>If you want to set a backup name, the name must meet the following conditions simultaneously:<br><br><br>* It should start with a Chinese character, a letter, or an underscore (_).<br><br>* The length should be between 1 and 128 characters.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br><br>* > Only primary\-secondary instances support setting the backup name. Single node instances do not support persistence and backup functions, so no need to set this parameter.<br><br><br>* > After the backup is successfully created, you can view and download the backup on the **Backups** page. For more details, refer to [Viewin backups](https://docs.byteplus.com/en/docs/redis/view-backup).<br><br><br>* > You can also modify the backup name after the backup creates successfully. For specific procedures, refer to [Modifying backup name](https://docs.byteplus.com/en/docs/redis/modifying_the_backup_name).<br> |
   |Confirm deletion |Enter the name of the target instance for confirmation. |

5. Click **Delete**.

## Relevant APIs

|API |Description |
|---|---|
|[DeleteDBInstance](https://docs.byteplus.com/en/docs/redis/deletedbinstance) |Call the DeleteDBInstance API to delete a specified Redis instance. |
