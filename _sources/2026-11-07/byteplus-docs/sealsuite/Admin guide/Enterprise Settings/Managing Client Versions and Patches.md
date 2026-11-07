---
title: "Managing Client Versions and Patches"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-versions"
---

SealSuite provides comprehensive client lifecycle management, enabling administrators to keep enterprise endpoints secure and up\-to\-date. Depending on business needs—such as feature iterations, security compliance, or emergency fixes—updates can be delivered via **Full Installers** or **Incremental Patches**.


* **Full Installer**: Ideal for initial deployment, major feature updates, or version migrations. Supports unified release and grayscale (canary) upgrades across all major platforms.

* **Incremental Patch**: Designed for hotfixes and localized optimizations. By deploying lightweight patches, administrators can perform immediate maintenance on specific versions without requiring users to reinstall the client, significantly reducing operational friction.


<span id="660cb287"></span>
## Releasing a Full Installer

Administrators should obtain client installers for various operating systems from the [Client Download Page](https://docs.byteplus.com/en/docs/sealsuite/downloding-the-sealsuite-client) and manually upload them to the Admin Console. Once published, a download portal is generated for employee self\-service.


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Enterprise** **Settings** \> **Versions**.

3. On the **Installation Package** tab, click  **+ New Version**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23bdef640555404c91454282c50e2fc7~tplv-goo7wpa0wc-image.image) </span>

4. Configure the following settings in the dialog box:

   * **Installation Package Information**

      
      |**Configuration** |**Description** |
      |---|---|
      |**OS** |Select the target operating system for the installer. |
      |**Software version** |Choose one of two methods:<br><br><br>* **Upload Package**: Upload the installer from your local machine.<br><br>* **Enter the Download Link**: Provide a direct URL. Refer to the [Download Guide](https://docs.byteplus.com/en/docs/sealsuite/downloding-the-sealsuite-client) or contact technical support for links.<br><br><br>**Note**: Do not modify the file name, as this allows the system to automatically parse the version number. |
      |**Version Number** |Automatically parsed after upload. You can customize the version using at least 3 digits:<br><br><br>* **3\-digit (xyz)** : Formatted as `x.y.z` (e.g., `210` becomes V2.1.0).<br><br>* **4\-digit (xyzw)** : Formatted as `x.y.zw` (e.g., `2010` becomes V2.0.10). *Example: V2.1.0 \> V2.0.10 \> V2.0.7.*  |
      |**Build Number** |Distinguishes between identical version numbers. This is appended to the package name. If version numbers match, the higher Build Number indicates the newer version (e.g., `r10989` in the package name). |
      

   * **Upgrade Policy**

      Defines the trigger logic and target audience. You can select one or more policies. If a user is assigned multiple policies, the priority is: **Silent Update** \> **Forced UI Prompt** \> **Dismissible UI Prompt**.

      
      |**Policy** |**Description** |**Common Parameters** |
      |---|---|---|
      |**Silent Update** |Updates automatically in the background without user intervention. (Not supported on Android/iOS). |* **Device and user scope**: Select **Full** or specify by **Users/Devices**. To appear on the "Initial Promotion" page, the scope must be **Full**.<br><br>* **Version scope**: Specify which legacy versions should be upgraded.<br><br>* **Pop\-up message**: Customize descriptions for prompt\-based strategies. |
      |**Pop up prompt, users can close** **it** |Users receive an upgrade notification pop\-up that can be manually closed. ||
      |**Forced pop\-up window, users cannot close it** |Users receive a mandatory notification that cannot be closed. They must upgrade to continue using the client. (Not supported on Android/iOS). ||
      

5. Set the **Release Status** to **Enabled** and click **Confirm**.


<span id="111ef2de"></span>
## Releasing a Patch (Hotfix)

Use patches for emergency fixes or localized optimizations for desktop clients. Patches are delivered via incremental updates ("Hotfixes") and do not require reinstallation. Obtain hotfix patches from SealSuite technical support.


* **Supported Clients**: Windows, macOS, and Linux (v3.2.16 and above).

* **Precision**: Ensure the patch file matches the target client version exactly.

* **Urgency**: For critical component fixes, the "Forced UI Prompt" strategy is recommended.

1. Log in to the Admin Console.

2. In the left navigation pane, go to **Enterprise** **Settings** \> **Versions**.

3. On the **Patch Package Management** tab, click  **+ New Version**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ddbeb7e73bb477594409c8f60d3774e~tplv-goo7wpa0wc-image.image) </span>

