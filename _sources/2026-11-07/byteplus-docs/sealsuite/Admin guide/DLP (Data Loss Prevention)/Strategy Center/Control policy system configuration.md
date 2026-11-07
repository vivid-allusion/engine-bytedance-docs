---
title: "Control policy system configuration"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-system-settings-for-file-egress-control-policies"
---

**System configuration** defines the global settings for the SealSuite DLP policy control module. By centrally defining how all clients consume resources, schedule scans, and handle evidence collection during sensitive data detection, administrators can balance enterprise data security against endpoint performance — minimizing the impact of continuous DLP monitoring on employee experience.

**Operations tip**: Continuous DLP monitoring inevitably consumes endpoint resources. If you notice abnormal CPU, memory, or bandwidth usage on a device, we recommend adjusting the global settings in this document first, or checking whether any audit policies are too broad or too aggressive. For example, try temporarily disabling the **File archiving** option on certain policies, or disabling the entire policy, to quickly isolate the source of the performance bottleneck.

<span id="7ba5fca6"></span>
## Prerequisites

Administrators need the following permissions. To add them, see [Configuring Administrator Access](https://docs.byteplus.com/docs/sealsuite/docs-adding-administrator_1).


* Menu permission: **Security** \> **DLP** \> **Strategy Center** \> **System Configuration**.

* Action permission: **DLP** \> **View policy management general config / Edit policy management general config**.


<span id="0eaf376f"></span>
## Scan resource configuration

Fine\-tune how SealSuite clients consume endpoint system resources when running detection tasks.


1. Log in to the Admin Console.

2. In the left navigation pane, choose **DLP** \> **Strategy Center** \> **System Configuration**.

3. Switch to the **Scan resource configuration** tab and click **Edit** on the right to configure the following.

   
   |**Section** |**Setting** |**Description** |
   |---|---|---|
   |**Full disk scan configuration** |Full Disk Scan |Controls the activation of the Full Disk Scan feature. When enabled, SealSuite periodically scans endpoint drives to identify sensitive "data at rest"—files already residing on the system. While this ensures a comprehensive security audit of legacy data, it leads to higher resource consumption. You should evaluate your security requirements before choosing one of the following scan frequencies:<br><br><br>* **High (Every 3 days)** : Facilitates rapid discovery of sensitive files at rest but results in more frequent system overhead.<br><br>* **Low (Every 10 days)** : Minimizes the impact on endpoint performance, though there may be a delay in identifying sensitive data. |
   |**Resource usage configuration** |Maximum CPU usage |Sets a maximum CPU usage threshold for the SealSuite client during high\-load operations, such as system scans, to ensure user productivity remains unaffected.<br><br>Adjustable between 10% and 50%, this setting involves a trade\-off: higher values accelerate scan completion but may reduce the responsiveness of other active applications, while lower values prioritize system performance over scan speed. |
   |**File parsing configuration** |Single file content parsing configuration |Specifies the maximum file size for deep content parsing across various file types. This limit is designed to prevent the client from exhausting system resources when handling oversized files; any file exceeding the threshold will bypass deep content inspection. |
   ||Nested file parsing configuration |Defines the maximum depth for parsing multi\-layered compressed or nested files. If "Synchronize the directory structure reporting" is enabled, alert details will include the full path of the sensitive file within the archive. |
   ||File scan timeout limit |Defines the maximum duration the system spends scanning an individual file.<br><br><br>* **Idle Scan Timeout**: Applies to background operations, such as Full Disk Scans. Since these tasks are non\-intrusive and invisible to the user, a longer timeout (10s–300s) is recommended to ensure deep and comprehensive inspection of legacy data. If a file exceeds this limit, the scan is skipped.<br><br>* **Outbound Scan Timeout**: Sets the maximum time the system scan a single file during a file transfer action (1s–30s). The default is 5s. This setting affects both audit depth and user experience. Set a reasonable timeout based on your organization’s security and usability needs to balance detection effectiveness with operational smoothness. If the scan is not completed before the timeout expires, the system automatically allows the file transfer. |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Setting thresholds in the <strong>File parsing configuration</strong> acts as a critical "circuit breaker" for client performance. When a file fails to be fully scanned because it exceeds these thresholds, the system automatically attaches a <strong>File Scanning Status</strong> tag (such as "Exceeded Parsing Time," "Exceeded Parsing Size," or "Exceeded Nesting Depth") and either skips the scan or allows the file to pass. To prevent these files from becoming security blind spots, you can use these status tags to create secondary sensitive data rules:</div>



1. <div data-tips="true" data-tips-type="tip">On the <strong>Sensitive Data Repository</strong> page, define files with these abnormal scanning statuses as a new sensitive data type.</div>


2. <div data-tips="true" data-tips-type="tip">In your <strong>File Transfer Control Policies</strong>, set specific audit and blocking rules for files carrying these tags.</div>



<span id="ecf2276c"></span>
## File content snippet reporting configuration

This feature allows the system to capture only the text immediately surrounding a sensitive keyword rather than the entire original file.

<span id="66f7b41e"></span>
### Configuration Procedure


1. Navigate to the **General** tab.

2. In the **File content fragment reporting configuration** section, click **Edit** and configure the following:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Enable Reported file content snippet** |Toggles the feature. When active, audit logs will display the context of sensitive hits. |
   |**Fragment context length** |Number of characters to capture before and after a sensitive hit (1–100). For example, a value of 50 captures 50 characters on either side, automatically preserving line breaks for readability. |
   |**Single file upload fragment limit** |Limits the number of unique text fragments reported for a single violating file (1–50). If a file contains multiple hits, they are reported in order until the limit is reached. |
   


<span id="dbcb4b4a"></span>
### Capture Logic Highlights


* **Smart Merging**: If two sensitive hits are close enough that their context windows overlap, the system merges them into a single, continuous snippet to avoid redundant data.

* **Multi\-Format Support**:

   * **Text/Office Files**: Direct text extraction.

   * **Images**: Snippets are generated based on OCR (Optical Character Recognition) results.

   * **Compressed/Code Files**: Includes the **full path and filename** within the archive to ensure a complete chain of evidence.

* **Reporting Constraint**: Snippet reporting is only triggered for **content\-based** rules. It will not trigger for metadata\-only violations (e.g., blocked file extensions or filenames).


<span id="86c4a70d"></span>
## Evidence file configuration

Centrally manage the full lifecycle of alert evidence, including evidence capture timing (screenshot mode), client\-side cache policies, upload bandwidth limits, and server\-side long\-term storage. The configuration here helps ensure the integrity of the audit evidence chain while minimizing the impact of evidence collection on endpoint performance and system privacy prompts.


1. Log in to the Admin Console.

2. In the left navigation pane, choose **DLP** \> **Strategy Center** \> **System Configuration**.

3. Switch to the **Evidence file configuration** tab configure the following.


<span id="5dfef9f3"></span>
### Screenshot configuration for evidence collection

Administrators can configure screenshot evidence capture modes independently for endpoints running different operating systems. The available modes differ significantly in trigger logic, endpoint experience, and applicable scenarios. Please select the mode based on actual requirements.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This is a global underlying configuration. The system will execute screenshots according to the mode configured here only when the <strong>Screenshot</strong> action is enabled in the specific <strong>Document outgoing control</strong> or <strong>Clipboard control policy</strong>.</div>



|**Configuration mode** |**Description** |**Applicable Scenarios and User Experience** |
|---|---|---|
|**Periodic screenshots** |The endpoint automatically captures the screen at fixed intervals and stores the screenshots locally in cache (1 second on Windows and 3 seconds on macOS). When an outbound file transfer is detected, the system immediately retrieves the most recent screenshot as evidence and reports it. |**Advantages**: Provides complete evidence coverage before, during, and after the outbound file transfer.<br><br>**Disadvantages**: On macOS 14+, this mode may frequently trigger system privacy prompts, which interferes with employees’ normal work. |
|**Outgoing screenshot** |Screenshot capture at fixed intervals is triggered only when an outbound file transfer is detected. For repeated transfer actions within 1 second, the system automatically reuses the most recent screenshot as evidence and reports it. |**Advantages**: Significantly reduces the frequency of privacy prompts on macOS 14+, minimizing disruption to employees’ normal work.<br><br>**Disadvantages**: As screenshots are taken less frequently, the outbound file transfer activity may not be captured in full. |



1. In the **Screenshot configuration for evidence collection** at the top, click **Edit** on the right.

2. In the window that appears, complete the following configuration:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cfdc2a229074e2ba04d624825d9ea2b~tplv-goo7wpa0wc-image.image) </span>

   * **Windows**: Fixed to **Periodic Screenshots** and cannot be changed. Periodic screenshots on Windows run silently without privacy prompts, so the employee’s experience is not affected.

   * **macOS**:

      * For macOS clients version **3.3.15 and later**, you can choose either **Periodic screenshots** or **Outgoing screenshot**  **(recommended)** .

      * For macOS clients earlier than version **3.3.15**, the system still uses **Periodic** **Screenshots**.

