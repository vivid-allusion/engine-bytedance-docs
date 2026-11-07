---
title: "Client-side custom permission management"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Client_permissions_management"
---

The root account needs to add members and set roles for sub\-accounts within the team before members can manage or access services within the application.

## Background

The root account is assigned the super administrator role by default in APMPlus. It has the privilege to add members and set their roles as administrators or members. The permissions for each role are as follows:

|Role |Permissions |
|---|---|
|Super administrator |Add or remove members, as well as their apps and services, and read and write permissions for all apps and services. |
|Administrator |Add or remove apps and services for all members, and read and write permissions for all apps and services. |
|Member |ead and write permissions or read\-only permissions for the selected applications and services are supported and can be configured as needed. |

## Limits

* Currently, client\-side monitoring provides two authorization management systems: IAM permission management and custom permission management. **IAM permission management is recommended**. In addition, the same user is subject to only one permission system, and the priority of IAM permission management is higher than that of the custom one. For example, when the same user is configured with both permission systems at the same time, only the IAM authorization takes effect.

* Cross\-account authorization is not supported.

* The permission management described in this topic is an independent permission system of APMPlus and is not based on IAM.

## Prerequisites

To create a sub\-account.

## Procedure

1. Log in to the [RUM console](https://console.byteplus.com/observe/apmplus-client) as a root user.

2. Click **Account permission control** in the upper\-right corner.

3. Click **Add member**, select the sub\-account and the permissions to grant to the sub\-account, and then click **Confirm**.

   Parameter description:

   |Parameter |Description |
   |---|---|
   |Sub\-account |Select a sub\-account. Multiple options can be selected. |
   |Role |Select the role to assign to the sub\-account.<br><br><br>* **Administrator**: When selecting the administrator role for a sub\-account, there is no need to select apps and services. They default to all apps and services.<br><br>* **Member**: When selecting the member role for a sub\-account, you need to manually select the apps and services visible to the sub\-account. |
   |Readable and writable apps |Select the apps that can be read and written. Multiple selections are supported.<br><br><br>* The app can be left blank and specified later.<br><br>* The option **All applications** indicates not only all current apps, but also those added later. Selected sub\-accounts will have the permissions assigned by their roles. |
   |Readable apps |Select readable apps. Multiple selection is supported.<br><br><br>* The app can be left blank and specified later.<br><br>* The option **All applications** indicates not only all current apps, but also those added later. Selected sub\-accounts will have the permissions assigned by their roles. |
   |Service |Select services. Multiple selections are supported.<br><br><br>* Services can be left blank and specified later.<br><br>* The option **All services** includes not only all current services, but also those added later. Selected sub\-accounts will have the permissions assigned by their roles.<br><br>* The selected services take effect only when they are activated for the app.<br><br>   For example, if sub\-account "Member" is assigned the member role, and app A and all services are selected for this account, but only RUM is activated for app A, then sub\-account "Member" will only have read and write permissions for RUM.<br><br>   If app A later activates the WebPro monitoring service, sub\-account "Member" will also simultaneously have read and write permissions for WebPro monitoring. |
