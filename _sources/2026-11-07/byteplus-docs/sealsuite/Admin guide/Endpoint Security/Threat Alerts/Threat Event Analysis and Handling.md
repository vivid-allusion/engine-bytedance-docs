---
title: "Threat Event Analysis and Handling"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/threat-event-analysis-and-handling"
---

In traditional endpoint security operations, administrators often face the dual challenges of "alert fatigue" and "broken traceability chains": a single\-point alert, such as an abnormal outbound connection from a process, can only reflect the final manifestation of an attack, but cannot intuitively present the original source of the attack.

The SealSuite **Threat Events** feature introduces higher\-level aggregation and analysis capabilities. It automatically links multiple related threat behaviors and malicious file alerts scattered across endpoints, and uses a **trace map** to reconstruct the complete attack path. This helps security administrators shift from "handling isolated alerts" to "operating complete events", improving efficiency across the full process from risk discovery and path tracing to closed\-loop handling.

<span id="1ddda10f"></span>
## Core Value


* **Locate the Root Cause of Attacks**

   Through full behavior backtracking, the system automatically locates the starting node of an attack chain. For example, it can identify the original download source, entry process, or associated parent execution chain that caused a malicious payload to be written to disk, helping administrators cut off risks at the source.

* **Identify Latent Persistence Mechanisms**

   Through in\-depth chain tracing, the system identifies hidden entities created by attackers to achieve long\-term persistence, including but not limited to hidden scheduled tasks, abnormal registry startup items, or disguised system services. This ensures that latent threats are thoroughly cleaned up.

* **Improve Assessment and Response Efficiency**

   The system converts fragmented raw logs into an intuitive topology graph, addressing the lack of context in single\-point alerts. It reduces the cost of correlation analysis for complex events, enabling administrators to quickly assess the impact scope of threats and issue handling instructions.


<span id="1789f561"></span>
## Feature Linkage Logic

To understand Threat Events, you need to understand their hierarchy and data flow in the SealSuite EDR system:


1. **Data foundation (EDR logs)** : Continuously records full raw behavior data from endpoints, providing basic evidence for security analysis and post\-incident audits.

2. **Single\-point alerts (Threat Behavior / Malicious Files)** : Refines raw logs based on detection rules and marks risky single\-point behaviors or malicious files.

3. **Assessment center (Threat Events)** : Serves as the core logic processing layer. Through entity correlation technologies, such as process chains, file hashes, and target network addresses, it aggregates scattered single\-point alerts into attack events with contextual relationships, resolving information chain breaks.

4. **Closed\-loop handling (Threat Response)** : Based on event assessment conclusions, administrators can directly trigger response instructions, such as terminating processes or isolating files, to perform targeted response actions.


<span id="6f759944"></span>
## Trace Map Elements

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2f16871cff148f9a295a03be36ee75a~tplv-goo7wpa0wc-image.image) </span>


* **Node Types**

   Nodes represent specific entities on the endpoint.

   * **Process**: A running program instance, labeled with its name and PID.

   * **File**: A static file entity on disk.

   * **Persistence object**: Includes services, scheduled tasks, registry startup items, and shortcuts.

   * **Network**: A target IP address or domain name.

