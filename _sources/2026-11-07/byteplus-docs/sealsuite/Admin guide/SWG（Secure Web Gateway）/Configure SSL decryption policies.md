---
title: "Configure SSL decryption policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-ssl-decryption-policies"
---

In today's internet communications, most web access and cloud applications use the HTTPS encryption protocol. Because encryption protects the content of data packets, the Secure Web Gateway (SWG) cannot by default access the specific information inside encrypted traffic (such as request paths, web page keywords, or uploaded file content).

**SSL decryption policies** define how SWG handles HTTPS traffic. When no SSL decryption policy is configured, the system does not decrypt HTTPS traffic by default. By configuring this policy, administrators can selectively perform decryption auditing, connection\-layer security validation, or connection blocking for specific business traffic.

<span id="b5bcee28"></span>
## Core purpose


* **Achieve content visibility**: Perform SSL/TLS decryption on encrypted traffic, enabling the system to identify detailed information inside encrypted packets — such as request paths, web page keywords, and uploaded/downloaded file content.

* **Optimize performance**: Configure no\-decrypt rules for high\-load or trusted traffic (such as video conferencing and large file downloads) to reduce gateway CPU consumption and ensure business availability.

* **Enforce connection\-layer validation**: During the TLS handshake, verify the target server's certificate status and protocol version, and intercept access requests with security deficiencies (such as expired certificates or TLS 1.0/1.1 protocols).


<span id="56bf91d9"></span>
## Decision logic

SealSuite SWG follows this underlying logic sequence to determine whether to decrypt HTTPS traffic:


1. **Explicit SSL policy evaluation (highest priority)** 

   When traffic enters the gateway, the system first checks whether it matches an **SSL decryption policy** configured by the administrator.

   * If it matches, the system strictly executes the action defined in that policy (decrypt, do not decrypt, or block access).

2. **Implicit policy\-driven decryption (default fallback)** 

   If the traffic does **not** match any SSL decryption policy, the system continues to check whether the traffic falls within the control scope configured in **Website content filtering**, **Cloud application control**, or **Threat protection** (for example, the domain is included in a filtering policy category).

   * **Within control scope**: The system **automatically decrypts** the traffic by default, ensuring that business security policies (such as keyword identification and malicious code scanning) can extract plaintext for inspection.

   * **Outside control scope**: The system **does not decrypt** the traffic by default, forwarding it securely in its encrypted state to protect privacy and conserve gateway compute resources.

> **Example**:

> Suppose the "Social media" category is configured in a website content filtering policy, but you have not configured any SSL policy for that category. When an employee accesses Weibo, the system triggers the implicit mechanism and **automatically decrypts** the traffic for auditing.

> If you configure a "Do not decrypt" rule specifically for "Weibo" in an SSL decryption policy, the explicit policy takes precedence and the system will **not decrypt** the traffic. In this case, website filtering can only act based on the domain name (not on specific URL paths or content).


<span id="86b5dca4"></span>
## Prerequisites

Complete the following configurations as described in [Configure traffic routing policies](https://docs.byteplus.com/docs/sealsuite/configure-traffic-routing-policies):


1. A traffic routing policy has been configured to ensure traffic passes through the SWG tunnel.

2. An enterprise root certificate has been configured to enable SWG to decrypt HTTPS encrypted traffic.


<span id="f04feee8"></span>
## Add an SSL decryption policy


1. Log in to the Admin Console and go to **SWG** \> **Strategy Center** \> **SSL Decryption**.

2. Click  **+ Add Strategy** in the upper\-right corner of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/562d4890cac64c59904aed77569b8f8f~tplv-goo7wpa0wc-image.image) </span>

