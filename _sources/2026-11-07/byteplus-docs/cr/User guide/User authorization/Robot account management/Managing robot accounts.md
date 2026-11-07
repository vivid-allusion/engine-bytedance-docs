---
title: "Managing robot accounts"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Manage_robot_accounts"
---

This topic describes how to edit, delete, disable, or reset the password of a robot account.

<span id="mmjtSYpX"></span>
## Disable/enable robot accounts

After disabling, the robot account will be temporarily unavailable, and all push and pull operations using this robot account will fail. After enabling, normal use is restored.


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar, click **Robot account**.

3. In the **Actions** column of the target robot account, click **disable** (or **enable**).

4. In the confirmation dialog box, click **confirm** to complete the operation.


<span id="slEWIiHW"></span>
## Reset password


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar, click **Robot account**.

3. In the **Actions** column of the target robot account, click **Reset password**.

   * **Automatic generation**: After you click **Confirm**, the password is generated automatically. The automatically generated password is displayed only once. Save it properly.

   * **Manual input**: Enter a password manually. The password must contain upper and lower case letters, and at least one digit or special character. The length must be 8 to 20 characters.

4. In the confirmation dialog box, click **confirm** to complete the operation.


<span id="bQL0j4N4"></span>
## Edit robot account


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar, click **Robot account**.

3. In the Actions column of the target robot account, click  **...**   **\> edit**.

4. Modify the robot account parameters. For parameter description, see [Create tag immutability rule](https://docs.byteplus.com/en/docs/cr/create-a-version-immutable-rule?lang=en)

5. Click **confirm** to complete the operation.


<span id="MeMVyFz3"></span>
## Delete robot account

You can delete currently unused robot accounts to free up quota slots.


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar, click **Robot account**.

3. In the Actions column of the target robot account, click  **...**  \> Delete.

4. Click **confirm** to complete the operation.