* **Node Color Levels**

   * 🔴 **Red**: Entity associated with a high or medium confidence alert, which is also the trigger cause of a single event.

   * 🟡 **Yellow**: Entity associated with a low\-confidence risk.

   * 🔵 **Blue /**  ⚪ **Gray**: Normal system process or entity that provides contextual background.

* **Edge Logic**

   Edges represent interaction actions between entities.

   * **Solid line (behavior line)** : Represents a clear action type, such as "Spawned", "Write file", or "Resolve domain".

   * **Dashed line (correlation line)** : Represents a weak logical correlation. For example, it identifies the mapping between a running process and its physical file entity, or connects multiple registry items with the same parameters.


<span id="4216eb53"></span>
## Operation Guide

<span id="28a59fdd"></span>
### 1. Access the Page


1. Log in to the Admin Console.

2. In the left navigation pane, go to **Endpoint Security** \> **Threat Events**. When an endpoint triggers a medium or high confidence alert, the system automatically generates a risk event and displays it in the **Threat Events** management list. Administrators can use "Last Active Time" and "Event Status" to preliminarily assess the urgency of the threat and determine whether immediate analysis is required.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1adf2501684c4f839eb70c1f771594a8~tplv-goo7wpa0wc-image.image) </span>

3. In the event list, click **Details** in the **Action** column of the target event to enter the event details page. Administrators can quickly identify the employee, endpoint device, operating system, and other entities associated with the threat. Based on this entity information, administrators can quickly assess whether the threat involves core business personnel, as well as the organization, security status, and compliance baseline of the related device, providing necessary environmental context for subsequent risk assessment.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad0984dbcb3a4e798f5912ac794881f8~tplv-goo7wpa0wc-image.image) </span>

4. On the details page, select the **Original Trace Map** tab. Administrators can use the trace map to intuitively understand the attacker's lateral movement traces, persistence strategy, and disguise behaviors intended to hide their true intent, achieving a shift from "seeing the alert" to "understanding the attack".


<span id="23ed1ecb"></span>
### 2. Review Node Attributes and Perform Forensics

Click any node in the trace map. The sidebar displays detailed metadata of the entity, providing administrators with in\-depth forensic evidence.


* **Identity and Legitimacy Check (Process / File)** 

   The system highlights the entity's execution path, command\-line arguments, hash values (MD5/SHA1), and digital signature status. Administrators can quickly determine whether the node is a disguised or tampered entity by checking whether the command line contains malicious instructions and whether the signature is valid or abnormal.

* **Persistence Mechanism Review (Service / Task / Registry)** 

   For system resident items, the system displays the startup type, trigger, executable file path, and specific registry key\-value content. By reviewing the execution frequency and execution path, administrators can determine whether the node is being used as a persistence backdoor by attackers.

* **Communication Characteristics and Threat Intelligence Correlation (Network)** 

   The system displays information such as source IP/port, destination IP/port, connection direction, and resolved domain names. Administrators can use this information to verify the source and destination of traffic and determine whether abnormal outbound communication exists.

* **Risk Correlation Information**

   If a node is involved in an alert, the sidebar also displays the **Related alert Information**. Administrators can view the alert name, threat level, and detection basis triggered by the node, enabling quick alignment between behavior in the trace map and underlying logs.


<span id="80af9490"></span>
### 3. Response and Handling

After completing trace analysis and confirming the threat, administrators can perform response actions in the following two ways to achieve physical risk containment and operational closure.


1. **Handle Risk Entities**

   On the **Associated Handling Items** tab, issue blocking instructions for specific infected entities to immediately interrupt attack behaviors. After a task instruction is issued, a record is also synchronized to the [Threat Response](https://docs.byteplus.com/en/docs/sealsuite/managing-threat-response-tasks) center.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d391a9bbd63241f7b90a83314f4f0ac2~tplv-goo7wpa0wc-image.image) </span>

   * **Process\-level response**: Execute **Finish**. Forcefully terminates the running malicious program to block its in\-memory activity and outbound network connections.

   * **File\-level response**: Execute **Isolation**. Moves the malicious payload to the isolation area and encrypts it to prevent it from being triggered or loaded again.

   * **Persistence item response**: Execute **Delete Scheduled Task**, **Delete Registry Startup Item**, or **Disable Service**. Cleans up resident backdoors left by attackers and prevents the threat from recurring after system restart.

2. **Assess the Threat Event**

   After containment actions are performed on the overall path, use the **Remediation** button in the upper\-right corner of the page to make a final assessment of the threat event and close its status.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49578971f9af41029c40f6a66ba49b89~tplv-goo7wpa0wc-image.image) </span>
