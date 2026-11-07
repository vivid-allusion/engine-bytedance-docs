---
title: "Configure threat protection"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-threat-protection"
---

The **Threat protection** module provides real\-time defense against web application\-layer attacks. Unlike web content filtering — which focuses on governing outbound employee access — threat protection focuses on deep inspection of inbound traffic payloads and anomalous callback behaviors. By identifying and blocking malicious scripts, exploit code, and botnet communication signatures in real time, this module effectively reduces the risk of advanced persistent threat (APT) attacks against your organization.

This document describes how to configure advanced threat protection policies, define the protection scope, and use security logs for incident investigation.

<span id="1775ba49"></span>
## Prerequisites

Complete the following configurations as described in [Configure traffic routing policies](https://docs.byteplus.com/docs/sealsuite/configure-traffic-routing-policies):


1. **Configure a traffic routing policy**: Ensure that traffic from managed endpoints is routed through the SWG tunnel.

2. **Distribute the corporate root certificate**: Ensure that endpoints trust the corporate CA certificate, enabling the system to decrypt HTTPS traffic for content inspection.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning"><strong>Feature\-triggered automatic decryption</strong>: Threat protection automatically triggers decryption when needed. When an administrator specifies a scanning scope in <strong>Threat protection domains</strong>, the system <strong>automatically decrypts the associated HTTPS traffic</strong> to identify attack payloads (such as injected scripts and malicious code) within the traffic. No additional SSL decryption policy is required.</div>


* <div data-tips="true" data-tips-type="warning"><strong>SSL decryption policy takes precedence</strong>: If you have explicitly configured a "Do not decrypt" rule for a specific resource in the <strong>SSL decryption policy</strong>, it takes precedence over threat protection's automatic decryption logic. In this case, even if the resource is within the protection scope, the system will skip decryption and cannot perform content scanning.</div>



<span id="b994fbe7"></span>
## Configure advanced threat protection policies

Advanced threat protection uses semantic analysis and behavior detection to identify and block web application\-layer attacks and data exfiltration.


1. Log in to the Admin Console.

2. Go to **SWG** \> **Threat protection** \> **Threat Protection config** in the left navigation pane.

3. Click **Edit** on the **Advanced threat protection** card, and configure each policy based on your security requirements.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e587e73efef24a61b0b223f969c9dfa5~tplv-goo7wpa0wc-image.image) </span>

   * **Protection details**

      Advanced threat protection analyzes behavioral signatures in application\-layer traffic to provide detection and defense across the following dimensions:

      
      |Attack category |Sub\-item |Detection and protection logic |
      |---|---|---|
      |**Injection attacks** |**SQL injection** (SQLi) |Blocks database injection attacks — including blind injection, union\-based queries, and error\-based injection — preventing attackers from illegally modifying or reading database content through web input fields. |
      ||**Remote code execution** (RCE) |Detects and blocks unauthorized calls to Unix or Windows system commands (such as Shellshock exploits). Prevents attackers from exploiting web vulnerabilities to execute malicious commands on the server (for example, `; cat /etc/passwd`) to gain system privileges. |
      ||**File inclusion** (LFI/RFI) |Identifies and filters local file inclusion (LFI) and remote file inclusion (RFI) requests that use path traversal patterns (such as `../`). Prevents attackers from reading sensitive system files or remotely executing malicious code scripts. |
      ||**Language\-specific** (PHP/Java) |Provides specialized protection for PHP and Java environments. Focuses on identifying and blocking application\-layer attacks that exploit deserialization vulnerabilities and unsafe function calls (such as `eval()` and `system()`). |
      |**Web Client Attacks** |**Cross\-site scripting** (XSS) |Detects malicious script injection in request payloads in real time. Focuses on protecting against reflected and stored XSS by blocking payloads containing `<script>` tags and anomalous event handlers such as `onload`/`onerror`, safeguarding user endpoints from script\-based attacks. |
      ||**Session fixation** |Monitors and identifies anomalous behavior during session management, preventing attackers from tampering with or pre\-setting a user's Session ID. Ensures the uniqueness and security of user sessions, guarding against unauthorized account hijacking. |
      |**Protocols and Scanners** |**Protocol enforcement** |Enforces HTTP/HTTPS request validation based on RFC protocol standards. Identifies and blocks anomalous packets containing malformed request headers, non\-standard HTTP methods, and formatting errors, reducing the risk of malformed\-packet attacks against web services. |
      ||**Scanner detection** |Maintains a fingerprint library of automated scanners. Accurately identifies and blocks traffic patterns from automated vulnerability scanning tools such as SQLMap, Nikto, Nmap, and Nuclei, effectively preventing reconnaissance and information gathering by attackers. |
      |**Information leak protection** |**Server error suppression** |Automatically monitors and blocks detailed error messages generated by backend servers. Masks responses including Java stack traces, SQL error messages, and IIS default error pages, preventing attackers from obtaining enterprise system architecture information through error feedback. |
      ||**Web shell detection** |Identifies and blocks communication fingerprints and response content characteristic of common web shells (such as China Chopper and Weevely), preventing attackers from establishing persistent backdoor control channels. |
      

   * **Configure actions**

      For each protection item, you can select the following actions:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c656360227c648fe859cb38c0d2df1bb~tplv-goo7wpa0wc-image.image) </span>

      * **Deny**: The system immediately terminates the connection and displays a security block page to the user (see custom messaging below). The system always logs blocked events.

      * **Allow**: The system permits access.

         * **Record logs**: When selected, the system still records the access log even though the action is allowed, enabling silent auditing or risk analysis later.

   * **Configure the block page**

      When any protection item triggers a "Deny" action, the managed endpoint displays a security block page. You can customize the messaging to meet your organization's requirements:

      * **Notification title**: Customize the main heading of the block page.

      * **Notification content**: Customize the detailed block explanation text.

      * **Preview**: During configuration, use the preview area at the bottom of the page to see how the message will appear in a browser.

      * **Multilingual support**: Configure a **Default language** and click  **+ Add language** as needed to provide localized messaging for employees in different languages (currently supporting English and Japanese).


