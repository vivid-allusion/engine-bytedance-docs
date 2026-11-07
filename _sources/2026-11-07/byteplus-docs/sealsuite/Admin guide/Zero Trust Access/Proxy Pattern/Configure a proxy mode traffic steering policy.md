---
title: "Configure a proxy mode traffic steering policy"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-proxy-mode-traffic-diversion-strategy"
---

A **traffic routing policy** controls traffic in proxy mode. It determines whether network requests from an endpoint enter the enterprise encrypted proxy tunnel or use the local network directly. An administrator can define flexible policy rules based on employee identity, network location, or specific application processes. For example, video meetings during remote work may experience lag, large file downloads may consume gateway bandwidth, or broad domain names may cause unrelated traffic to enter the proxy tunnel. In these cases, configure a traffic routing policy to let specific traffic bypass the proxy tunnel and connect to the Internet directly. This effectively reduces gateway load and improves employees’ Internet access experience, while still securing internal network access.

This topic describes how to configure a traffic routing policy in SealSuite.

 &nbsp;

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Make sure the SealSuite client version is 3.3.19 or later to support proxy mode.

* We strongly recommend that you first refer to [Configure a proxy mode ACL policy](https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-acl-policy) to add an Access Policy. This ensures that after traffic is taken over, allow or block actions can be executed based on permission configurations, avoiding interruptions to compliant services.


 &nbsp;

<span id=".5re75Yqg5byV5rWB562W55Wl"></span>
## Add a traffic routing policy


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **Zero Trust Access** \> **Proxy Policy**.

3. Switch to the **Traffic Routing** tab, and click **Add traffic diversion strategy** in the upper\-right corner.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-routing-list.png) </span>

4. On the **Add Traffic Routing Strategy** page, complete the following configurations and click **Confirm** to save.


 &nbsp;

<span id=".5Z-65pys5L-h5oGv"></span>
### Basic information

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-routing-general.png) </span>


* **Policy name**: Enter a custom name to uniquely identify the policy.

* **Strategy status**: Select **Enable** or **Disable**.

* **Priority**: Set the priority of the current policy. The value ranges from 0 to 100. A larger value indicates a higher priority. Multiple policies can take effect at the same time. When the system checks endpoint traffic, it matches policies in descending order of priority and stops matching after a match. If two matching policies have the same priority, the policy with the latest modification time is applied first.


 &nbsp;

<span id=".5Yqo5L2c6YWN572u"></span>
### Action configuration

Select how the system handles traffic when network requests from an endpoint match the conditions of this policy.

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-routing-general.png) </span>


* **Force redirection**: Send traffic that matches the rule through the encrypted tunnel to the proxy gateway. This is typically used to secure access to core internal business data.

* **Bypass/Direct Connect**: Traffic that matches the rule does not enter the proxy tunnel. Instead, it directly uses the employee's current local network for access. This is suitable for public cloud services, video meetings, and other scenarios that consume high bandwidth and do not require internal network permissions. It can effectively prevent access lag and reduce enterprise bandwidth pressure.

* **Route by permissions**: Traffic is steered only when the user has "access permission" for the application. Otherwise, the traffic uses a direct connection. This mode automatically inherits the application scope defined in ACL policies. The administrator only needs to manage permissions in ACL, and the traffic routing scope is automatically synchronized in real time, reducing maintenance costs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Traffic takeover priority note</strong></div>


<div data-tips="true" data-tips-type="tip">When an enterprise enables both ZTNA proxy mode and SWG, the <strong>boundary between internal and external networks may be unclear</strong>. For example, public cloud SaaS software can be both an Internet application and an office asset. <strong>Coarse\-grained configurations</strong>, such as configuring global takeover in SWG, can also cause <strong>the address of the same application to be included in the traffic routing policy scopes of both systems</strong>. When the SealSuite client processes network traffic, it follows the logic that <strong>proxy mode takes precedence over SWG</strong>.</div>



* <div data-tips="true" data-tips-type="tip">If traffic hits the <strong>Force redirection</strong> policy in proxy mode, the traffic is sent into the proxy tunnel and is <strong>no longer</strong> controlled by SWG policies.</div>


* <div data-tips="true" data-tips-type="tip">If traffic hits the <strong>Bypass/Direct Connect</strong> policy in proxy mode, or does not match any proxy policy and uses the local network for direct connection, the client continues to determine whether the traffic is within the takeover scope of SWG. This determines whether public network security filtering is applied.</div>



