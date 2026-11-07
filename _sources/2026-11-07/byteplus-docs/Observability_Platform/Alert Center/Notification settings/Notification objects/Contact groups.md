---
title: "Contact groups"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Contact_groups"
---

A contact group is a collection of contacts, making it convenient to group or batch manage contacts. This topic describes how to create and manage contact groups.

<span id="BpHksifa"></span>
## Limits

Currently, you can create up to 300 contact groups.

<span id="mcGjLi1l"></span>
## Creating contact groups


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe).

2. In the left navigation pane, select "**Alert Center \-\> Notification configuration**" to go to the "Notification configuration" page.

3. On the **Notification object** tab, select **Contact group** to enter the contact group management page.

4. Click **Create contact group** and configure the relevant parameters as needed.

   
   |Parameter |Description |
   |---|---|
   |Contact group name |Specify a name for the contact group as a unique identifier. Duplicate names are not allowed. |
   |Contacts |The contacts in the current contact group. |
   


<span id="MFJULcGP"></span>
## Manage contact groups

Click a button in the "Actions" column to the right of the target contact group to perform the corresponding operation. The currently supported management operations are as follows:


|Actions |Description |
|---|---|
|Edit |Edit the configuration information of an existing contact group. |
|Delete |Delete a contact group that is no longer needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If a contact group is already associated with contacts or notification policies, deleting the contact group will also disassociate the contacts or notification policies.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If contact groups are synchronized by importing VMP notification configuration data, we recommend that you manually delete the contact groups from the VMP contact group menu in advance. Otherwise, deleted contact groups will be recreated. For more information, see <a href="https://docs.byteplus.com/en/docs/Observability_Platform/Importing_VMP_notification_configuration_data">Importing VMP notification configuration data</a>.</div><br> |