3. Click **Confirm** to complete the configuration.


<span id="38c613fc"></span>
### Forensic file configuration

Manage client\-side caching and upload of alert\-related evidence files, as well as server\-side storage policies.

Click **Edit** on the right side of **Forensic file configuration** and complete the following configurations:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c57505c24e764277a2edf1729f93b853~tplv-goo7wpa0wc-image.image) </span>


|**Setting** |**Description** |
|---|---|
|**Single device forensic file upload rate limit** |Limits the maximum network speed per device when uploading evidence files. This prevents high\-volume uploads from consuming excessive upstream bandwidth and impacting other business operations. |
|**Alarm and evidence file upload time** |Sets how long the client waits before uploading alerts and evidence to the Admin Console after an event is detected. If set below 5 minutes, it may impact device network performance. Extending this delay can help distribute network pressure. |
|**Retention Period for Evidence on Desktop Client** |The maximum duration that unsent evidence files are stored on the local disk of the SealSuite client. Range: 1–7 days. A longer period ensures that offline devices can upload evidence once they reconnect but increases local disk usage. |
|**Retention Period for Evidence on SealSuite Server** |Defines how long uploaded evidence is kept in the Admin Console. This directly impacts server storage consumption. Set this according to your enterprise data retention and compliance policies.<br><br>> Keeping files for more than 15 days may impact storage space. Enter 0 for permanent storage. |
|**Server\-side Storage Node** |Select the object storage service used for evidence files. The system supports built\-in storage or integration with external object storage. |
|**Evidence file upload size limit policy** |Allows you to create multiple policies with different retention rules based on file type and target scope.<br><br><br>1. Click  **+ New Policy**.<br><br>2. Configure the following.<br><br>   * **General**: Name and Priority (higher values are matched first).<br><br>   * **Limit configuration**: Set a unified upload limit for all file types, or enable **Personalized configuration** to define specific limits for different file types (useful for prioritizing high\-risk formats).<br><br>   * **Scope**: Define the users or devices this policy applies to. |


