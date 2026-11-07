---
title: "Configure proxy mode ACL policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-acl-policy"
---

An **ACL (Access Control List) policy** is the core access control engine of a proxy gateway. It determines whether traffic that reaches the gateway can access the target application. By configuring ACL policies, you can precisely define "who (specific employees or devices) can access what (specific internal applications)".

In proxy mode, SealSuite provides access control at two levels:


* **Basic admission control (ACL policy)** : Operates at the transport layer (L4). It mainly makes admission decisions based on employee identity, device attributes, target application ports, and the process that initiates the request.

* **Fine\-grained control policy**: Operates at the application layer (L7). For applications that use HTTP/HTTPS, it provides in\-depth permission verification and audit based on URL paths. This locks access permissions to specific pages or API endpoints and effectively reduces the risk of lateral privilege escalation within applications.


For applications that require Layer 7 control, an ACL policy is a prerequisite for enabling fine\-grained control. An access request must first pass transport\-layer verification by the ACL policy before the traffic can enter the subsequent application path evaluation process.

This document describes how to configure ACL policies in SealSuite Zero Trust proxy mode.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">ACL policies and fine\-grained control policies are applied <strong>in series</strong>. If the ACL policy action is set to "Reject", traffic is blocked directly, and subsequent fine\-grained control verification is not triggered.</div>


 &nbsp;

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Make sure you have deployed and added at least one **proxy gateway** node on the **Zero Trust Access** \> **Gateway Config** \> **Proxy Gateway** page by following [Access a proxy gateway](https://docs.byteplus.com/en/docs/sealsuite/access-proxy-gateway).

* To configure policies based on specific applications, make sure you have defined basic resources on the **Zero Trust Access** \> **Application** \> **Proxy App** page by following [Manage proxy applications](https://docs.byteplus.com/en/docs/sealsuite/management-agent-mode-application-resources).

* Make sure the SealSuite client has been upgraded to version 3.3.13 or later.


 &nbsp;

<span id=".5re75YqgLWFjbC3nrZbnlaU="></span>
## Add an ACL policy


1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **Zero Trust Access** \> **Proxy Policy**.

3. Switch to the **ACL Policy** tab to open the ACL policy list page.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/acl-list-ready.png) </span>

   * **Default access mode description**: The upper\-left corner of the page displays the underlying access control mode of the current proxy gateway. Click **Switch** to change between the following two states.

      * **Closed Network Mode (default)** : All traffic that does not match any "Allow" policy is forcibly blocked. In this mode, you usually need to add "Allow" policies to permit specific access.

      * **Default open mode**: A more permissive mode. All traffic that does not match any "Reject" policy is allowed by default. In this mode, you usually need to add "Reject" policies to block specific access.

4. On the right side of the page, click **Add access policy**.

5. On the policy configuration page that appears, complete the following configurations as needed, and click **Confirm**.


 &nbsp;

<span id=".5Z-65pys5L-h5oGv"></span>
### General


* **Policy name**: Customize the policy name. We recommend the format "department + application + permission", such as "R&D\-GitLab\-Allow", to simplify future O&M management.

* **Strategy status**: Select the initial status of the new policy, either enabled or disabled.

* **Priority**: The priority of the current policy. The value ranges from 0 to 100. A larger value indicates a higher priority. The system matches policies in descending priority order and stops after a match. If two policies with the same priority are matched, the most recently modified policy takes effect first.

* **Strategy effective duration**: Configure the time range during which the policy takes effect. Custom durations in days are supported.


 &nbsp;

<span id=".5Yqo5L2c"></span>
### Action

The action that the gateway performs when an endpoint network request matches all conditions in this policy. Configure this setting based on the current default access mode of the gateway.


* **Allow**: Allows access requests.

   * **In default deny mode** (common): Used to **authorize access** (allowlist). In a fully closed environment, this grants specific personnel or devices permission to access target applications.

   * **In default open mode** (special): Used for **audit tracing** or **exception allow rules in deny policies**. For example, a low\-priority policy named "Deny all contractors from accessing internal systems" already exists. If an external audit expert needs temporary access to the finance system, you can configure a high\-priority "Allow" policy for that expert to allow precise access.

* **Reject**: Blocks access requests.

   * **In default open mode** (common): Used to **restrict access** (blocklist). In a fully open environment, this blocks specific personnel or devices from accessing target applications.

   * **In default deny mode** (special): Used for **audit tracing** or **exception blocks in allow policies**. For example, a low\-priority policy named "Allow all R&D employees to access the test environment" already exists. If interns need to be prevented from accessing the test environment, you can configure a high\-priority "Deny interns from accessing the test environment" policy to precisely remove interns from the broad allowlist.


 &nbsp;

<span id=".5a6i5L2T"></span>
### Object

Define the specific scope controlled by this policy, including "who the policy applies to (effective objects)" and "what is controlled (applications)".


* **Scope**: Restricts the effective scope by **employee** or **device**.

   * **Employee**: Restricts the employee scope by **department**, **role**, or specific **member**.

   * **Device**: Restricts the device scope by **device**, **operating system**, or **device group**.

* **Software**: Select the internal applications to which this policy applies. You can select specific **application names** or **application tags**. The application data here comes from the "Proxy App" resource library configured in the system. If the application you need is not in the list, go to the **Zero Trust Access** \> **Application** \> **Proxy App** page to create and define the resource first. For more information, see [Manage proxy applications](https://docs.byteplus.com/en/docs/sealsuite/management-agent-mode-application-resources).

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1"><strong>Configuration efficiency note</strong>   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">To ensure that the application traffic authorized here is correctly taken over by the SealSuite client, we recommend setting the action to <strong>"Route by permissions"</strong> when you configure the <a href="https://docs.byteplus.com/en/docs/sealsuite/configuring-proxy-mode-traffic-diversion-strategy">traffic routing policy</a>. In this mode, the traffic routing scope automatically follows ACL authorization updates here in real time. Manual maintenance is not required, which prevents policy failures caused by inconsistent configurations at the source.   </div>
   

 &nbsp;

<span id=".6auY57qn6YWN572u"></span>
### Advanced settings

Supports more fine\-grained conditional control based on device admission status and the network process that initiates access. If the basic "personnel + device" authorization dimensions cannot meet your security requirements, use the configurations here to enforce additional access conditions.

 &nbsp;

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Advanced conditions apply only to PC clients (Windows, macOS, and Linux). Mobile clients (iOS and Android) skip these conditions during policy matching.</div>


<span id=".6Kem5Y-R5Zy65pmv"></span>
#### Trigger scenario

Administrators can decide whether to allow access based on the real\-time health status of devices, such as whether prohibited software is installed or whether the device is infected with a virus. Select a configured trigger template from the drop\-down list. If no template is configured, click **Go to Manage Trigger Templates** on the right to add one.

On the **Trigger template library** page, click **Add template** to create a new admission condition combination.

&nbsp;


|Configuration item |Configuration description |
|---|---|
|**Template name** |Customize an easy\-to\-identify name, such as "High\-risk device template". |
|**Template description** |Provide a brief description of the template purpose. |
|**Trigger configuration** |When you add a template, you can flexibly combine trigger conditions across multiple risk status dimensions and antivirus status dimensions based on different security control scenarios. Click **Add Condition** to combine multiple groups of rules.<br><br>The proxy gateway cannot directly scan endpoint files or processes. All condition judgments under trigger configurations are implemented by consuming alert data reported by the SealSuite client. Therefore, effective risk status conditions strongly depend on corresponding detection policies issued in the relevant modules.<br><br><br>* **Risk status**<br><br>   The proxy gateway integrates with the inspection capability of **Endpoint Security Baseline** and uses real\-time device risk alert events as the basis for ACL access control. All trigger conditions of the risk status type strongly depend on the [control policies](https://docs.byteplus.com/en/docs/sealsuite/docs-control-rules) issued in the **Endpoint** \> **Endpoint Management** \> **Endpoint Baseline** module. The client scans and reports alert events only after you configure and enable detection rules for specific software or processes in the baseline module. These alert events make the ACL control conditions here take effect. Note that to control specific software or processes, you must first add the corresponding [detection rules](https://docs.byteplus.com/en/docs/sealsuite/docs-configure-detection-items) to the baseline policy. The software or processes then appear in the configuration list.<br><br>* **Anti\-virus status**<br><br>   The proxy gateway integrates with the **Endpoint Antivirus** component and uses real\-time virus scan alert events on devices as the basis for ACL access control. All trigger conditions of the antivirus status type strongly depend on the [virus detection policies](https://docs.byteplus.com/en/docs/sealsuite/docs-policy-configuration) issued in the **Endpoint Security** \> **Endpoint Antivirus** module. The ACL control conditions here take effect only after the client performs a virus scan and reports malicious file alert events to the backend. |


**Configuration example: Prevent devices with prohibited download tools installed from accessing an internal code repository**

To help you better understand how endpoint policies coordinate with ACL advanced trigger policies, this example shows the complete operation path for the business requirement "Block devices with prohibited download tools installed from accessing an internal code repository (GitLab)":


1. **Step 1: Configure the endpoint baseline (define and discover risks)** 

   In the **Endpoint** \> **Endpoint Management** \> **Endpoint Baseline** module, add the target prohibited download tool, such as specific P2P software, as an "application detection item". Then configure it in an endpoint control policy and issue it to all employees. After the client scan detects the software, the client reports an alert event to the backend.

2. **Step 2: Configure an ACL policy (block based on risk)** 

   In **Proxy Policy** \> **ACL Policy**, create an Access Policy, set the action to **Reject**, and select the internal code repository, such as GitLab, as the application. In **Trigger scenario**, select **Risk status** \> **Non\-compliant software installed on the device**, and select the download tool defined in Step 1.

3. **Final result**: When an employee tries to access GitLab, the proxy gateway checks the device security status in real time. If the device has alert records for the prohibited software, the gateway directly blocks the access request to enforce device\-based access control.


 &nbsp;

<span id=".6L-b56iL"></span>
#### Process

After this feature is enabled, only specific client processes are allowed or denied access to the target application. For example, you can allow only the company\-issued Chrome browser process to access core business systems. This blocks access requests from malicious crawlers, scripts, or non\-standard browsers.

Turn on the **Process** configuration switch, click **Select process** on the right, and select an existing process on the **Process library** page that appears or click **New process** to add a process.

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/2026-09-24/proxy-en-review/process-new-ready.png) </span>


* **Configuration rules**

   In the new process window that appears, configure specific process identification rules based on the operating system (Windows or macOS). Click **Add Condition** to combine conditions across the following dimensions:

   * **Process name**: The executable file name of the process, such as `chrome.exe`.

   * **Process signature**: The digital signature publisher information of the process file.

   * **Process path**: The installation or execution path of the process on the device.

* **Configuration recommendations (prevent false blocks)** 

   To improve block accuracy, we recommend the following configurations:

   * **Prioritize signatures**: For legitimate signed software, we strongly recommend **combining "process name + process signature"** . Relying only on "process name" can be easily spoofed by malware or duplicate the name of other common system programs. This can cause security policies to be bypassed or falsely block traffic. Digital signatures can verify the genuine software publisher at the cryptographic level.

   * **Avoid broad paths (Windows)** : In Windows, avoid using a broad drive path such as `C:\` as the only condition. Otherwise, the client includes network requests from all programs in that directory, including core system services and antivirus software, in the control scope. This can easily disrupt core business operations. Always combine path conditions with other fields.

   * **Note signature differences (macOS)** : Due to the Apple distribution mechanism, the underlying digital signature identifiers of the same software are usually different when the software is downloaded from the official software website with a developer signature and from the Mac App Store with an official Apple distribution signature. Therefore, pay close attention to the enterprise software distribution channel during configuration to avoid missed blocks.


 &nbsp;

<span id=".566h55CGLWFjbC3nrZbnlaU="></span>
## Manage ACL policies

Administrators can search for and adjust created policies on the **ACL Policy** list page.


* **Filter and search**: Quickly filter by policy name, action, status, and application address, such as IP address, domain name, or wildcard domain name.

* **Manage effective status**: Use the status switch in the **Actions** column to enable or disable a policy with one click.

* **Edit and delete**: Click **Edit** to modify the policy configuration. Click **Delete** to remove obsolete policies. Before deletion, assess risks based on the current default access mode of the gateway. Make sure deletion does not accidentally block legitimate access or expose sensitive resources.


 &nbsp;

<span id=".5Luj55CG6K6_6Zeu5pel5b-X5a6h6K6h"></span>
## Audit proxy access logs

After ACL policies are configured, click **Audit Logs** \> **Proxy Layer 4 Access Log** in the Admin Console. View proxy access logs to verify policy effects.

In the log list, click **Log Details**. Analyze and resolve access issues from the following four dimensions.


* **Basic information**: Confirms the **employee identity** and **device status** that initiate access. This helps verify whether the account is normal and whether the device is a managed endpoint.

* **Access behavior**: The core logical evaluation area.

   * **Matched policy**: Clearly shows which policy the current traffic matches. This helps troubleshoot policy conflicts or priority configuration errors.

   * **Action and status**: Clearly shows whether the action is "Allow" or "Reject". If access fails but the log shows "Allow", check the status of the backend application service.

* **Forwarding path**: Reconstructs the network path.

   * **Access Gateway**: Confirms which gateway the traffic passes through. Abnormal gateway status or incorrect DNS resolution addresses can cause access timeouts.

   * **Traffic tracing**: If no matching logs appear, verify the log filters and check whether the scope of the **traffic routing policy** covers the target application.

* **Endpoint attributes**: Provides in\-depth security audit.

   * **Process tracing**: Displays the specific **process name, path, and signature** that initiate the request. This helps identify whether unauthorized plugins, malicious scripts, or unauthorized software are trying to connect to intranet assets.
