---
title: "Creating a sub-account"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-creating-iam-users"
---

To create a sub\-account for team members or applications and assign specific permissions, follow the steps in this guide. This article introduces how to create a sub\-account and grant permissions to the sub\-account.

<span id="4d6aebb7"></span>
## **Prerequisites**

Before reading this article, please make sure you have a solid understanding of the key concepts of access authorization. For details, see [Creating a sub-account ](https://docs.byteplus.com/docs/byteplus-vod/docs-creating-iam-users).

<span id="f59c2a1a"></span>
## **Procedure**


1. Sign in to the [BytePlus IAM console](https://console.byteplus.com/iam/create_user/name).

2. On the **User** page, click **Create New User**. Each IAM user represents a sub\-account.

3. Choose the creation method. You can create a user with username or phone number.

4. In the **Fill in information** section, fill in the user's basic information. You can click **Add User** to create multiple IAM users.

5. In the **Login settings** section, choose the access method and set the corresponding parameters. For account security, it is recommended to choose only one of the following access methods and avoid mixed usage:

   * **Programmatic access**: Access using an access key. When enabled, the system automatically generates a pair of AK/SK for the IAM user.

   * **Console access**: Access using a username and password. When enabled, you need to set a password and choose whether to enable multi\-factor authentication.

6. Click **Next**. On the **Permission Settings** page, perform the following operations:

   1. Choose permission policies. You can enter "vod" in the search box to search for preset policies for BytePlus VOD or create custom policies.

   2. Set the scope of the policies:

      * **Global**: The policies take effect within the current sub\-account.

      * **Specified Project**: The policies take effect within the specified project.

7. Click **Next**. Carefully review your settings, then click **Submit**. The IAM user is created.

8. (Optional) After creating the sub\-account, you can modify the user's permissions on the **User details** page.