<span id="645581b7"></span>
## Browser plug\-in control configuration

Centrally manage the enablement status and scope of the SealSuite browser security extension.

When the extension is enabled, it provides deep control over browser behavior, significantly improving the accuracy of SealSuite DLP's outbound behavior detection and log completeness in web scenarios (for example, supporting classification inheritance when downloading Feishu/Lark cloud documents).

<span id="82912cbe"></span>
### Prerequisites


* **Environment requirements**: The extension currently supports Chrome and Edge browsers on Windows 10 or later and macOS 11 or later.

* **Version requirements**: Only applies to SealSuite client version 3.3.12 or later.


<span id="60c46c3b"></span>
### Procedure


1. Log in to the Admin Console.

2. In the left navigation pane, choose **DLP** \> **Strategy Center** \> **System Configuration**.

3. Switch to the **Browser plug\-in control configuration** tab and click **Edit** on the right.

4. Turn on the **Enable browser extension management** toggle to enable the ability to control browser behavior through the extension.

5. Complete the following configuration:

   
   |**Field** |**Description** |
   |---|---|
   |**Browser plugin management configuration** |After enabling extension control, you can customize how the extension appears in employees' browser extension lists:<br><br><br>* **Custom plugin icon**: Use the default system icon, or upload a custom enterprise logo (delete the default icon first, then upload).<br><br>* **Custom plugin title**: Supports names in both Chinese and English (default: SealSuite Browser Security Extension).<br><br>* **Custom plugin description**: Briefly describe the extension's security protection purpose.<br><br><br>You can preview the appearance in the **Browser plugin style preview** area below. |
   |**Scope** |Define the scope of extension control by **employees** (by department/role/member) or **devices**. To exclude specific sub\-departments or individual employees from a large department that is already in scope, enable **Exclude object** below and select the target objects. Excluded objects will not be subject to extension control. |
   

