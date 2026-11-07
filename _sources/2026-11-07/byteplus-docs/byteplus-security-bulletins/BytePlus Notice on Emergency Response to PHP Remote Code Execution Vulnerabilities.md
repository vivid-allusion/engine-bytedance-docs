---
title: "BytePlus Notice on Emergency Response to PHP Remote Code Execution Vulnerabilities"
product: "BytePlus Security Bulletins"
product_code: "byteplus-security-bulletins"
section: "Document"
source: "https://docs.byteplus.com/en/docs/byteplus-security-bulletins/CVE-2026-109618_CVE-2026-109619"
---

# Background

A recent outbreak of PHP remote code execution vulnerabilities poses potentially serious security risks. The Byteplus security team has responded promptly to provide customers with comprehensive and reliable mitigation measures. Organizations are advised to investigate and remediate affected systems immediately.

PHP is a widely used open\-source server\-side scripting language that powers numerous websites and applications. On October 21, 2026, the PHP team disclosed two severe remote code execution vulnerabilities:

* **CVE\-2026\-109618: Remote Code Execution Due to Improper Out\-of\-Memory Handling.**  When parsing file uploads or other requests, PHP may terminate processing prematurely due to memory exhaustion, leaving internal data partially initialized and improperly cleaned up. Subsequent access to this invalid data during request shutdown may cause memory corruption.

* **CVE\-2026\-109619: Remote Code Execution Due to Stale Global State.**  When a request terminates abnormally or shuts down, PHP may fail to properly clear internal state, such as session and error\-handling state, leaving references to freed memory. Subsequent requests handled by the same worker process may access these stale references, triggering a use\-after\-free vulnerability that can lead to remote code execution.

# Vulnerability Number

**CVE** **IDs**: CVE\-2026\-109618, CVE\-2026\-109619

# Risk Level

Critical

# Vulnerability Status

As of 08:00:00, October 22, 2026 (UTC+ 8)

|<br>Vulnerability Details<br> |<br>PoC Status<br> |<br>Exploitation in the Wild<br> |
|---|---|---|
|<br>Publicly disclosed<br> |<br>Publicly disclosed<br> |<br>Not found<br> |

# Scope of Impact

* 5.4.0 <= PHP < 8.2.35

* 8.3.0 <= PHP < 8.3.36

* 8.4.0 <= PHP < 8.4.27

* 8.5.0 <= PHP < 8.5.12

# mitigation measures

For Byteplus customers, the platform provides comprehensive and reliable security solutions, and troubleshooting and handling can be carried out following the steps below:

5. ### Full\-funnel Self\-Audit: Pinpointing Vulnerability Exposure Surfaces

> 1. Activate **Cloud** **Security** **Center** and purchase the Advanced Edition: https://console.byteplus.com/security\-center

> 2. On the Risk Management \- Vulnerability Detection page, click Scan Now, and after the scan is completed, go to the All Vulnerabilities \- System Application Vulnerabilities page to view the results.

> 3. Enter PHP in the vulnerability name search box to check whether there are any affected assets, and click Details to view the affected assets and remediation suggestions.

> 4. On the System Configuration \- Installation and Uninstallation page, confirm that security protection has been enabled on all hosts to perform runtime detection on post\-exploitation behaviors, including but not limited to reading and writing of sensitive files, backdoor persistence, and execution of suspicious code.

6. ### Prevention and Hardening: Restrict the Kill Chain of Conventional Attacks

> 1. Activate **Cloud Firewall**: https://console.byteplus.com/firewall

> 2. On the firewall switch page, click Internet boundary firewall, locate the public network EIP address of the business asset, and turn on the asset protection switch.

> 3. Go to Access Control \> Internet Boundary. On the Inbound Rules tab, click Add Policy. Add an access control policy to only allow trusted IPs to access the service ports of the assets.

7. ### Prevention and Reinforcement: Blocking Attack Behaviors at the Boundary

> 1. Enable **Web Application Firewall**: https://console.byteplus.com/waf

> 2. On the Web Application Firewall page, navigate to Vulnerability Protection and verify that it is enabled and configured in Strict or Normal mode. Continue to monitor alerts..

8. ### Continuous Monitoring: Capture Exploit Behavior Streams

> 1. Activate **Advanced Network Threat Detection System**: https://console.byteplus.com/ndr

> 2. On the Asset Center page, locate the public network EIP of the business asset and enable the asset protection switch.

> 3. Continuously monitor the Threat Center \- Alerts view for security alerts related to PHP remote code execution.

# Fix Recommendations

Upgrade PHP to version 8.5.12, 8.4.27, 8.3.36, or 8.2.35, or a later version in the corresponding release branch.