3. Configure the parameters based on your business requirements.

   * **General**

      
      |**Field** |**Description** |
      |---|---|
      |**Policy name** |Enter a custom name to identify this policy, such as "Video conferencing no\-decrypt policy." |
      |**Priority** |Set the priority using the slider or by entering a value directly (0–100). A higher value means higher priority. If two policies have the same priority value, the system uses the creation or modification time — the most recently created or edited policy takes precedence. |
      

   * **Apply rule**

      
      |**Field** |**Description** |
      |---|---|
      |**Decrypt** |The system decrypts matching TLS traffic to obtain plaintext data. You can also establish pre\-connection security compliance validation rules based on digital certificate attributes.<br><br>After enabling the **Certificate validation** toggle, the system performs security checks during the TLS connection establishment (handshake) phase. If the target server certificate fails any of the selected validation types below, the system blocks the connection.<br><br><br>* **Certificate not trusted**: The system verifies the issuing authority of the target server's certificate. If the certificate is not issued by a trusted authority, or the certificate chain is incomplete, the system blocks the connection.<br><br>* **Revocation check**: The system uses OCSP (Online Certificate Status Protocol) to verify whether the certificate has been revoked by the issuing authority.<br><br>   * **Revocation check timeout settings**: Set the query wait time in seconds. If no revocation status response is received within the specified time, the system defaults to passing the check, preventing normal business disruption caused by network fluctuations.<br><br>* **Certificate version**: Enforce the minimum encryption protocol version used during the connection. If the actual version is lower than the configured value, the system blocks the connection.<br><br>   * **Minimum client certificate version**: Restricts the protocol version initiated by the endpoint.<br><br>   * **Minimum server certificate version**: Restricts the protocol version supported by the target website server. |
      |**Do not decrypt** |The system does not decrypt the traffic. The traffic is forwarded in its encrypted state. |
      |**Block** |Blocks access and displays a pop\-up alert on the user's client. |
      

   * **Controlled resources**

      Click  **+ Add condition** to define the addresses or application scope this policy applies to. You can directly reference built\-in or custom resources from **Settings** \> **Resources** \> **Resource Library** \> **Cloud Applications** or **Web URL library**, or manually enter custom domains. Note: Exact domain matching takes precedence over wildcard domain matching (for example, `mail.google.com` takes precedence over `*.google.com`).

   * **Scope**

      Select the employees, departments, or specific devices this policy applies to. Use **Exclude object** to fine\-tune exemptions.

4. Click **Confirm** to save the configuration.


<span id="928b4ec8"></span>
## Policy matching and operations

<span id="16811597"></span>
### Policy matching mechanism

Building on the underlying decision logic described in [Decision logic](https://docs.byteplus.com/docs/sealsuite/configure-ssl-decryption-policies#56bf91d9), the SSL decryption policy list follows a strict hierarchical matching logic. When processing access requests, the system applies different evaluation paths based on the resource source type (resource library categories or user\-defined):


* **Path A: Resource library (Cloud Applications** / **Web URL library)** 

   1. If you select resource categories from the system resource library in the controlled resources, the system follows a **resource precision first** logic — policies matching exact domains (such as `mail.google.com`) take precedence over policies matching wildcard domains (such as `*.google.com`).

      * **Example**: Between the following two policies, even though Policy A has a higher numeric priority, Policy B's controlled resource is an exact domain, so the system will still apply the decrypt action for `mail.google.com`.

         * Policy A: Priority 100, `*.google.com` no\-decrypt policy.

         * Policy B: Priority 90, `mail.google.com` decrypt policy.

   2. When resource precision is equal, the system matches by the policy's priority value. A higher value means higher matching priority. If priority values are equal, the most recently created or edited policy takes precedence.

* **Path B: Custom resources**

   If you manually enter domain lists through **Custom Address** \> **Domain address** in the controlled resources, the system skips resource precision matching and goes directly to the **policy priority matching** phase.


<span id="9f40bbfb"></span>
### Day\-to\-day policy operations

On the SSL decryption policy main page, administrators can manage the full policy lifecycle.


* **Multi\-dimensional search and filtering**: Supports combined filtering by **Policy name**, **People/Department/Role**, **Device information**, **IP address**, and **Action** to quickly locate target policies.

* **Manage policy status**: Use the toggle in the **Action** column on the right side of the list to quickly **Enable** or **Disable** a policy. Disabled policies do not participate in the matching logic described above.

* **Edit**: Click **Edit** in the Action column to modify all parameters of an existing policy. After saving, the new rules are immediately pushed to the SWG nodes.

* **Delete**: Click **Delete** in the Action column, or select multiple policies and click **Bulk delete** at the bottom left to remove policies you no longer need.


<span id="d14ab06a"></span>
## Auditing and logging

To maintain consistency in audit dimensions, the SSL decryption process itself does not generate independent audit logs. SSL decryption policy matches and their corresponding decrypt/block results are recorded in different locations depending on the type of controlled resource: under **Web filtering** \> **Access Event Logs**, or **Cloud App Control** \> **Access Event Logs** / **DLP Event Logs**.