4. Configure the following settings in the dialog box:

   * **Patch package information**

      
      |**Configuration** |**Description** |
      |---|---|
      |**OS** |Select the target operating system for the patch. |
      |**Software version** |Upload the patch file or enter a download link obtained from the technical support.<br><br>**Note**: Do not modify the file name. |
      |**Version Details** |**App Version**, **Build ID**, and **Patch Version** are automatically parsed and displayed after upload. |
      |**Package MD5** |(Optional) If provided, the client performs an MD5 verification before applying the patch.<br><br><br>* **Windows**: `certutil -hashfile [filename] MD5`<br><br>* **macOS**: `md5 [filename]` |
      

   * **Upgrade Rule**

      Defines the trigger logic and target audience. You can select one or more policies. If a user is assigned multiple policies, the priority is: **Silent Update** \> **Forced UI Prompt** \> **Dismissible UI Prompt**.

      
      |**Policy** |**Description** |**Common Parameters** |
      |---|---|---|
      |**Silent Update** |Updates automatically in the background without user intervention. (Not supported on Android/iOS). |* **Device and user scope**: Select **Full** or specify by **Users/Devices**. To appear on the "Initial Promotion" page, the scope must be **Full**.<br><br>* **Version scope**: Specify which legacy versions should be upgraded.<br><br>* **Pop\-up message**: Customize descriptions for prompt\-based strategies. |
      |**Pop up prompt, users can close** **it** |Users receive an upgrade notification pop\-up that can be manually closed. ||
      |**Forced pop\-up window, users cannot close it** |Users receive a mandatory notification that cannot be closed. They must upgrade to continue using the client. (Not supported on Android/iOS). ||
      

5. Set the **Release Status** to **Enabled** and click **Confirm**.


<span id="f97121c9"></span>
## Version Management and Maintenance

<span id="858024a8"></span>
### Lifecycle Operations

For any created version (whether a Full Installer or an Incremental Patch), administrators can perform the following management tasks within the version list:


|**Operation** |**Description and Logic** |
|---|---|
|**Go Online / Offline** |* **Online**: Activates the version's upgrade policy. The system begins distributing the installer or patch to all endpoints within the defined target scope.<br><br>* **Offline**: Suspends the distribution policy. Once offline, terminals logging in will no longer receive update notifications for this version. Terminals that have already installed the update are unaffected. |
|**Edit** |Allows modifications to the upgrade strategy, target scope, and descriptive metadata for the current version. Changes take effect for subsequent update requests. |
|**Rollback** | **(Patch Management Only)**  Used to urgently withdraw a patch that is causing operational issues. Rolling back a patch removes the configuration from the system, and the client reverts to its state prior to the patch installation.<br><br>**Important Constraints**:<br><br><br>1. **Version Eligibility**: Rollback is only permitted for the **currently online patch with the highest version number** for a specific [App Version + Build ID]. For example, if patches `1.0.1`, `1.0.2`, and `1.0.3` are all online for the same client version, only `1.0.3` can be rolled back. Once `1.0.3` is rolled back, the historical patches `1.0.2` and `1.0.1` **remain ineligible** for rollback.<br><br>2. **Re\-activation**: A patch in the "Rolled Back" state must be **Edited** and saved before it can be set to "Online" again. |
|**Delete** |Permanently removes the version record from the management console.<br><br>**Risk Warning**: Deletion is irreversible. Once deleted, target terminals can no longer retrieve or update to this version. It is strongly recommended to take a version **Offline** first to verify that there is no negative business impact before final deletion. |


<span id="302b3929"></span>
### Installation and Verification

