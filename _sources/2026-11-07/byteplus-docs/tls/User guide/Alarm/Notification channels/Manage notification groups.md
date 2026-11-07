---
title: "Manage notification groups"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/manage_alarm_notification_groups"
---

This article describes common operations for notification groups, including viewing the notification group configuration, modifying notification groups, and deleting notification groups.

<span id=".5p-l55yL5ZGK6K2m57uE6YWN572u"></span>
## View notification group configuration


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, choose **Common Functions** \> **log alarm** \> **notification management**.

4. On the **notification management** page, under the **Notification Groups** tab, view the notification group configuration.

   The **notification management** page shows all notification group information in the current region, including group name, ID, number of notification channels, creation time, and last operation time. Click the notification group name to view its configuration details. The basic information displayed on the page includes:

   
   |Display item |Description |
   |---|---|
   |Notification group name |Name of the notification group.<br><br>Click the copy icon to quickly copy the notification group name. |
   |Notification policy |This includes notification rules and notification channels.<br><br>Notification channels include notification schedules, channel types, recipient channels, recipients, and content templates. |
   |Project |The IAM project to which the notification group belongs.<br><br>If you need to adjust the project, find the specified project in the [Project List](https://console.byteplus.com/iam/resourcemanage/project) and move resources in or out. |
   


<span id=".5L-u5pS55ZGK6K2m57uE"></span>
## Edit notification group


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Features** \> **log alarm** \> **notification management**.

4. On the **notification management** page, under the **notification group** tab, find the specified notification group, and click **Edit** in the corresponding **Actions** column.

5. Reset the notification group’s configuration and click **Save**.


<span id=".5Yig6Zmk5ZGK6K2m57uE"></span>
## Delete notification group

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Deleting a notification group does not remove the associated IAM user.</div>


* <div data-tips="true" data-tips-type="tip">After an alarm policy binds to a notification group, if the notification group is deleted, TLS will stop sending alarm notifications to that notification channel.</div>


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Functions** \> **log alarm** \> **notification management**.

4. On the **notification management** page, under the **Notification Groups** tab, find the specified notification group, then click **Delete** in the corresponding **Actions** column.

5. Confirm the notification group information to be deleted, then click **Delete**.
