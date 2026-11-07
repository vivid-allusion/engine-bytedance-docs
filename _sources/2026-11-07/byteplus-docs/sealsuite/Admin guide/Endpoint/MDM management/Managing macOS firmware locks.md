---
title: "Managing macOS firmware locks"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-macos-firmware-locks"
---

SealSuite provides firmware lock capabilities for macOS devices to control access to macOS Recovery. By restricting recovery mode access, administrators can enhance device security and ensure organizational compliance.

<span id="8d138e9e"></span>
## Feature Overview

SealSuite categorizes firmware locks based on the macOS hardware architecture:


* **Recovery Lock**: For Apple Silicon\-based devices.

* **Firmware Password**: For Intel\-based devices.


By implementing these locks, enterprise administrators can:


* **Prevent unauthorized OS reinstallation**: Ensure users cannot enter recovery mode to reinstall the system using non\-standard enterprise images.

* **Assist IT troubleshooting**: IT personnel can use the firmware lock to access recovery mode for troubleshooting. After use, the password can be reset for continued security.

* **Facilitate device offboarding**: Securely clear firmware lock passwords when devices are sold, donated, or retired from enterprise management.

* **Monitor security audits**: Track historical operations and commands via firmware lock audit logs.


<span id="42bc7de8"></span>
## Configuring Recovery Lock (Apple Silicon)

Recovery Lock is designed for macOS devices with Apple Silicon.


* **Requirement**: Supports macOS 11.5 and above.

* **Effect**: Changes take effect immediately without requiring a reboot.


<span id="3739bc44"></span>
### Enabling Recovery Lock


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Endpoint** \> **MDM** \> **Firmware Lock**.

3. Locate the **Recovery Lock** section and click **Manage Recovery Lock**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5f4f464d37d4c1c8d4effb97c3c12aa~tplv-goo7wpa0wc-image.image) </span>

4. Configure the target **Scope**:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0723ae6a2dc4c298b95773b52bd3ee1~tplv-goo7wpa0wc-image.image) </span>

   * Select the target audience by **User** or **Device**.

   * (Optional) Enable **Exclude Object** to exempt specific devices, groups, departments, or roles.

5. Click **Enable Recovery Lock** at the bottom of the page.


<span id="cfb604aa"></span>
### Managing Recovery Lock


1. Navigate to **Endpoint** \> **MDM** \> **Firmware Lock**.

2. In the **Manage Recovery Lock** tab, available administrative actions include:

   * **Device Overview**: View a list of all Apple Silicon devices covered by the policy, including their status, the status of the last command, and update timestamps.

   * **Search & Filter**: Filter devices by keyword, recovery lock status, or command status.

   * **Data Maintenance**: Click **Refresh** for real\-time updates or **Export** the list as a local file.

   * **Individual Device Control**: In the **Actions** column, click **Manage** to:

      * Enable/Disable Recovery Lock.

      * Update the Recovery Lock password.

      * **Delete Device Record**: Permanently remove the device record (Note: This action is irreversible).

   * **Audit Logs**: Click **View Log** in the **Actions** column to view the device's firmware lock audit trail.

   * **Global Controls**: Use the toggle in the top right to enable/disable the feature globally.

   * **Password Retrieval**: Click **Search Firmware Lock Password** to retrieve a specific password using the **DID** or **Serial Number**.


<span id="6b208d08"></span>
## Configuring Firmware Password (Intel\-based)

Firmware Password is used for Intel\-based macOS devices.


* **Requirement**: Supports macOS 10.13 and above.

* **Effect**: Changes take effect only after the device is **rebooted**.


<span id="4075d115"></span>
### Enabling Firmware Password


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Endpoint** \> **MDM** \> **Firmware Lock**.

3. Locate the **Firmware Password** section and click **Manage Firmware Password**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bd1a5c2beaf41bebeb822c9d339cb6a~tplv-goo7wpa0wc-image.image) </span>

4. Define the **Target Scope** and any necessary **Exclusions**.

5. Click **Set Firmware Password** at the bottom of the page.


<span id="21d27432"></span>
### Managing Firmware Password


1. Navigate to **Endpoint** \> **MDM** \> **Firmware Lock**.

2. In the **Firmware Password** section, click **Manage Firmware Password**.

3. Available administrative actions include:

   * **Policy Monitoring**: View all Intel\-based devices subject to the policy, including their current password status.

   * **Search & Data Management**: Search by user or device, filter by status, and export list data for auditing.

   * **Device Commands**: In the **Actions** column, click **Manage** to:

      * Enable/Disable the Firmware Password.

      * Update the password.

      * Delete device records.

   * **Traceability**: Click **View Log** to view audit logs for specific devices.

   * **Password Lookup**: Use the **Search Firmware Lock Password** tool in the top right to retrieve passwords via **DID** or **Serial Number**.

   * **Scope Adjustment**: In the **Assign Scope** tab, click **Modify** at the bottom to modify your target or exclusion scopes.
