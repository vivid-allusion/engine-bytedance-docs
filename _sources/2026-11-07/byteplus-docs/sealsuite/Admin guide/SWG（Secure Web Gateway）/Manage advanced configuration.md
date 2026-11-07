---
title: "Manage advanced configuration"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/manage-advanced-configuration"
---

To ensure high service availability and a smooth employee experience without compromising security, you can use the advanced configuration module to fine\-tune SWG runtime behavior. This guide explains how to configure policies for specific scenarios like network failures, public Wi\-Fi authentication, and Microsoft 365 performance optimization, helping you maintain business continuity in complex environments.

<span id="70e513ba"></span>
## How to access


1. Log in to the Admin Console.

2. Go to **SWG** \> **Advanced Config** in the left navigation pane.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce2925059aaf4c11aa5389b9f37597d6~tplv-goo7wpa0wc-image.image) </span>


<span id="b150160a"></span>
## Configure Scope for Control Policies

This provides a centralized entry point for adjusting the distribution scope of the corporate root certificate. Administrators can quickly modify the certificate's auto\-installation targets, keeping the security audit scope in sync with actual business needs (such as organizational changes or management requirement adjustments).


1. Click **Configure** to navigate to **Enterprise settings** \> **Company General** \> **General Settings**, where you can update the certificate's auto\-distribution scope in the **Root Certificate Management** section.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6c0cbd678ed47008db0008252a767fa~tplv-goo7wpa0wc-image.image) </span>

2. Click **Configure** in the  **② Certificate Auto\-Installation Scope** section.

3. Redefine the scope dimensions based on your current operational needs.

4. Click **Confirm**. After saving, the SealSuite client automatically syncs the latest distribution policy and silently imports the certificate on newly added target endpoints.


<span id="52172ca6"></span>
## Client Fault Escape Strategy

When SWG serves as the mandatory path for enterprise internet access, its connection stability directly affects business continuity. Under extreme network fluctuations or gateway node failures, if the client cannot establish an encrypted tunnel, employees may lose internet access entirely.

The Client Fault Escape Strategy feature provides an automated service availability monitoring and degradation mechanism. The system uses the client to probe gateway nodes in real time. When it determines that connection quality is critically poor or all nodes are unavailable, it allows the client to temporarily bypass the SWG tunnel and connect directly to the public internet, ensuring that business operations are not disrupted by security system communication failures.


* **Configuration**: In the **Client Fault Escape Strategy** section, click **Edit** and configure the following parameters in the popup:

   * **Fault Detection Mechanism**

      
      |Field |Description and logic |
      |---|---|
      |**Probe interval** |Defines how frequently the client sends node availability checks. For example, if set to 5 seconds, the client sends a probe packet to all available nodes every 5 seconds to obtain latency information. |
      |**Probing frequency** |Defines the number of consecutive abnormal samples required to trigger an action. Multiple consecutive probes filter out false positives caused by occasional network jitter. |
      |**Fault threshold** |Defines the hard threshold for determining that a node is unavailable. If the probe latency for the current node consecutively exceeds this threshold, the system considers the node failed and immediately triggers a **node switch**. If all nodes meet this failure condition, **failover** is triggered. |
      |**Health threshold** |A performance threshold for optimizing the browsing experience. When the current node's latency exceeds the set value (for example, 100 ms) and the difference from the lowest\-latency available node reaches the set value (for example, 50 ms), the client automatically performs a **node switch**, migrating the connection to the optimal node. |
      

   * **Client Failover Mechanism**

      Defines the action taken when failover is triggered. Currently fixed to **Internet direct access**, meaning the system temporarily disables SWG traffic routing and allows traffic to exit directly through the local network.

* **Configuration impact**:

   * **Temporary security compliance degradation**: When failover is triggered and direct internet access is enabled, web traffic from managed endpoints no longer passes through SealSuite SWG for auditing and filtering. Policies such as web content filtering, cloud application control, and threat protection are temporarily suspended.

   * **Automatic control recovery**: During the failover period, the client continues probing node status. As soon as an SWG node becomes available again, the system immediately re\-establishes the secure tunnel and restores all security policies.


<span id="96e6dcbe"></span>
## Captive Portal Authentication

On public Wi\-Fi networks (such as airports and hotels), the network typically redirects user requests to a specific web authentication page, requiring users to log in or acknowledge terms before they can access the internet. If SWG attempts to establish an encrypted tunnel before authentication is complete, the authentication page may fail to load, leaving the user unable to connect.

The Captive Portal Authentication feature automatically identifies such network environments. During authentication, the system temporarily allows endpoint traffic to pass through so the authentication process can complete, and automatically restores security protection once the device is online.


* **Configuration**:

   1. In the **Captive Portal Authentication** section, click **Edit**.

   2. On the configuration page, enable the **Portal authentication scanning** toggle.

   3. Set the client **Temporary release time** — the maximum duration of the unprotected state after bypass is triggered (in minutes, default is 10 minutes). After this threshold is exceeded, the system forces an attempt to re\-establish the secure tunnel. To prevent endpoints from being exposed in an unprotected state for extended periods, do not set this value too high.

   4. Click **Confirm** to complete the configuration.

