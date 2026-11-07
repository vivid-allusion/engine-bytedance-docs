---
title: "Creating contact groups"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-contact"
---

When you configure an alert policy or event rule, if you want notifications to be received by email, phone number, or SMS message, you must associate an alert contact group, which consists of one or more contacts. This topic describes how to create a contact group.

## Limits

Currently, you can create up to 300 contact groups.

## Procedure

1. Log in to the [Cloud Monitor console](http://console.volcengine.com/observe/cloud-monitor/overview).

2. In the left navigation bar, click **Notification \> Notification policy**.

3. On the **Notification object** tab, select **Contact group** to enter the contact group management page.

4. Click **Create contact group** and configure the relevant parameters as needed.

   |Parameter |Description |
   |---|---|
   |Contact group name |Specify a name for the contact group as a unique identifier. Duplicate names are not allowed. |
   |Contacts |The contacts in the current contact group. |

## Validate results

After you create the alert contact group, you can click **Notification \> Notification policy \> Notification object** to view the contact group information. The **Number of contacts** column displays the number of contacts included in the current contact group. If the displayed information is a hyphen (\-) or `0`, no contacts have been added to the current contact group. You can click **Manage contacts** in the Actions column to add contacts.

## Manage contact groups

Click a button in the "Actions" column to the right of the target contact group to perform the corresponding operation. The currently supported management operations are as follows:

|Actions |Description |
|---|---|
|Edit |Edit the configuration information of an existing contact group. |
|Delete |Delete a contact group that is no longer needed.<br><br>> **warning**<br><br><br><br>* > If a contact group is already associated with contacts or notification policies, deleting the contact group will also disassociate the contacts or notification policies.<br><br><br>* > If contact groups are synchronized by importing VMP notification configuration data, we recommend that you manually delete the contact groups from the VMP contact group menu in advance. Otherwise, deleted contact groups will be recreated. For more information, see [Importing VMP notification configuration data](https://docs.byteplus.com/en/docs/Observability_Platform/Importing_VMP_notification_configuration_data).<br> |
