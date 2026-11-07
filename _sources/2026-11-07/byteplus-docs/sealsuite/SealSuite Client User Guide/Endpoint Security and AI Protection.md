---
title: "Endpoint Security and AI Protection"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/endpoint-security-and-ai-protection"
---

In the SealSuite client, click **Security** in the left navigation pane to go to the **Security Overview** page. This page provides global detection capabilities and is divided into two status sections: **AI Guard** and **Endpoint Security**, providing a comprehensive view of the security protection status of the current device.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddd6e7a761ef4dd182f0f95c4af99896~tplv-goo7wpa0wc-topic.webp) </span>

 &nbsp;

<span id="one-click-detection-and-repair"></span>
## One\-click detection and repair

Click **One\-click detection** at the bottom of the **Security Overview** page. The system automatically performs a comprehensive detection on the current endpoint. The detection covers regular endpoint security, such as baseline, software, and viruses, as well as AI office scenario risks, such as malicious Skills. If risks are detected, the system displays the number of risks in the statistics on the right.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8784a464dad4d15add33f8bcff9cd81~tplv-goo7wpa0wc-topic.webp) </span>

Click detection details. A risk\-fixing drawer appears on the right, displaying all detected risks by category.


* **One\-click repair**: For common risk items that support automatic handling, click **One\-click repair** at the bottom of the list to complete the process.

* **One\-click Delete**: If the detected risk items contain only **malicious Skill** **extensions**, click **One\-click Delete** to physically remove them from the local device.

* **Manual intervention**: Some risks, such as password strength check failures and missing required software, require manual intervention. Employees can follow the system guidance to complete the fix.


 &nbsp;

<span id="ai-office-security"></span>
## AI Guard

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The items displayed in this section depend on whether the administrator has configured related AI Security policies in the Admin Console. If no policies are configured, this card is not displayed in the client.</div>


After the enterprise administrator enables AI Security Protection, the **Security Overview** page displays an **AI Guard** card in the upper\-right corner, showing the brief status of **Skill Security Scan** and **Runtime Protection**. Click **Details** on the card to go to a dedicated page to view more information and perform operations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/662d0d7cb9bb4f2bbf7f7ca46c0ab4c6~tplv-goo7wpa0wc-topic.webp) </span>


* **Runtime Protection**: Displays the real\-time running status of the underlying security capabilities on the current endpoint, including **Malicious Behavior Protection (EDR)** , **Sensitive Data Protection (DLP)** , and **High\-risk port protection (Firewall)** . These capabilities comprehensively protect data and device security during daily work and AI interactions. Click **Protection log** in the upper\-right corner to view related security blocking logs, such as DLP blocking records triggered by non\-compliant outbound data transfers in AI applications.

* **Skill Security Scan**: Displays the security scan status of Skills in the system and the number of malicious Skills detected. If risks are found, employees can click to view the risk details list and delete the malicious extensions to physically remove them from the local device. This section also displays the currently effective scan policies, such as whether real\-time scanning and scheduled scanning are enabled.

* **Agent Behavior Guardrails**: Displays the security protection features enabled for AI tools on the current device. This module sets secure operation boundaries for AI tools, preventing them from accessing sensitive files or performing high\-risk operations during runtime, and protecting the endpoint work environment.


 &nbsp;

<span id="endpoint-security"></span>
## Endpoint Security

The **Endpoint Security** section is displayed in the lower\-right area of the **Security Overview** page. It includes the status of regular endpoint security items, such as **Baseline compliance** and **Trojan Virus**.

 &nbsp;

<span id="baseline-compliance"></span>
### **Baseline compliance**

Displays the status and detection results of device baseline and running process protection.


* **Device baseline**: The system checks whether system settings, account password policies, and other configurations meet the enterprise security baseline requirements.

* **Running process**: The system monitors processes currently running on the endpoint, prompting employees to manually run certain required processes or end non\-compliant processes marked in the blacklist.


 &nbsp;

<span id="trojan-virus"></span>
### **Trojan Virus**

Displays virus scan results for the endpoint. If the system detects virus files, it provides different handling logic based on the control action and notification policy configured by the enterprise administrator in the Admin Console.


* **Reminder only**: The client only displays a pop\-up notification to notify the employee that malicious files are detected. The files are not quarantined.

* **Quarantine, recoverable**: The system automatically moves virus files to the file quarantine area and may display a pop\-up notification. Employees can click **Quarantine Zone** in the upper\-right corner of the **Security Overview** page to view details. For such files, employees can choose to restore, trust, or delete them.

   * **Restore**: Restores the file to its original path.

   * **Trust**: Restores the file and adds it to the whitelist. The file will no longer be checked.

* **Quarantine, unrecoverable**: The system automatically moves virus files to the quarantine area. In the **Quarantine Zone**, employees can only delete the files and cannot restore or trust them.