* **Client notifications**:

   * **User notification**: When a captive portal is detected and bypass is triggered, the SealSuite client displays a popup informing the user that they are in a temporary bypass state. The notification auto\-closes after 10 seconds, and the user can also dismiss it manually.

   * **Status display**: During the temporary bypass period, the client's SWG connection status shows "Disconnected," and the user cannot manually initiate a connection.

   * **Admin Console status**: On the **Access Devices** page, the device status is also displayed as "Disconnected."


<span id="b2ac5026"></span>
## Microsoft 365 Recommended Configuration

Microsoft 365 services (such as Teams and SharePoint) are extremely sensitive to network latency. Performing SSL decryption on these services often causes audio/video stuttering, file sync failures, or client login issues. Additionally, because Microsoft frequently updates its service IP ranges and domain addresses, manually maintaining a bypass list is prohibitively expensive for administrators.

To address this, SealSuite provides the **Microsoft 365 recommended configuration** feature. Once enabled, the system automatically syncs the latest Microsoft official network endpoint data via API and generates a high\-priority **SSL decryption** exemption rule in the background. This feature reduces the burden of manually maintaining address lists while ensuring that M365 traffic bypasses the encryption/decryption engine through transparent forwarding, preserving business continuity for video conferencing and large file transfers.


* **Configuration**: Enable the toggle in the **Microsoft 365 Recommended Config** section. In the confirmation dialog, read the prompt and click **Confirm**.

* **Configuration effect**: The system automatically generates a no\-decrypt rule with priority **100** for **Microsoft 365 recommended exemption addresses**. When a managed endpoint initiates a Microsoft 365 access request, the system matches this rule first and performs a "Do not decrypt" and "Transparent forwarding" action.

* **Policy restrictions**:

   * **Edit restrictions**: The auto\-generated exemption policy only supports modifying **effective scope** (people, departments, or devices). Other fields such as priority and action cannot be changed.

   * **Disable logic**: The auto\-generated exemption policy cannot be deleted or disabled from the SSL decryption policy list. To stop optimizing Microsoft 365 traffic, the administrator must return to the **Advanced config** page and disable the **Microsoft 365 recommended config** toggle.

* **Configuration impact**:

   * **Automatic policy override**: Because the rule generated by this feature has the **highest matching priority**, it overrides any manually configured blocking policies targeting Microsoft 365 resources. The system applies "Transparent forwarding" to ensure business availability takes precedence.

   * **Accelerated access**: Related traffic no longer consumes gateway encryption/decryption resources, significantly reducing access latency.

   * **Dynamic rule maintenance**: The system continuously maintains real\-time synchronization with Microsoft's official endpoint data, requiring no ongoing manual maintenance by administrators.


<span id="b8dfe604"></span>
## Advanced Web Filter Configuration

In practice, users may indirectly access high\-risk sites blocked by the organization (such as gambling or adult content) through legitimate services like Google Translate, Bing cached pages, or the Wayback Machine. Because the top\-level domain of such traffic belongs to a legitimate service, standard web content filtering or cloud application control policies may produce false negatives.

In the **Advanced Web Filter Configuration** section, administrators can enable the **Embedded Site Categorization** feature. This feature provides a deep parsing mechanism that unpacks and audits nested service traffic, preventing employees from bypassing organizational security controls through legitimate services.


* **Configuration**: On the **Advanced config** page, enable the **Embedded Site Categorization** toggle to activate the feature.

* **How it works**:

   * **Identify nested traffic**: Automatically identifies requests made through well\-known translation engines (such as Google Translate) or web cache services.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The current version only supports parsing nested traffic from <strong>Google Translate</strong> and <strong>Wayback Machine</strong>.      </div>
      

   * **Extract and validate**: Extracts the original target URL from the actual request and performs a secondary classification and evaluation against the organization's configured **cloud application control policies** and **web content filtering policies**.

   * **Policy enforcement**: Follows rule priority (Block \> Warn \> Audit \> Not enforced). If the nested site's access control policy has a higher priority than the outer proxy or translation service's policy, the nested site's own control policy takes effect.

* **Configuration impact**:

   * **Blocking effect**: If you have configured a policy to block the "Gambling" category, when a user attempts to access a gambling site through Google Translate, the system blocks the nested content from loading and returns a standard block page — even though the request is wrapped under a legitimate translation service domain.

   * **User experience note**: If employees report being blocked by SealSuite while using translation or web snapshot features normally, advise them to check whether the original page they are translating contains high\-risk content that the organization has blocked.


<span id="83920e47"></span>
## Log Record Management

**Log Record Management** controls whether the system records full Internet access audit logs. In complex enterprise network environments, administrators can flexibly configure this switch to effectively balance full behavior traceability and audit analysis efficiency.


* **Configuration method**: On the **Advanced** page, find the **Log Record Management** section and turn on the feature switch.

* **Execution logic**:

   * **Disabled (default)** : The system records only access events that match custom control policies. It does not record background forwarded traffic that does not match any policy. This mode is suitable for scenarios where administrators want to focus on high\-risk event analysis and improve the efficiency of daily audit operations.

   * **Enabled**: The system records audit logs for all traffic taken over by the gateway. Even if the traffic does not match any custom business control policy, such as website content filtering or cloud application control, the system records its application domain\-level access trace. This mode is suitable for scenarios with strict compliance audit requirements where full traceability of employees’ Internet access behavior is required.
