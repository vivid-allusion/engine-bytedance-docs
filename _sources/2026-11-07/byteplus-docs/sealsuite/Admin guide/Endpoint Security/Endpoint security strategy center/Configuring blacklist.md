---
title: "Configuring blacklist"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-blacklist"
---

**Blacklist** is used to forcibly block known malicious files or processes across all endpoints. When you receive external threat intelligence or discover internal malicious files (such as specific ransomware hashes), administrators can use this feature to add risk signatures into the system for global blocking and rapid response to known threats. This document introduces how to add and manage blacklist rules.

<span id="583d0ee1"></span>
## Add a blacklist entry


1. Log in to the Admin Console.

2. In the left navigation pane, select **Endpoint Security** \> **Strategy Center**.

3. On the **Strategy Center** page, click the **Blacklist** tab.

4. On the right side of the page, click  **+ Add Blocklist**, complete the following configurations, and click **Confirm**.

   
   |**Field** |**Description** |**Example** |
   |---|---|---|
   |**Virus type** |Select the risk type you want to assign to the blacklisted item. Options include **Unknown**, **Phishing**, **Trojan**, **Webshell**, **Malicious Email**, **Exploitation tools**, **Malicious advertising**, **Hacking tools**, **Ransom software**, **Virus**, or **Mining tools**. |**Example 1**: Add files by name and flag them as ransomware. This example ensures `suspicious_file.exe` and `unwanted_app.dll` are flagged as ransomware during scans on Windows.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0418d62ea2014254adacea26587fa825~tplv-goo7wpa0wc-image.image) </span><br><br>**Example 2**: Add a process to the blocklist. This example adds the `hacker_tool.exe` process to the blocklist for targeted detection on Windows and Linux systems.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f69557126054052b4fb1511996a1970~tplv-goo7wpa0wc-image.image) </span><br><br>**Example 3**: Add a file by its SHA1 hash. This example adds a file with a specific SHA1 hash to the blocklist for macOS and Linux to flag it as a virus.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1741bdb830d247eabf8eca3ffa0f5934~tplv-goo7wpa0wc-image.image) </span> |
   |**Task type** |Select the type of item to add to the blocklist. Options include **Process**, **File name**, or **File SHA1**. ||
   |**Related configuration** |Enter the specific configuration details based on the selected task type. Press Enter to separate multiple entries. ||
   |**OS** |Select the applicable operating systems. Options include **macOS**, **Windows**, or **Linux**. ||
   


<span id="f1e8436a"></span>
### Manage existing blacklist entries

In the **Blacklist** list, you can view the details of each rule, as well as **Edit** or **Delete** them.