<div data-tips="true" data-tips-type="tip"><strong>Best practice</strong>: Although the system provides a priority fallback mechanism, we strongly recommend that you proactively define clear boundaries during policy configuration to reduce troubleshooting complexity. Define internal application addresses precisely in proxy mode and add them to the SWG exclusion list so that SWG does not take over this traffic.</div>


 &nbsp;

<span id=".5byV5rWB6IyD5Zu0"></span>
### Traffic routing scope

Define which traffic is controlled by this policy. SealSuite proxy mode can match traffic by its destination application, originating process, and network location.

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-routing-scope.png) </span>


* **Select app**: Select the destination addresses to which this policy applies. You can select **Apply all** or **Selected applications**. The application data here comes from the "proxy application" resource library configured in the system. If the application you need is not in the list, go to **Application** \> **Proxy App** to create and define the resource first. For more information, see [Manage proxy applications](https://docs.byteplus.com/en/docs/sealsuite/management-agent-mode-application-resources).

* **Process** (optional): After this option is enabled, the traffic routing action can be determined based on the "initiator" of the traffic, that is, the specific software on the endpoint.

   * **Use case**: Assume that traffic to `*.corp.com` is configured to use the encrypted proxy tunnel. If an internal video meeting server also uses this domain name, high\-bandwidth video traffic may consume the company's dedicated line bandwidth. To prevent this, use this field to configure a separate high\-priority policy. Select the process name `zoom.exe` or `feishu.exe` (use the actual video meeting software in your environment), and configure the action to use the local network. This protects internal systems and prevents issues such as video meeting lag.

   * **Configuration steps**:

      1. After you enable the switch, click **Select process**.

      2. In the **Process library** that appears, directly select existing process rules.

      3. If the list does not contain the process you need, click **New process** in the upper\-right corner.

      4. On the creation page, enter the **Rule Name** and select the corresponding **Operating system**. Windows and macOS are currently supported. Matching by **process name**, **process signature**, and **process path** is supported. You can combine multiple conditions to precisely define a process. The available logical relationships are "belongs to" and "contains any".

   * **Configuration recommendations (prevent false blocking)** :

      * **Prefer signatures**: To improve interception accuracy for properly signed software, we strongly recommend that you **combine "process name + process signature"** . Relying only on "process name" can be easily spoofed by malware, or can duplicate the name of another common system program. This may cause security policies to be bypassed or false blocking to occur. A digital signature verifies the real software publisher at the cryptographic level. Combining the process name and process signature helps ensure that only the actual target software is allowed or blocked.

      * **Avoid broad paths (Windows)** : In Windows, avoid configuring an overly broad drive path such as `C:\` as the only condition. Otherwise, the client includes all network requests from all programs in that directory, including system core services and antivirus software, in the control scope. This can easily cause system\-wide network disconnection or critical service outages. Always combine path conditions with other fields, such as the process name.

      * **Note signature differences (macOS)** : The distribution mechanism of Apple systems means that the same software usually has different underlying digital signature identifiers when downloaded from the official website (developer signature) and from the Mac App Store (Apple official distribution signature). If only the process signature of the official website version is entered, the same software downloaded from the App Store cannot be controlled, creating a policy gap. Pay special attention to the software distribution channels used by your enterprise during configuration.

* **Network location** (optional): After this option is enabled, the traffic routing action can be determined based on the current network environment of the endpoint. The "network location" data here comes from the **network zone** resource library maintained globally in the system. To add network zone resources, see [Network zone management](https://docs.byteplus.com/en/docs/sealsuite/network-zone-management).

   * **Any network zone**: Do not restrict the network location. The current policy takes effect in any network environment.

   * **Specified network zones**: Select one or more defined network zones, such as "Beijing headquarters office area". This traffic routing policy is triggered only when the system detects that the current network environment of the endpoint, such as IP or Wi\-Fi, matches the characteristics of the selected zones.

   * **Unknown network zone**: If the current network environment of the endpoint does not match the characteristics of any network zone defined in the SealSuite Admin Console, it is determined as an "unknown network zone". This usually indicates that the employee is on an uncontrolled public network or home network. Select this option to create traffic routing rules specifically for external network environments. For example, automatically bypass traffic on the corporate internal network, and automatically force traffic routing at home.


 &nbsp;

<span id=".55Sf5pWI5p2h5Lu2"></span>
### Effective conditions

Specify the users or devices to which this policy applies.

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-routing-effective.png) </span>


* **Scope**: Restrict the effective scope by **User** or **Device**.

* **Exclude object** (optional): You can also exclude certain special objects. The policy does not take effect for excluded objects. The final effective scope is **effective objects \- excluded objects**.


 &nbsp;

<span id=".5a6i5oi356uv5pWI5p6c"></span>
## Client experience

After a traffic routing policy is enabled, the network page of clients on endpoints within the effective scope shows different connection options depending on the gateways deployed by the enterprise:

 &nbsp;

<span id=".5Zy65pmv5LiA77ya57qv5Luj55CG5qih5byP77yI5LuF6YOo572y5LqG5Luj55CG572R5YWz77yJ"></span>
### Scenario 1: Pure proxy mode (only proxy gateways are deployed)

If the enterprise has deployed only proxy gateways and has not deployed traditional VPN gateways, the client directly enters a pure proxy work environment.

End users can manually connect or disconnect as needed in the VPN module on the overview page or network page. The accessed proxy gateway cluster is determined by the client access policy:


* If automatic access is used, the system selects the cluster.

* If the administrator allows manual cluster selection, users can select a proxy gateway cluster within the scope allowed by the policy. For the specific configuration method, see [Configure a proxy mode client access policy](https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-client-access-policy).


 &nbsp;

<span id=".5Zy65pmv5LqM77ya5re35ZCI5qih5byP77yI5ZCM5pe26YOo572y5LqG5Luj55CG572R5YWz5LiOLXZwbi3nvZHlhbPvvIk="></span>
### Scenario 2: Hybrid mode (both proxy gateways and VPN gateways are deployed)

If the enterprise is in a security architecture transition period, or maintains both gateway types for special requirements, employees can switch between VPN and proxy mode.

Employees can freely switch between **split tunnel mode/full tunnel mode (VPN)**  and **proxy mode** in the VPN module on the overview page or network page, based on the connectivity of the current service.


* When split tunnel/full tunnel mode is selected, traffic is controlled by traditional VPN policies.

* When "proxy mode" is selected, traffic is controlled by the traffic routing policy and ACL policy configured in this topic. Which proxy gateway cluster is accessed, and whether employees are allowed to manually select a cluster, are controlled by the [client access policy](https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-client-access-policy).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To help enterprises smoothly roll out a zero trust architecture, the administrator can click <strong>Switch</strong> in the upper\-right corner of the <strong>Proxy Policy</strong> list page, and set the enterprise\-wide "client default connection mode" to <strong>proxy mode</strong>. This setting only determines the initial default option when a new employee installs or starts the client for the first time. It does not affect the employee's permission to switch modes later.</div>


 &nbsp;

<span id=".566h55CG5byV5rWB562W55Wl"></span>
## Manage traffic routing policies

An administrator can monitor, search for, and adjust created policies in real time on the traffic routing policy list page.

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-routing-list.png) </span>


* **Filter and search**: Supports combined filtering and queries by policy name, action, status, and application address, such as IP address, domain name, and wildcard domain.

* **Manage effective status**: Use the status switch in the **Actions** column of the list to enable or disable a policy with one click.

* **Edit policy**: If business requirements change, click **Edit** in the Actions column. The configuration panel opens with the current policy settings prefilled. Make your changes and click **Confirm**. The new configuration is delivered and takes effect immediately.

* **Delete policy**: Click **Delete** and complete the secondary confirmation to remove policies that are no longer needed. A deleted policy cannot be restored. Before you proceed, confirm that related services are not affected.


 &nbsp;

<span id=".5p-l55yL5Luj55CG5Zyo57q_6K6-5aSH"></span>
## View online proxy devices

The system records an employee endpoint as "online" when all the following conditions are met:


1. The client is currently in **proxy mode**.

2. The client is in the VPN **connected** state and has not been manually disconnected.

3. The employee identity or device falls within the scope of at least one **traffic routing policy**.


Go to **Zero Trust Access** \> **Online Endpoints** \> **Proxy Online Endpoints** to verify policy delivery and view details of current active connections:

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/border-online-proxy.png) </span>


* **Check device online status**: If an employee reports that an application cannot be accessed, search for the device by employee name or device information. If the device is not online, check whether the client is in proxy mode, whether it is connected, and whether the employee identity or device is within the effective scope of the traffic routing policy.

* **Connection details**: Includes the type of the connected device, internal and public IP addresses, and associated employee identity and department information.

* **Connection duration**: Helps determine whether abnormal long\-lived connections or zombie sessions exist.
