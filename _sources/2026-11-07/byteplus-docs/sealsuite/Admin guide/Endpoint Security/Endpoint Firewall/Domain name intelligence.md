---
title: "Domain name intelligence"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/domain-name-intelligence"
---

You can configure the Domain Threat Intelligence and Endpoint Protection features to block and alert on access to malicious domains. This helps protect your organization from a wide range of threats, including remote access trojans (RATs), crypto mining pools, malware, botnets, APTs, and phishing sites.

<span id="b86a9036"></span>
## How It Works

The Domain Threat Intelligence feature prevents employees from accidentally accessing malicious domains. For example, if a user clicks a malicious link, this feature can instantly block the connection, preventing malware infection and protecting corporate data.

For devices belonging to employees in critical roles or departments, you can enable Endpoint Protection. This feature uses the endpoint firewall to provide targeted, device\-level blocking of malicious domains, adding a robust layer of security for your core business operations.

<span id="a97b16f6"></span>
## Step 1: Configure the Domain Intelligence Library

First, you need to select which categories of threats the system should monitor.


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Endpoint Security** \> **Threat Intelligence**.

3. On the **Domain Name Intelligence** page, click **Library** **Configuration** in the top\-right corner.

4. In the **Configuration** section, select the threat types you want to enable.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c0cf4d77b634fa69e8d0462eaaa9ab0~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) If you identify a false positive, you can add the domain to the allowlist. In the **Allowlist** section, click  **+ Add Allowlist** and enter the domain details.

6. Click **Confirm**.


<span id="8a5df143"></span>
## Step 2: Configure Endpoint Protection

Next, define how the system should respond when a threat is detected on an endpoint.


1. Log in to the Admin Console.

2. Go to **Endpoint Security** \> **Threat Intelligence**.

3. In the **Endpoint Protection** section of the **Domain Name Intelligence** page, click **Configure**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d715244395824be69c0468f089ecfcd7~tplv-goo7wpa0wc-image.image) </span>

4. On the **Endpoint Protection** page, set the following parameters:

   
   |**Section** |**Parameter** |**Description** |
   |---|---|---|
   |**Access mode** |Block access |Blocks access to the malicious domain and displays a notification on the client. An alert is also generated in the Admin Console. |
   ||Audit access |Allows access to the domain but still generates an alert in the Admin Console for visibility. |
   |**Notification** |/ |We recommend enabling notifications when using **Block access** mode. You can click **Edit Notification Template** to customize the notification content. |
   |**Operating System** |/ |Select the operating systems this policy applies to (**Windows** or **macOS**).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">MacOS clients require network extension permissions.</div><br> |
   |**Scope** |By User |Apply the policy to specific **Departments** or **Roles**. It's recommended to scope this to only those who require endpoint protection. |
   ||By Device |Apply the policy based on **Operating System**, individual **Devices**, or **Device Groups**. |
   

5. Click **Confirm**.

6. Return to the **Domain Name Intelligence** page and enable the main **Endpoint Protection** toggle switch.


<span id="6c50563f"></span>
## Step 3: View Domain Intelligence Alerts


1. Log in to the Admin Console.

2. Go to **Endpoint Security** \> **Threat Intelligence**.

3. The **Domain Name Intelligence** page provides a comprehensive overview of detected threats:

   * The dashboard displays a breakdown of **Threat Types** and a **Threat Trend** chart for the last 7 days (or a custom range).

   * The alert list below provides detailed information for each event. You can use the **Custom Filter** and **Columns** options to refine your view.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf00e9ce44684839a4faa316aed17b7a~tplv-goo7wpa0wc-image.image) </span>

   
   |**Column** |**Description** |
   |---|---|
   |**Trigger time** |The time the event was detected by the system. |
   |**Report time** |The time the event was logged in the Admin Console. |
   |**User Information** |The user associated with the event. Hover for more details. |
   |**Device Information** |The device associated with the event. Hover for more details. |
   |**OS** |The operating system of the affected device. |
   |**Threat type** |The category of the threat that was detected (e.g., "Malware," "Phishing"). |
   |**Action** |The action taken by the system ("Block" or "Allow"). |
   |**Destination IP address** |The malicious domain that was detected. |
   |**Device IP address** |The source IP address that initiated the network request. |
   |**Client version** |The version of the SealSuite client that reported the event. |
