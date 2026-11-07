---
title: "Managing file scan whitelists"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-file-scan-whitelists"
---

File Scan Whitelists are primarily used to address high\-frequency false positives during the DLP auditing process. When certain trusted applications (such as cloud document synchronization tools or code compilation tools) generate a large volume of normal read/write activities in specific paths, these behaviors may be misidentified as exfiltration risks, resulting in a flood of redundant alerts.

By configuring a scan whitelist, administrators can instruct SealSuite to skip DLP scanning for these specific paths. This effectively reduces "noise" in the audit logs and lowers system resource consumption while ensuring smooth business operations.

<span id="cc8a1a6e"></span>
## Adding a File Scan Whitelist


1. Log in to the Admin Console.

2. In the left navigation pane, go to **DLP** \> **Strategy Center**.

3. Switch to the **Whitelist** tab at the top of the page and select **File Scanning Allowlist**.

4. In the top right corner of the **File Scan Whitelist** page, click  **+ Add Allowlist**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aaf17d0955e646e099e4717ff3051aed~tplv-goo7wpa0wc-image.image) </span>

5. In the dialog box, configure the following information:

   
   |**Parameter** |**Description** |**Configuration Recommendation** |
   |---|---|---|
   |**Whitelist Name** |A custom identifier for the policy. |It is recommended to name it after the application or path, e.g., "Lark Sync Cache Exclusion." |
   |**Remarks** |(Optional) A description of the background or reason for the whitelist. |Briefly describe why this path is excluded for future auditing and review. |
   |**Client Version** |Defines the version range of the SealSuite client for which the whitelist is active.<br><br><br>* **All Client Versions**: (Default) Applies to all endpoints.<br><br>* **Some Client Versions**: Supports conditions such as **Higher than**, **Equal to**, **Lower than**, or **Range**. For a **Range**, enter both the start and end version numbers (inclusive). |Use this to target specific versions if false positives are known to occur only on certain client releases. |
   |**Outbound file path** |Specifies the folders or file paths that should be exempt from DLP scanning.<br><br><br>1. Select the target operating systems (**Windows** and/or **macOS**).<br><br>2. Enter the paths in the corresponding input fields. |You can add up to 30 paths (max 500 characters per entry).<br><br>**Note**: Use **wildcards** and **environment variables** to ensure paths remain valid across different user profiles. See the [Appendix](https://docs.byteplus.com/docs/sealsuite/managing-file-scan-whitelists#b6ed4201) for details. |
   

6. Click **Confirm** to complete the configuration.


<span id="9761b4b8"></span>
## Managing Whitelists

In the list of whitelists, administrators can perform the following maintenance tasks:


* **Search and Filter**: Perform combined queries based on whitelist name, remarks, operating system, outbound path, or the name of the last modifier.

* **Edit and Delete**: Modify the configuration of custom whitelists as needed. If a whitelist is obsolete or no longer required, it can be permanently removed.


<span id="90d87881"></span>
## FAQ

**Q: What is the difference between a "File Scan Whitelist" and a "File Outbound Blocking Whitelist"?** 

**A:**  The core differences lie in the **target** and the **enforcement stage**:


|**Dimension** |**File Scan Whitelist** |**File Outbound Blocking Whitelist** |
|---|---|---|
|**Target** |Specific file paths or directories. |Specific employees, departments, or devices. |
|**Mechanism** |The system performs **no scanning** at all for files in these paths. |The system **still scans** and identifies risks but does **not intercept** the action. |
|**Problem Solved** |**False Positives**: Prevents trusted app background activity from generating excessive audit logs. |**Authorization**: Allows trusted personnel to transfer sensitive files for legitimate business needs under strict policies. |


**Q: Why do I still see alerts for a path that has been whitelisted?** 

**A:**  Please verify the following two points:


1. **Client Version**: Ensure the "Client Version" range defined in the whitelist covers the affected endpoint.

2. **Path Accuracy**: Verify that environment variables are used correctly. For example, hardcoding `C:\Users\admin\...` on Windows will cause the whitelist to fail for other users (e.g., `C:\Users\john\...`).


<span id="b6ed4201"></span>
## Appendix

<span id="b90ad0ea"></span>
### Wildcards and Environment Variables

To ensure your path configurations accurately cover different user environments, please follow these formatting standards:


* **Supported Wildcards:** 

   * `*` (Asterisk): Matches any number of characters. Example: `C:\Downloads\*` matches all files in that directory.

   * `?` (Question Mark): Matches any single character. Example: `app?.exe` matches `app1.exe` or `appA.exe`, but not `app12.exe`.

* **System Environment Variables:** 

   * **Windows**: Use `%USERPROFILE%` to represent the root directory of the current user. Example: `%USERPROFILE%\Documents\*`.

   * **macOS**: Use `$HOME` to represent the root directory of the current user. Example: `$HOME/Library/*`.
