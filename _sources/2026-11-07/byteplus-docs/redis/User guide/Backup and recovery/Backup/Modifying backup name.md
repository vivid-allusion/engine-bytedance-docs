---
title: "Modifying backup name"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifying_the_backup_name"
---

Backups created through the automatic backup policy, as well as backups created manually without a set name, all use the backup ID as the backup name by default. You can modify the default backup name to a specified name on the Redis console, which makes it convenient to quickly filter out the specified backup from the backup list according to the backup name later.

## Prerequisite

* The instance type is the **Primary\-secondary** instance. Single\-node instances do not support backup and restore functionality. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

* Backups have been created either automatically or manually, and the backup status is **Available**. For more details on the backup status, refer to [Backup status](https://docs.byteplus.com/en/docs/redis/view-backup).

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

   You can choose any of the following methods to find the target backup.

   * **Method 1**

      1. On the **Instances** page, click the name of the target instance.

      2. On the instance details page, click **Backups**.

      3. On the **Backups** tab, under the **Basic backups** sub\-tab, you can filter out the target backup according to the start and end times in the upper right corner of the backup list.

   * **Method 2**

      1. In the left navigation bar, select **NoSQL Database \> Redis \> Backups**.

      2. Under the **Basic backups** sub\-tab of the **Backups** page, you can filter out the target backup through the filtering conditions in the upper right corner of the list, as well as fields such as **Backup status** and **Instance status** in the list.

   > **tip**

   > For more information about backup filtering conditions or fields, refer to [Viewing backups](https://docs.byteplus.com/en/docs/redis/view-backup).

3. Place the mouse over the name of the target backup, and an ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) icon will automatically appear on the right side of the backup name. Click the ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png) icon.

4. In the popped\-up text box, enter a new backup name.

   > **tip**

   > The name needs to meet the following conditions simultaneously:

   * > It should start with a Chinese character, a letter, or an underscore (_).

   * > The length should be 1 to 128 characters.

   * > It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).

5. Click **OK**.
