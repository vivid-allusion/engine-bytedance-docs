---
title: "Managing file outbound control whitelists"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-file-outbound-block-allowlists"
---

The **File Outbound Block Allowlist** is a feature for creating temporary exceptions to strict file\-blocking rules. When you need to handle business exceptions, such as during employee offboarding or for specific project needs, you can use this allowlist to grant specific users or devices temporary permission to send files without altering the main security policy.

<span id="c8aaec78"></span>
## Prerequisites

The following SealSuite client versions are required:


* **Windows**: 3.2.14 or higher

* **macOS**: 3.2.14 or higher


<span id="b5f78f55"></span>
## Creating an Allowlist Entry


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, go to **DLP** \> **Strategy Center** \> **Whitelist**.

3. Click the  **+ Create allowlist** button in the top\-right corner.

4. Configure the following parameters in the configuration panel:

   
   |**Section** |**Field** |**Description** |
   |---|---|---|
   |**General** |**Policy name** |A unique identifier for the allowlist policy. |
   ||**Remarks** |A description of the policy's purpose (e.g., "Special handover for offboarding employee"). |
   |**Allowlist settings** |**Effective content** |Currently fixed to **Any File**. |
   ||**Source channel** |Select the specific transfer channels (e.g., IM, Browser, Mail) to be exempted. |
   ||**Expiration Time** |Set the validity period. Choose **Permanent** or **Specify expiration time** (automatically expires after a set date). |
   |**Scope** |/ |Define the users, departments, or devices to which this exemption applies. |
   

5. Click **Confirm** to save and apply the policy.


<span id="37ec7492"></span>
## Managing Allowlists

From the **File Outbound Block Allowlist** dashboard, you can maintain existing rules:


* **Search and Filter**: Filter policies by name, member, device, or active status.

* **Maintenance**:

   * **Manually Created Rules**: You can view **Details**, **Edit**, or **Delete** these entries.

   * **API\-Generated Rules**: Rules created via OpenAPI are identified as `API Creation`. These are read\-only in the Admin Console and cannot be edited or deleted manually.


<span id="8a417ebb"></span>
## FAQ

**Q: Does the Channel Control Policy remain active after a File Outbound Block Allowlist is configured?** 

**A:**  Yes. **Channel Control Policies** and **File Outbound Block** **Allowlists** operate at different enforcement layers. Their relationship is as follows:


1. **Channel Control Policies** manage the usage permissions of specific software or channels. If an administrator disables an application (e.g., prohibiting the use of Baidu Netdisk for file transfers), the employee cannot initiate any file transfer actions through that app.

2. **File Outbound** **Allowlists** manage exemptions for specific content. The system only executes the "Bypass Block" instruction if the employee is permitted to use the software and the file they are sending triggers a sensitive data rule.


If the channel itself is blocked, the process never reaches the file detection stage, rendering the file allowlist ineffective. For an allowlist to be meaningful, ensure that the target user has the necessary permissions to use the corresponding channel.

**Q: What is the difference between this "Allowlist" and the "Exclusion Scope" within a standard File Blocking policy?** 

**A**: These serve different operational purposes:


* **Exclusion Scope (Long\-term Baseline)** : Use this for permanent architectural exclusions. For example, if the IT department is never subject to a specific restriction, they should be in the "Exclusion Scope" of that policy.

* **Allowlist (Temporary Exception)** : Use this for time\-bound business needs. For example, if a restricted employee needs to transfer files for a specific project handover, the "Allowlist" grants them a temporary bypass. Once the allowlist expires, the user automatically reverts to the standard restricted state without needing manual policy adjustments.