6. Click **Confirm** to save.


<span id="1603bb11"></span>
### Expected results

After saving the configuration, the system deploys and controls the extension as follows:


* **Automatic deployment and installation**: For endpoints within the target scope that meet the environment requirements, the SealSuite client automatically and silently pushes and installs the SealSuite Browser Security Extension into supported browsers (such as Chrome and Edge). No employee action is required.

* **Employee experience**: After installation, employees will see the extension in their browser's extension bar (displayed with your custom icon and name). The extension runs silently in the background and does not interfere with normal web browsing or operations.

* **Security control enforcement and next steps**: Once the extension is enabled, the system has the foundational capability for deep control over browser download behavior. You can then go to the **Data Identification** module to configure specific identification sources. For example:

   * **Inherit Feishu/Lark document classification**: If you want files downloaded from Feishu to automatically inherit their original security classification, go to **File source library** and add a source rule with the type "Feishu/Lark cloud document". For details, see [Managing the File Source Library](https://docs.byteplus.com/docs/sealsuite/managing-the-file-source-library).


<span id="cc404e17"></span>
## Agent plug\-in control configuration

This feature serves as the basic switch for controlling tool execution in specific AI Agents. After it is enabled, the SealSuite client can identify internal interaction behaviors of AI Agent tools, enabling precise audit and blocking of outbound behaviors in AI scenarios.

<span id="6129eb8f"></span>
### Prerequisites


* **Controlled tool scope**: To perform fine\-grained behavior audit and blocking for the four desktop AI application tools **EasyClaw, OpenClaw, QClaw,**  and **StepClaw**, you must enable the plugin control switch here and ensure that the endpoint plugin is loaded successfully before configuring a [document outgoing control policy](https://docs.byteplus.com/en/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule). For other types of AI applications supported by the document outgoing control policy, you do not need to enable this switch. You can directly select the corresponding channel in the policy configuration to enable control.

* **Supported systems**: Windows and macOS.

* **Version requirement**: This feature takes effect only on SealSuite client version **3.3.16 or later**.


<span id="84b755fb"></span>
### Procedure


1. Log in to the Admin Console.

2. In the left navigation pane, choose **DLP** \> **Strategy Center** \> **System Configuration**.

3. Switch to the **Agent plug\-in control** tab and click **Edit** on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccbf14a6247c48e7ae916ebf0485db3c~tplv-goo7wpa0wc-image.image) </span>

4. Turn on the **Enable Agent plug\-in control** toggle.

5. Based on your enterprise control requirements, select the AI Agent tools to control.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e26d9f40309849b3915dc28888b40f06~tplv-goo7wpa0wc-image.image) </span>

6. **Scope**: You can define the effective scope of this control capability by **User** or **Device**:

   * When selecting **User**, you can restrict the scope by **Department** or **Role**.

   * When selecting **Device**, you can restrict the scope by specific **Device**, **OS**, or **Device Group**.

   * Turn on the **Exclude objects** switch below to exclude specific objects. The final effective scope is effective scope minus excluded objects.

