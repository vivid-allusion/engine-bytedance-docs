---
title: "Managing Windows patches and repairs"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-windows-patches-and-repairs"
---

The Patch Management function enables you to manage Windows vulnerability patches, set up auto\-remediation rules, and view relevant statistics.

<span id="Usage scenario"></span>
# Usage scenario

This comprehensive management solution facilitates vulnerability discovery and repair for all Windows devices in your organization. Enabling patch management can prevent vulnerability calculation caused by server\-level upgrades, reducing unnecessary bandwidth usage. Customizing auto\-remediation rules based on your organization's security requirements can improve the efficiency of vulnerability repair. You can monitor the overall status of current device vulnerability repair through different views and manually repair devices as needed.

<span id="Enabling patch management"></span>
# Enabling patch management


1. Log in to the Admin Console.

2. In the left navigation bar, select **Endpoint** \> **Endpoint Control** \> **Patch Management**.

3. In the upper right corner of the **Patch** **Management** page, click **Disabled Patch Management**.

   The patch management switch is disabled by default.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/851e690d336f48ef87695666217e95bf~tplv-goo7wpa0wc-image.image) </span>

4. In the **Enable Patch Management** dialog box, click **OK**.

   With the patch management function enabled, SealSuite will automatically collect vulnerabilities on Windows devices upon their login to SealSuite.


<span id="Configuring auto-remediation rules"></span>
# Configuring auto\-remediation rules


1. Log in to the Admin Console.

2. In the left navigation bar, select **Endpoint** \> **Endpoint Control** \> **Patch Management**.

3. Click **Configure** at the top of the **Patch** **Management** page or **Configure** in the **Active Remediation Rules** area.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d0085d29915476d90fc8f9f7d3f648d~tplv-goo7wpa0wc-image.image) </span>

4. Under the **Auto\-Remediation Rules** tab, enable auto\-remediation rules of different levels.

   The **Add effective scope** page will appear after a rule is enabled.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0fdc69424fe4a729d3dd733d6ad0073~tplv-goo7wpa0wc-image.image) </span>

5. In the **Add effective scope** page, configure **Employee** or **Device** on which the rule will take effect and click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a5cf48de2cb4ede99683f044e4e3d15~tplv-goo7wpa0wc-image.image) </span>

6. (Optional) Under the **Allowlist** **settings** tab, configure **Employee** or **Device** on which rules won't take effect and click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f132a852157042159b04663b06761f80~tplv-goo7wpa0wc-image.image) </span>

7. (Optional) Under the **General** **Settings** tab, click **Edit** to configure the fields with detailed information in the table below, and click **Confirm** to save any changes made.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ada492e7b29045c58bc09cd1a4fc30fc~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Delayed installation of new patches** |To mitigate potential risks associated with newly released patches, a rule can be set to delay their installation. This feature enables automatic installation of patches after a specified number of days, ranging from 0 to 30. It is recommended to set the delay to 5 days. |
   |**Patch installation concurrency** |Control the number of devices that can install patches concurrently. Choose **No** **control** for no limit or set the maximum number of devices that can install patches concurrently per minute, ranging from 1 to 50. |
   |**Installation failed retry** |Choose whether to retry patch installation after a failed attempt. Select **Do not retry** for no retries or set a specific number of retry times. |
   |**Patch Blocklist** |* Exclude specific patches from being installed on users' devices by clicking **Add** **new** to add them based on their Windows KB numbers. Multiple selections are supported.<br><br>* In the **Action** column, click **Remove** to remove patches and allow them to be installed on users' devices. |
   


<span id="Viewing vulnerability statistics"></span>
# Viewing vulnerability statistics


1. Log in to the Admin Console.

2. In the left navigation bar, select **Endpoint** \> **Endpoint Control** \> **Patch Management**.

3. At the top of the **Patch** **Management** page, select **Global** **View** or **Rule** **View** to view the table below for information on vulnerability statistics and fixes.

   * **Global view**: Displays vulnerability statistics and fixes for all devices in a consolidated manner.

   * **Rule View**: Displays vulnerability statistics and fixes only for devices with configured auto\-remediation rules.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65482ee588f24aa8b8193da9e17064fd~tplv-goo7wpa0wc-image.image) </span>

   
   |**Information Area** |**Description** |
   |---|---|
   |**Vulnerability Remediation Summary** |This section showcases monthly and cumulative repair progress for all non\-allowlist Windows devices or devices with the rule in effect.<br><br>The bug fix rule in effect is displayed on the right side, with greyed\-out icons indicating rules not in effect. |
   |**Vulnerability Statistics** |This section displays the number of vulnerabilities and trends over time for all non\-allowlist Windows devices or devices with the rule in effect. Vulnerability statistics can be viewed by **Vulnerabilities** or **Devices**. |
   |**Vulnerability List** |This section provides a comprehensive overview of each vulnerability, including its name, severity level, release and update dates, status, and the number of devices impacted. Some of the fields are described below:<br><br><br>* **Repaired**: Indicates that all devices affected by the vulnerability have been patched.<br><br>* **To be repaired**: Indicates that the patch to fix the vulnerability has been released but has not yet been installed. The installation time can be checked under the corresponding vulnerability.<br><br>* **Repairing**: Indicates that patches are currently being automatically installed on the device.<br><br>* **Not repaired**: Indicates that vulnerabilities not covered by the active remediation rules can be found in the **Action** column and must be repaired individually.<br><br><br>**Impact Devices Count**: Click on the number of impacted devices provides access to the affected devices, which displays details on affected devices and their repair status.<br><br>**Action**: Provides a **Repair** option when a vulnerability affects a large number of devices. If a device is in an **Unrepaired** state, no operation entry will be displayed in the **Action** column. |