After publishing a version or patch, administrators can monitor the distribution health through global analytics or verify status at the individual client level.


* **Global Monitoring (Admin Console)** 

   Using the real\-time data dashboard, administrators can track distribution quality and use integrated troubleshooting tools to locate anomalous endpoints.

   
   |**Monitoring Metric** |**Business Context and Verification Role** |**Diagnostic Integration** |
   |---|---|---|
   |**Installed Count / Ratio** |Measures whether the file has been successfully delivered and extracted to the terminal's local disk. If this number is lower than expected, check for concurrency bottlenecks or network environment issues. |Click the **numerical value** to jump to the **Asset List**. The system will automatically apply a filter for devices with failed installation status for that version, allowing for rapid troubleshooting. |
   |**Activated Count / Ratio** | **(Patch Only)**  Measures whether the patch logic has been successfully loaded and is actively running. If the "Activated" count is significantly lower than the "Installed" count, it typically indicates the patch has been delivered but the terminal has not yet restarted. Use a prompt\-based policy to remind users. |Click the **numerical value** to jump to the **Asset List**. The system will automatically apply a filter for devices where the patch is installed but not yet effective, facilitating targeted follow\-up. |
   

* **Individual Verification (Client\-Side)** 

   During troubleshooting or random audits, you can guide users to the **Setting** page in the SealSuite client to verify the version status:

* **Full Installer Verification**: Check the **App Version** in the "About" section. Verify the version number and Build Number against the released version in the Admin Console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1750919085924fc0b8d34fae81039b85~tplv-goo7wpa0wc-image.image) </span>

* **Patch Verification**: Check the **Patch Version** in the "About" section to confirm it matches the hotfix version you published.


<span id="8dd09560"></span>
## General Configuration

<span id="6f4cc00d"></span>
### Concurrency and Bandwidth Throttling

To prevent large\-scale updates from exhausting server bandwidth, configure global download limits.


1. On the **Versions** page, click **Concurrency and Speed Limit** in the top right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9005e25971714e588b1a034c870d18ee~tplv-goo7wpa0wc-image.image) </span>

2. Set the following parameters:

   * **Number of concurrent devices upgrade**: The maximum number of terminals allowed to download simultaneously. Recommended to be ≤ 1% of the total terminal count.

   * **Speed limit for device upgrade**: The maximum bandwidth allocated per device (Default: 500 KB/s).


<span id="d7b9b1e0"></span>
### Distribution Portals

SealSuite provides two distinct portals for client acquisition based on deployment stage and security requirements.


1. Navigate to the **General Settings** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3fe5cfbc9354eb49ce5aecf9b68322e~tplv-goo7wpa0wc-image.image) </span>

2. Select the appropriate distribution address:

   
   |**Portal Type** |**Access Requirement** |**Logic and Use Case** |
   |---|---|---|
   |**Initial Promotion** |No Login Required |Used for new hire onboarding or contractor access.<br><br>**Note**: Installers will only appear here if their upgrade policy scope is set to **Full**. |
   |**Standard Download** |Login Required |Used for ongoing self\-service updates by existing employees. After logging in, the portal displays the latest authorized versions based on the user's account scope. |
   

* **URL Management**: To reset the download portal URLs, click **Configure** to navigate to the **Company General** page and perform the reset.

* **Integrated Configuration**: On the "Company General" page, you can also manage **Root Certificates** and **Privacy Policies**. Ensure these are configured before initiating a large\-scale rollout.


<span id="1a6fcbfe"></span>
### Global Installation Statistics

Track version coverage across the entire organization using the global dashboard under the **General Settings** tab.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2866c1d1908347fe81e417c1e76236c0~tplv-goo7wpa0wc-image.image) </span>


* **Multi\-dimensional Filtering**: Use the dropdown to view distribution by OS (Windows, macOS, Linux, etc.).

* **Data Drill\-down**: Click a version bar in the chart to see the exact number of installations.

* **Diagnostic Link**: Click the **Number of installations** to jump to the **Asset List**, where you can see the specific devices running that version.