7. Click **Confirm** to save the configuration.


<span id="b024987a"></span>
### Expected results

After you complete and save the preceding configuration, the system deploys the plugin and enforces control based on the following logic.


* **Restart required for the configuration to take effect (important)** : Enabling or disabling the Agent plugin control switch, as well as installing or uninstalling plugins, takes effect only after **the SealSuite client application on the endpoint is restarted**. Be sure to notify the relevant employees to restart the application.

* **Silent deployment and running**: For endpoints that are within the **Scope** and meet the version requirement, the SealSuite client automatically and silently installs the Agent control plugin into the runtime environment of the controlled tool. The plugin runs silently in the background throughout the process and does not interrupt employees' normal work.

* **Next steps**: Enabling the switch here only means that SealSuite has the basic capability to identify internal interaction behaviors of AI Agents. To perform specific blocking or logging actions, go to the [document outgoing control policy](https://docs.byteplus.com/en/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule) page, select the corresponding AI application in the **Control channel**, and configure the corresponding sensitive data filtering rules.


<span id="eb85e6bc"></span>
## IM receiver audit configuration

Instant messaging is the most common data interaction channel in enterprises. By default, SealSuite only records which chat software was used for an outbound transfer. Enable this audit feature to collect **receiver information** (such as receiver name, personal/group type, and internal/external attribution). This helps security administrators accurately define the scope of a data leak (e.g., whether a file was sent to a competitor), improving traceability.

Because enabling this feature impacts the user experience differently on Windows and macOS (macOS requires mandatory permissions and system prompts), SealSuite supports independent configurations per OS and channel. This allows you to balance security demands with the employee experience.

<span id="d13b1fc4"></span>
### Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, select **DLP** \> **Strategy Center** \> **System Configuration**.

3. Click the **Instant messaging receiver audit** tab and click **Edit**.

4. Turn on the **Chat software permission management** master switch.

5. Configure the **Windows** and **macOS** system cards based on your enterprise's requirements. After enabling the master switch, select the specific IM channels below.

   
   |OS |Interaction and permission details |
   |---|---|
   |**Windows** |Windows has no special permission requests. The SealSuite client silently collects receiver information in the background without employee awareness. |
   |**macOS** |Due to strict macOS privacy protections, SealSuite requires specific system permissions to collect receiver information from chat windows.<br><br><br>* **Channel permission requirements**<br><br>   * Enabling any audit channel requires the endpoint to grant the "Accessibility" permission.<br><br>   * If you enable the "**WeChat**" channel, technical limitations require the endpoint to also grant the "Screen Recording" permission.<br><br>* **Endpoint experience and compliance risks**<br><br>   Enabling macOS audit channels directly impacts the user experience. If the endpoint lacks the necessary permissions, the SealSuite client displays a **Permission guidance window**, prompting the employee to grant authorization in System Settings. Otherwise, the control fails. Additionally, **macOS 14 and later** features strict anti\-screenshot prompts. If an employee grants "Screen Recording" for "**WeChat**" auditing, the system menu bar occasionally displays "SealSuite Assistant is capturing your screen". We **strongly recommend issuing internal compliance announcements and managing expectations** before enabling this feature to alleviate employee privacy concerns. |
   

6. Configure effective scope: Define the scope by **User** or **Device**.

   * By **User**: Restrict by **Department** or **Role**.

   * By **Device**: Restrict by **Device**, **Operating system**, or **Group**.

   * Enable the **Excluded object** switch to exclude specific targets. The final scope is the **Effective scope** minus the **Excluded object**.

7. Click **Confirm** to save the configuration.


<span id="54258937"></span>
### Log audits

When an employee within the effective scope triggers an outbound file alarm via a controlled IM application, administrators can view the details under **Investigation audit** \> **Audit log** \> **File Sharing Log**. In the log's **Basic information** section, the system supplements the basic route data with receiver\-specific details under **More information** (based on the channel type).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84be128b2c9847c2a4aedc64f45ac97e~tplv-goo7wpa0wc-image.image) </span>
