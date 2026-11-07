---
title: "Managing process injection whitelists"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-process-injection-whitelists"
---

Process Injection Whitelists are primarily used to resolve compatibility conflicts between the SealSuite DLP module and third\-party software on endpoints. Since the DLP module utilizes a memory injection mechanism to monitor application behavior for security purposes, conflicts may arise with specific software (e.g., self\-developed industrial software or specialized financial plugins), leading to startup failures, crashes, or performance lags. By adding the affected software to a whitelist, you can **exempt** it from DLP injection, immediately restoring the application's functionality.

<span id="c267d7c3"></span>
## Prerequisites


* **Client Version Requirement**: Windows ≥ 3.2.16


<span id="8f312c87"></span>
## Adding a Process Injection Whitelist


1. Log in to the Admin Console.

2. In the left navigation pane, go to **DLP** \> **Strategy Center**.

3. Switch to the **Whitelist** tab at the top, and select **Process Injection Allowlist** from the left\-hand menu.

4. In the top right corner of the **Process Injection Allowlist** page, click  **+ Add Allowlist**.

5. In the dialog box, configure the following information:

   
   |**Parameter** |**Description & Business Logic** |**Configuration Recommendation** |
   |---|---|---|
   |**Allowlist Name** |A custom identifier for the policy. |It is recommended to name it after the affected software, e.g., "In\-house ERP Compatibility Exclusion." |
   |**Remarks** |(Optional) Records the background or reason for the whitelist. |Briefly describe the conflict, e.g., "Resolves ERP crash issue after enabling DLP." |
   |**Allowlist Content** |Identifies targets via **Process Name** or **Process Path**. Matching either condition triggers the exemption. |Currently supports Windows endpoints only. Both fields allow up to 100 characters. We recommend using **wildcards** and **environment variables**. See the [Appendix](https://docs.byteplus.com/docs/sealsuite/managing-process-injection-whitelists#652d79b1) for details.<br><br><br>* **Process Name**: e.g., `app_name.exe`. Supports wildcards like `app?.exe` to match `app1.exe`.<br><br>* **Process Path**: e.g., `C:\Program Files\MyApp\*`. |
   

6. Click **Confirm** to complete the configuration.


<span id="d48c270a"></span>
## Managing Whitelists

In the list of whitelists, administrators can perform the following maintenance tasks:


* **Search and Filter**: Perform quick lookups based on name, remarks, content, or the user who last modified the entry.

* **Edit and Maintain**: Click **Edit** to update the processes or paths included in the whitelist.

* **Cleanup Obsolete Rules**: If your development team resolves a software compatibility issue through a version update, it is recommended to **Delete** the corresponding whitelist entry to restore the full scope of security protection.


<span id="bce51033"></span>
## FAQ

**Q: What is the difference between a "Process Injection Whitelist" and a "File Scan Whitelist"?** 

**A:**  The core differences lie in the **enforcement stage** and the **type of problem solved**:


* **Process Injection Whitelist (Focus: Stability)** : Operates during the loading phase of the DLP monitoring driver. It is used to resolve memory conflicts between SealSuite and third\-party software. If specific software crashes or fails to load plugins, use this to **exempt** the process from injection to ensure endpoint stability.

* **File Scan Whitelist (Focus: Accuracy)** : Operates during the data behavior analysis phase. It is used to reduce audit noise. If the software runs normally but its legitimate read/write activities in specific paths are frequently flagged as false positives, use this to **exclude** the related paths from scanning to improve audit precision.


**Q: Why does the software still encounter errors after I added the process name to the whitelist?** 

**A:**  This may be due to the following reasons:


1. **Incomplete Coverage**: Some software consists of multiple sub\-processes. We recommend using the **Process Path** with wildcards (e.g., `C:\SoftwarePath\*`) to cover the entire installation directory.

2. **Environment Variable Errors**: Ensure you are using the Windows format `%USERPROFILE%` rather than the macOS format.


<span id="652d79b1"></span>
## Appendix

<span id="10d1715f"></span>
### Wildcards and Environment Variables

To ensure your whitelist accurately matches software paths across different employee computers, use the following standard syntax:


* **Supported Wildcards:** 

   * `*` (Asterisk): Matches any number of characters. Example: `proc_*` matches `proc_1.exe` and `proc_update.exe`; `C:\MyApp\*` matches all files and subfolders in that directory.

   * `?` (Question Mark): Matches any single character. Example: `app?.exe` matches `app1.exe` or `appA.exe`, but not `app12.exe`.

* **System Environment Variables:** 

   * **Windows**: `%USERPROFILE%` represents the root directory of the currently logged\-in user (e.g., `C:\Users\Username`). Example: `%USERPROFILE%\AppData\Local\Temp\*`.
