---
title: "Secure Web Gateway overview"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/secure-web-gateway-overview"
---

SealSuite **Secure Web Gateway** (SWG) is a key part of the SealSuite unified office security solution. It delivers integrated Internet access control, cloud application security control, and network\-side Data Loss Prevention (DLP) for enterprises. It replaces fragmented and costly traditional on\-premises security appliances. Through a unified platform, it helps enterprises connect to the Internet and SaaS services securely, efficiently, and compliantly.

&nbsp;

<span id="f31b24b4"></span>
## Core capability matrix

SealSuite SWG provides security capabilities across the following four dimensions. These dimensions form closed\-loop management through coordinated policies:


* **Traffic routing layer**: Managed by the **traffic routing policy**. It identifies the Endpoint environment based on the network location, such as an office area or an unknown network. It then determines which traffic enters the SWG tunnel for security control, and which traffic uses a local direct connection.

* **Protocol processing layer**: Managed by the **SSL decryption policy**. As a traffic preprocessor, it determines whether to decrypt HTTPS encrypted packets and provides certificate security validation at the connection layer.

* **Business control layer**: Composed of **website content filtering**, **cloud application control**, **AI security**, and **threat protection**. After traffic is decrypted, it enforces URL access control, application action control, AI semantic audit, and malicious code detection.

* **Operations assurance layer**: Provides **access device management** and **advanced configuration**. It ensures business continuity through real\-time connection monitoring, automatic fail\-open on failures, forced Portal authentication, and other mechanisms.


&nbsp;

<span id="a7084f5c"></span>
## Traffic processing sequence

When an Endpoint initiates an Internet access request, SealSuite SWG processes the data flow in the following order:


1. **Traffic routing matching**: The client matches the "traffic routing policy". If the request matches an "excluded object", the traffic does not enter the tunnel. If it is not excluded, the traffic is diverted to an SWG node.

2. **Decryption decision**: After traffic reaches the gateway, the system identifies the protocol type. For HTTPS requests, the system first matches the **SSL decryption policy**:

   * If an SSL decryption policy is matched and the action is  **"Do not decrypt"** : The system stops packet processing and forwards the traffic directly. All subsequent Web access control policies do not take effect.

   * If an SSL decryption policy is matched and the action is  **"Decrypt"** : The system decrypts the traffic and extracts plaintext data.

   * If no SSL policy is configured, but a business control policy references the resource: The system performs **business\-driven automatic decryption**.

3. **Content audit and filtering**: In the plaintext data stream, the system matches **advanced threat protection**, **website content filtering**, **cloud application control**, and **AI security protection** rules in parallel or in sequence.

4. **Forward response**: After all policies pass validation and no "Block" action is triggered, the gateway egress forwards the traffic to the destination server.


&nbsp;

<span id="1ebc9207"></span>
## Dependencies and constraints between modules

Understanding the logical dependencies between features helps you quickly troubleshoot issues in complex operations environments:

&nbsp;

<span id="4eacc0ae"></span>
### Logical dependencies (Prerequisites)


* **The traffic routing policy is the foundation of all security capabilities**: If no traffic routing policy is configured, traffic does not pass through the gateway. Website filtering, cloud application control, and threat protection cannot take effect.

* **Certificate distribution is the core support for deep audits**: All technical capabilities related to SSL decryption, such as keyword filtering, cloud application action identification, and sensitive data scanning, require the Endpoint to trust the enterprise CA certificate. Otherwise, the system cannot inspect encrypted traffic for Security Detection. This exposes the Administrator to audit blind spots and control failure risks.


&nbsp;

<span id="e90c56e0"></span>
### Priority constraints (Conflict handling)


* **The SSL decryption policy has the highest decision priority**: The "Do not decrypt" action in an SSL decryption policy takes precedence over the automatic trigger logic of "website content filtering" and "cloud application control". If "Do not decrypt" is configured, keyword blocking or file audit for the resource becomes ineffective.

* **Business\-driven behavior**: Website content filtering and cloud application control can automatically trigger SSL decryption. The administrator does not need to manually configure an SSL decryption policy for each controlled application.


&nbsp;

<span id="YBxkNgkPAV"></span>
## Get started

After you understand the basic concepts and working principles of Secure Web Gateway (SWG), start configuration by following the path below. This helps you gradually build a comprehensive enterprise Internet security system.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Secure Web Gateway features are currently in invite\-only beta. To use them, contact your sales or technical support representative for activation.</div>


&nbsp;

