---
title: "Application Management"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70064"
---

To effectively manage your BytePlus RTC applications throughout their lifecycle, you can use this guide. It provides step\-by\-step instructions for creating applications to ensure data isolation, managing user access permissions, changing application states (enabling, disabling, deleting), and securely rotating your AppKey.

> You can also create apps by calling the CreateApp API. For more information, see [CreateApp](https://docs.byteplus.com/en/docs/12/docs-74487).


<span id="creating-an-application"></span>
## Creating an application


1. Log in to the [BytePlus RTC Console](https://console.byteplus.com/rtc/listRTC).

2. Click **App management** in the left navigation bar, then click **Create app**, and follow the interface prompts to add an application.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0102f64179192e1b2ca698d37142dfd2.png) </span>

   **Project**: If you need to restrict IAM users to access and operate only specific applications, you can add the IAM users to the project associated with the application. If you do not have a project yet, you can first choose the default project and change the project after creating the application. For detailed operations, see [Managing Application Permissions](https://docs.byteplus.com/docs/byteplus-rtc/docs-70064#permissions).

   After an application is created, the console assigns it a unique AppID and AppKey.


<span id="permissions "></span>
## Managing application permissions

<span id="restricting-iam-users-to-access-only-specified-applications"></span>
### Restricting IAM users to access only specified applications

Add IAM sub\-accounts to a project to restrict their access to only the applications within that project.


1. Go to [Project](https://console.byteplus.com/iam/resourcemanage/project), and find the project associated with the application.

2. Enter the project details page, click **Permission**, and follow the prompts to add the target user.


<span id="changing-the-project-associated-with-an-application"></span>
### Changing the project associated with an application

Move the application from one project to another.


1. Go to [Project](https://console.byteplus.com/iam/resourcemanage/project), and find the project associated with the application.

2. Enter the project details page, click **Resources**.

3. In the resource list, find the target application (you can locate it by its AppID), click **Remove**, and then select the new project to move the application to.


<span id="close"></span>
## Disabling or enabling an application

When you no longer need an application, you can disable it. You can re\-enable a disabled application at any time. The change takes about one minute to apply.

The impact after disabling is as follows:


* **Users already in a room**: They can remain in the room during the deactivation period, will not be removed, and will still be billed normally.

* **Users who have created a room but have not yet joined it**: They cannot join the room during the deactivation period and can only rejoin after the application is enabled.

* **Users who have not created a room or entered any room**: During the deactivation period, new rooms cannot be created or joined. These actions can only be performed after the application is enabled.

1. (Optional) If you need to disable the application, it is recommended to dismiss any rooms that are still in use by calling [BanRoomUser](https://docs.byteplus.com/en/docs/12/docs-336038).

2. Find the application on the [Application management](https://console.byteplus.com/rtc/listRTC), and click on **Application configuration**.

3. In the **App state** bar, switch the application state to **Enbale** or **Disable**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b8e4cf85eb4032e4e27033cc6b85a1a.png) </span>


<span id="deleting-an-application"></span>
## Deleting an application

If you no longer need an application, you can delete it after disabling it. Once deleted, the application will no longer appear in the application list.

> Deleted applications will still appear in the Usage Statistics.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59e403a15fc9c5dc37de7c37d22a8369.png) </span>

<span id="change"></span>
## Changing your AppKey

Whether in development or in production environments, you need to use AppKey to generate tokens. During development, you can generate temporary tokens in the console. After going live, tokens are generated in the business server. See [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121) for details. You can choose whether to enable a secondary AppKey according to the security requirements of your project.

After activating the secondary AppKey, two AppKeys, the primary and secondary, are valid at the same time. That is, tokens generated by either of them can be used normally for RTC services. If the primary AppKey is compromised, switch to the secondary AppKey. After you migrate all your services to use the new primary AppKey, disable the original one to minimize service disruption.

Changing AppKey may have a significant impact on business after it goes live. We recommend changing AppKey only when necessary, such as when an AppKey leak occurs. Switching the primary/secondary AppKey will have the following effects:


* Tokens generated by the AppKey that has been disabled will all become invalid, and users cannot use these tokens to join a room. Before disabling the original AppKey, ensure that the AppKey used by the business server to generate tokens is valid.

* Once an AppKey is deleted, it cannot be restored.


After confirming that you need to change the AppKey, follow the steps below:


1. In [BytePlus RTC Console](https://console.byteplus.com/rtc/listRTC), find the application and click Application Configuration.

2. Click the switch button on the Secondary AppKey tab to activate the secondary AppKey. After activation, tokens generated by either the primary or secondary AppKey can be used for authentication when a user joins a room.

3. Click the switch button to switch between the primary and secondary AppKeys.

> The primary AppKey cannot be disabled or deleted. Therefore, switch between the primary and secondary AppKeys first.


4. Three days after completing the previous step, click the switch button to disable the secondary AppKey. If the account is bound to a secure mobile phone, verify the phone number after confirmation. After successful verification, disable the secondary AppKey. Tokens generated by this AppKey will all become invalid.

> Users who joined a room using a token generated by this AppKey before disabling it can stay without getting any warning messages.


5. Delete the secondary AppKey.

6. Create a new secondary AppKey and activate it according to step 2.
