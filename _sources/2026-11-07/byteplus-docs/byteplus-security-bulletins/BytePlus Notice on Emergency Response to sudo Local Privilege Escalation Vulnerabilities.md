---
title: "BytePlus Notice on Emergency Response to sudo Local Privilege Escalation  Vulnerabilities"
product: "BytePlus Security Bulletins"
product_code: "byteplus-security-bulletins"
section: "Document"
source: "https://docs.byteplus.com/en/docs/byteplus-security-bulletins/CVE-2025-32463_CVE-2025-32462_solution"
---

<span id=""></span>
# **Background**

Recently, two sudo local privilege escalation vulnerabilities(CVE\-2025\-32463/CVE\-2025\-32462) were detected, leading to potential critical risks. The Security Team of BytePlus responded promptly, providing comprehensive and reliable mitigation measures for its customers. We suggest all enterprise customers conduct complete troubleshooting and remediation.

<span id=""></span>
# **Description of the Vulnerabilities**

Sudo is a shell command used on Unix\-like operating systems. On July 1, 2025, two local privilege escalation vulnerabilities were identified in sudo, which could allow unintended elevation of a regular user's privileges to those of a privileged user, effectively bypassing operating system\-level access controls. Among them, CVE\-2025\-32463 is classified as *critical* and affects systems with the default configuration. The vulnerability leverages sudo’s chroot functionality to escalate privileges from a normal user to a privileged user.

<span id=""></span>
# **Code of the Vulnerabilities**

CVE\-2025\-32463、CVE\-2025\-32462

<span id=""></span>
# **Severity**


|<div style="text-align: center"><br><strong>Code</strong></div><br> |<div style="text-align: center"><br><strong>Severity</strong></div><br> |
|---|---|
|<div style="text-align: center"><br>CVE\-2025\-32463</div><br> |<div style="text-align: center"><br>Critical</div><br> |
|<div style="text-align: center"><br>CVE\-2025\-32462</div><br> |<div style="text-align: center"><br>Low\-Risk</div><br> |


<span id=""></span>
# **Status of the Vulnerabilities**

Updated as of July 2, 2025, 00:00:00（UTC+8）


|<div style="text-align: center"><br><strong>Vulnerability Details</strong></div><br> |<div style="text-align: center"><br><strong>Poc Status</strong></div><br> |<div style="text-align: center"><br><strong>Exploit in the wild</strong></div><br> |
|---|---|---|
|<div style="text-align: center"><br>Public</div><br> |<div style="text-align: center"><br>Public</div><br> |<div style="text-align: center"><br>Undiscovered</div><br> |


<span id=""></span>
# **Impact Scope**


|<div style="text-align: center"><br><strong>Code</strong></div><br> |<div style="text-align: center"><br><strong>Impact Scope</strong></div><br> |
|---|---|
|<div style="text-align: center"><br>CVE\-2025\-32463</div><br> |<div style="text-align: center"><br>1.9.14 <= sudo <= 1.9.17</div><br> |
|<div style="text-align: center"><br>CVE\-2025\-32462</div><br> |<div style="text-align: center"><br>1.9.0 <= sudo <= 1.9.17</div><br><br><br><div style="text-align: center"><br>1.8.8 <= sudo <= 1.8.32</div><br> |


<span id=""></span>
# **Remediation Suggestion**

Upgrade sudo to at least version 1.9.17p1

<span id=""></span>
# **Mitigation Measures**

The platform offers a comprehensive and reliable security solution to customers of BytePlus. The following steps can guide you to troubleshoot and address the issue. 

Utilizing the vulnerability detection capability of the Cloud Security Center to identify and locate assets that contain vulnerability CVE\-2025\-32463 and vulnerability CVE\-2025\-32462. See the detailed remediation recommendations to get more information.


> 1. Log in to the Cloud Security Center, apply for beta access and purchase the higher\-version: https://console.volcengine.com/security\-center/csc

> 2. Open **Risk Management\-Vulnerability Detection**. Click **Scan Now**, and search for vulnerability CVE\-2025\-32463 and vulnerability CVE\-2025\-32462. If they are found, click **Details** to check affected assets and remediate according to suggestions.


Use **Cloud Security Center** to perform real\-time detection of sudo privilege escalation activities through its runtime monitoring capabilities. It also supports detection of other post\-exploitation behaviors, including access to sensitive files, suspicious code execution, persistence, and further privilege escalation.


> 1. Log in to the Cloud Security Center, apply for beta access and purchase the higher\-version: https://console.volcengine.com/security\-center/csc

> 2. Open **System Configuration\-Install and Uninstall** to make sure protection is activated on all hosts.

> 3. Continuously monitor security risks. If any intrusion activity is detected, you can view the details on the **Security Alerts** page and follow the recommended actions to respond accordingly.


<span id=""></span>
# **Reference**


1. https://cve.mitre.org/cgi\-bin/cvename.cgi?name=CVE\-2025\-32463

2. https://www.stratascale.com/vulnerability\-alert\-CVE\-2025\-32463\-sudo\-chroot

3. https://cve.mitre.org/cgi\-bin/cvename.cgi?name=CVE\-2025\-32462

4. https://www.stratascale.com/vulnerability\-alert\-CVE\-2025\-32462\-sudo\-host
