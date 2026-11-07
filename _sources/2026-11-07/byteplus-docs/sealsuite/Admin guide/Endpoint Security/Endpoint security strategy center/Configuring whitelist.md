---
title: "Configuring whitelist"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-whitelist"
---

**Whitelist** configuration is a global exception mechanism in the Endpoint Security system. When legitimate enterprise files, self\-developed tools, or normal processes are mistakenly blocked by security policies (such as antivirus or Skill detection), administrators can configure a whitelist to precisely allow them. This ensures business continuity while maintaining defense strength. This document introduces how to configure and manage various whitelists.

<span id="82e31061"></span>
## File allowlist

File allowlists exclude trusted files or processes that are falsely reported by the antivirus engine from scanning, ensuring normal business operations.

<span id="a023a522"></span>
### Add a file allowlist


1. Log in to the Admin Console.

2. In the left navigation bar, select **Endpoint Security** \> **Strategy Center**.

3. On the **Strategy Center** page, click the **Whitelist** tab.

4. On the right side of the **File allowlist** area, click  **+ Add Allowlist**, complete the following configurations, and click **Confirm**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**OS** |Select the operating system this rule applies to (Windows, macOS, Linux). Multiple selections are allowed.<br><br>If you plan to use "File Path" as a condition, ensure you only select one OS type to prevent path format conflicts. |
   |**Allowlist settings** |Define the criteria for the exclusion. You can add multiple rules; all rules must be met (AND logic) for the rule to take effect.<br><br>Supported rules:<br><br><br>* **File SHA1:**  Uses the file's unique hash. This is the recommended method as it is the most precise.<br><br>* **File path:**  Excludes files within a specific directory. The system validates the path format based on the selected OS.<br><br>* **File signature:**  Excludes files with a specific digital signature.<br><br>* **File name** / **File extension** / **Alarm Name** |
   |**Remarks** |(Optional) Add a description for audit purposes (e.g., "Finance Dept Reporting Tool"). |
   |**Scope** |Define where this rule applies. You can apply it to **All objects** or restrict it to specific **Departments, Roles, Employees**, or **Devices**. |
   


<span id="67117b6a"></span>
### Add a file whitelist from alert events

When you confirm an alert is a false positive on the **Threat Alerts** page, you can add the file to the global whitelist with one click directly from here.


1. Go to **Threat Alerts** \> **Virus Killing**.

2. Locate the false positive event and click **Remediation** in the **Action** column.

3. Select the target file, click **Add to Allowlist** in the **Action** column.

4. A dialog will appear with pre\-filled information:

   * **OS:**  Defaults to the OS of the reporting device.

   * **Configuration:**  Defaults to **File SHA1** (safest method). If the SHA1 is unavailable, it defaults to File Path/Name.

   * **Scope:**  Defaults to "All devices."

5. Adjust the settings if necessary and click **Confirm**.


<span id="907f14c3"></span>
### Manage existing file whitelists

In the **File Allowlist** list, you can view detailed information (settings, scope, last modified by) for existing rules. Use the **Edit** or **Delete** options to modify or remove rules as needed.

In the **File Allowlist** list, you can:


* View detailed information for each rule, such as **Configuration conditions**, **Effective objects**, **Remarks**, and the **Last modifier**.

* **Edit** or **Delete** existing rules.


<span id="07e8bf88"></span>
## PowerShell Run Parameters Whitelist

For **Windows** endpoints, if you have enabled **Suspicious PowerShell script execution detection** when configuring detection policies, you can now add trusted command\-line parameters as exceptions using this feature. This precisely allows specific operations and avoids intercepting legitimate O&M scripts.

<span id="54e8e48f"></span>
### Add whitelist command\-line parameters


1. Log in to the Admin Console.

2. Navigate to **Endpoint Security** \> **Strategy Center**.

3. Click the **Whitelist** tab and locate the **PowerShell Run Parameters Whitelist** area.

4. Click  **+ Add Allowlist**. You can choose between **Single Add** or **Batch Add**.

   * **Adding a single whitelist**

      Configure the following parameters and click **Confirm**.

      
      |**Configuration Area** |**Description** |**Examples** |
      |---|---|---|
      |**Command line arguments** |Enter the command\-line parameter to be allowed. Supports Chinese, English, special characters, and spaces, up to 2048 characters |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab5ba01a66c947e58742401595a74684~tplv-goo7wpa0wc-image.image) </span> |
      |**Match type** |Supports **Include match** or **Regular match**.<br><br><br>* **Include match**: The actual command line contains the allowlisted command\-line parameter.<br><br>* **Regular match**: The actual command line matches the regular expression defined in the allowlist. ||
      |**Comment** |Add a note to describe the purpose of the command line. ||
      

   * **Batch add whitelist**

      Click **Template download**, complete the file according to the instructions, upload the file, and finally click **Confirm**.


<span id="182ed987"></span>
### Test and manage whitelist command\-line parameters


* **Test Regex**: When configuring regex match rules, we recommend using the test feature. Enter a real command\-line example to verify whether the expression hits as expected.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69436a3a2cc94cfb9f7ba21dcd9f2a5a~tplv-goo7wpa0wc-image.image) </span>

* **Export List**: Click **Export List** to export all current PowerShell whitelist rules as an Excel file for backup, auditing, or migration.

* **Manage existing rules**: In the **PowerShell Run Parameters Whitelist** list, you can view all added rules, and **Edit** or **Delete** them.