<span id="w6PYvxW1ue"></span>
### 1. Route and decrypt traffic

This is the starting point for enabling SWG and the prerequisite for all upper\-layer policies to take effect.


* **Configure a traffic routing policy**: Configure a traffic routing policy to connect Endpoint traffic that requires control to the SWG tunnel. This process usually guides you through initial enterprise root certificate configuration. This certificate is the basis for subsequent HTTPS content audit.

   * See: [Configure a traffic routing policy](https://docs.byteplus.com/en/docs/sealsuite/configure-traffic-routing-policies?lang=en)

* **Configure an SSL decryption policy**: Although various control policies automatically trigger decryption on demand, SSL decryption policies have the highest priority. Use this policy to force "do not decrypt" for highly trusted or latency\-sensitive services, such as video conferencing. This optimizes performance and ensures service compatibility.

   * See: [Configure an SSL decryption policy](https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies?lang=en)


&nbsp;

<span id="yka4joVf5F"></span>
### 2. Configure core security policies and define protection rules

After traffic is successfully connected, configure one or more of the following policies based on your enterprise security goals.


* **Website content filtering**: Configure this policy to control employee access to different website categories, such as social networking, gaming, and video. You can also use it to prohibit access to known risky sites, such as phishing and malware websites.

   * See: [Configure a website content filtering policy](https://docs.byteplus.com/en/docs/sealsuite/configure-web-content-filtering-policies?lang=en)

* **Cloud application control**: Configure access deny or access audit policies to prohibit employee access to specified cloud applications, such as personal cloud drives, public email, and AI tools, or to record employee access to these applications.

   * See: [Configure cloud application control policies](https://docs.byteplus.com/en/docs/sealsuite/configure-cloud-application-control-policies?lang=en)

* **Web Data Protection**: To audit or block outbound web text, file uploads, and file downloads, go to **DLP \> Strategy Center \> Control Strategy \> Network DLP** to configure a policy. The system detects sensitive data when traffic passes through SWG.

   * See: [Configure a Web Data Protection policy](https://docs.byteplus.com/en/docs/sealsuite/configuration-web-data-protection-policy?lang=en)

* **GenAI Data Protection**: To detect prompts that employees send to AI applications or submit through large language model APIs, go to **DLP \> Strategy Center \> Control Strategy \> GenAI Data Protection** to configure a policy. The policy uses classification and grading rules to identify sensitive content, and then audits or blocks it.

   * See: [Configure a GenAI Data Protection policy](https://docs.byteplus.com/en/docs/sealsuite/configure-genai-data-protection-policy?lang=en)

* **Threat protection**: Configure this policy to defend against advanced Web attacks, such as SQL injection, cross\-site scripting (XSS), and Web Shell backdoors.

   * See: [Configure threat protection](https://docs.byteplus.com/en/docs/sealsuite/configure-threat-protection?lang=en)

* **AI security**: Configure AI security protection to discover AI assets used by the enterprise, or to use semantic recognition to prevent prompt attacks such as role\-playing and target hijacking. Use the GenAI Data Protection policy described earlier to detect sensitive data in prompts.

   * See: [AI security protection overview](https://docs.byteplus.com/en/docs/sealsuite/ai-security-protection-overview?lang=en)


&nbsp;

<span id="inXFO7wG63"></span>
### 3. Handle special scenarios and optimize performance

In addition to core policies, use the following configurations to ensure high business availability, handle special business scenarios, and optimize performance.


* **Manage advanced configuration**: Configure SWG service high availability to ensure business continuity.

   * See: [Manage advanced configuration](https://docs.byteplus.com/en/docs/sealsuite/manage-advanced-configuration?lang=en)


&nbsp;

<span id="Q0tzmdjOg7"></span>
### 4. Perform daily monitoring and operations

After policies go live, continuously monitor their running status and handle daily events.


* **Manage online devices**: View the list of devices currently connected to SWG in real time. In emergencies, you can perform **forced disconnect** or **temporary allow** operations on a specific device. Temporary allow generates a passcode that lets the user temporarily bypass controls.

   * See: [Manage access devices](https://docs.byteplus.com/en/docs/sealsuite/manage-connected-devices?lang=en)

* **Analyze access data**: Use visual dashboards and reports to analyze employee Internet access trends, traffic distribution, and most visited websites. This provides data support for continuous policy optimization.

* **Audit event logs**: Regularly review alert or block logs generated by each policy. This helps you identify potential risks, handle security events promptly, and determine whether false positives exist, so you can refine the policies.