<span id="8b68ab85"></span>
## Configure threat protection domains

Because threat protection involves deep packet inspection, it consumes gateway processing resources. Administrators can define a specific scanning scope — only resources in the list are inspected, while all other traffic is exempted to optimize performance.


1. Go to **SWG** \> **Threat Protection** \> **Threat Protection Config** \> **Effective Domains**.

2. Configure the scanning resource list. You can select built\-in or custom website categories from the resource library.


<span id="6073021c"></span>
## Security log analysis

The security log module records all events captured by the threat protection engine. Administrators can use this module to trace attack activity and assess the accuracy of existing policies based on log details.

<span id="8a170678"></span>
### Quick search and filtering

On the main **Security logs** page, use the filters at the top to quickly narrow the audit scope. For example:


* **Locate by threat signature**: Filter by **Threat type** (such as SQL injection or remote code execution) to find specific attack events.

* **Audit by action result**: Filter for records where the **Action** is "Allow" with logging enabled, to check for potential false negatives; filter for "Deny" records to verify that blocks are working as expected.

* **Trace by target resource**: Search for a specific **URL** to view the access frequency and potential threat risk of that site within your organization.


<span id="75fcba72"></span>
### In\-depth event investigation

Click **Details** on any log entry to reconstruct the full event across the following dimensions:


* **Determination basis**: View the **Triggered URL** and specific **Threat type** to confirm the attack payload.

* **Subject characteristics**: Identify the **User identity** (name, department, account status) and **Device characteristics** (operating system version, SealSuite client version) associated with the threat.

   * **Operations tip**: If the same device generates a large volume of the same threat type within a short period, investigate whether the endpoint has been compromised and is attempting to launch outbound attacks.


<span id="9bd0b905"></span>
### Packet\-level root cause analysis

In the event details, click **View details** in the detailed log records to access the lower\-level network packet analysis interface. This is critical for confirming false positives and troubleshooting network connectivity issues. Key fields:


* **status (status code)** : Verify the gateway response. For example, `403` indicates that SWG successfully blocked the request.

* **method (request method)**  and **user_agent**: Determine whether the request originated from a browser or an automated script.

* **intranet_ip (gateway internal IP)**  and **sip (source IP)** : Confirm the traffic flow path within the enterprise intranet.

* **duration (request round\-trip time)** : Evaluate the impact of the detection engine on business access performance.
