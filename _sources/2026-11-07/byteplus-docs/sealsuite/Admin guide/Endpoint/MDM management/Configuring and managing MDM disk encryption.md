---
title: "Configuring and managing MDM disk encryption"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-and-managing-mdm-disk-encryption"
---

This document provides a detailed guide on enabling and configuring the Disk Encryption feature within SealSuite MDM.

<span id="507eb3eb"></span>
## Feature Overview

The Disk Encryption feature in SealSuite MDM is designed to protect sensitive data stored on mobile devices from unauthorized access and potential data breaches. By encrypting data at rest, the system ensures that information remains unreadable to unauthorized users even if a device is lost or stolen. SealSuite utilizes advanced encryption algorithms (such as FileVault for macOS and BitLocker for Windows) to provide a transparent encryption process that does not interfere with the user's daily operations.

<span id="e2dcdb6b"></span>
## Configuring Disk Encryption


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Endpoint** \> **MDM** \> **Disk Encrypt**

3. In the top left corner of the **Disk Encrypt** page, select the target operating system (**macOS** or **Windows**).

4. Click **Enable Disk Encrypt** to open the configuration page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71d40ce8891c4ffe987fb1c8bf175d1e~tplv-goo7wpa0wc-image.image) </span>

5. Define the target **Scope** (by User or Device) and specify any **Exclusion Objects**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08382b16abcf4820bc723844b5017a6e~tplv-goo7wpa0wc-image.image) </span>

   * Once the scope is finalized, the disk encryption policy is activated.

   * The final effective scope is calculated as: **Target Scope \- Exclusion Objects**.

6. Click **Confirm** to deploy the policy.


<span id="1fd5959a"></span>
## Disabling Disk Encryption


1. On the **Disk Encrypt** page, select the target operating system (**macOS** or **Windows**).

2. In the top left corner, click **Disable**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e2d4732b2b142bc8b4ac6aca0c7d39d~tplv-goo7wpa0wc-image.image) </span>

3. Confirm the action in the pop\-up dialog.

   * **Note**: After disabling, unencrypted devices will no longer be automatically encrypted. However, you can still retrieve the recovery keys for devices that were previously encrypted under this policy.


<span id="581d8277"></span>
## Re\-enabling Disk Encryption


1. On the **Disk Encrypt** page, select the target operating system (**macOS** or **Windows**).

2. In the top left corner, click **Enable**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/940948e4666f462e9d1a6c700a95fb4c~tplv-goo7wpa0wc-image.image) </span>

3. Disk encryption will be immediately reactivated for the defined scope.


<span id="427e7d4a"></span>
## Exporting Disk Encryption Data


1. On the **Disk Encrypt** page, select the target operating system (**macOS** or **Windows**).

2. In the top right corner, click **Export**.

3. The system will generate and download a CSV file containing disk encryption status and details.

   * **Security Warning**: Handle exported files with extreme caution to prevent the accidental leakage of sensitive recovery keys.


<span id="849c7853"></span>
## Retrieving Recovery Keys

If a user is locked out of their device, administrators can retrieve the recovery key through the following steps:


1. On the **Disk Encrypt** page, click **Disk Recovery Key** in the top right corner.

2. On the search page, enter the **Device DID** and the **Device Serial Number**.

3. The system will display the corresponding recovery key for the specified device.
