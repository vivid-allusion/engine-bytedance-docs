---
title: "Threat Behavior Analysis and Management"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/threat-behavior-analysis-and-management"
---

In Endpoint Detection and Response (EDR), continuous analysis of all behavior logs enables real\-time detection and identification of potential endpoint security threats. The **Threat Behavior** page serves as the operation center where administrators can centrally assess security alerts and issue response instructions.

With this feature, administrators can quickly determine the nature of a threat and issue response instructions for affected risk entities, such as files, processes, and services, to eliminate endpoint security risks.

<span id="b399b635"></span>
## Key Capabilities


* **Centralized alert assessment**: Aggregates scattered behavior alerts into actionable threat behaviors, helping administrators determine the nature of the alert based on attack details, such as “Real”, "False positive", or "Others".

* **Response instruction delivery**: For identified risk entities, administrators can directly issue response instructions on the page, such as “Isolation” for files and “Finish” for processes.

* **Visualized attack chain analysis**: Uses the ATT&CK attack matrix to visually display the attack stage and techniques associated with a threat, helping administrators evaluate the depth of the risk.


<span id="8cfaf09b"></span>
## Prerequisites

Threat behavior analysis and assessment highly depend on low\-level endpoint behavior telemetry. Before using this feature, ensure that you have configured and delivered an effective EDR log collection policy (see [Configuring EDR behavior collection policy](https://docs.byteplus.com/docs/sealsuite/configuring-edr-behavior-collection-policy)) through security policy configuration. If no collection policy is configured, the system cannot obtain endpoint behavior traces and therefore cannot generate threat behavior alerts.

<span id="2c533038"></span>
## Feature Relationship

To improve security operations efficiency, SealSuite EDR establishes a layered processing mechanism from raw data to threat events. It connects scattered signals into a complete evidence chain, helping administrators perform risk investigation and closed\-loop handling more accurately and efficiently.

<span id="9cae91a5"></span>
## Threat Behavior, Threat Events, and EDR Log


* **Data Extraction and Aggregation**

   * **EDR Log**: Serves as the lowest\-level evidence foundation and continuously records all raw behaviors that occur on endpoint devices, such as process startup, file read/write, and network connections.

   * **Threat Behavior (risk fragment)** : The system uses built\-in detection rules to extract insights from massive EDR logs. When raw behavior matches risk characteristics, a threat behavior alert is generated.

   * **Threat Events (complete storyline)** : To help administrators understand the full attack picture, the system further aggregates multiple logically related threat behaviors, such as those involving the same process chain or target IP address, and automatically connects them into a more complete threat event.

* **Use Scenarios and Operations Path**

   * **Daily assessment**: Administrators can usually operate by "Threat Events". By viewing the **Original Trace Map**, administrators can quickly understand the full attack context and perform one\-click handling, avoiding hidden risks that may be missed when only a single alert is handled.

   * **In\-depth tracing**: When handling events or investigating false positives, administrators can drill down to associated "Threat behavior" and locate specific raw **EDR logs**. By analyzing low\-level evidence such as file paths and command\-line parameters, administrators can complete a security closed loop from event conclusion to raw evidence.


<span id="89c645cc"></span>
## Threat Behavior and Threat Response


* **Threat behavior (instruction delivery)** : On this page, administrators assess risk entities and perform handling operations, such as applying “Isolation” to files and “Finish” to processes.

* **Threat response (task tracking)** : Instructions issued by administrators on the Threat Behavior page are converted into specific "response tasks." To track the delivery time, execution progress, and final result of a task, go to the **Threat Response** page for closed\-loop tracking.


<span id="e8ffb0e4"></span>
## Threat Behavior Dashboard and List Management

Log in to the SealSuite Admin Console and go to **Endpoint Security \> Threat Alerts \> Threat Behavior**. You can use the dashboard to gain a global view of threat dynamics across the network.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a2710df3e334bf6be58e99236738ca0~tplv-goo7wpa0wc-image.image) </span>


* **Threat Category Statistics Cards**

   The top of the Threat Behavior page provides a dashboard that automatically classifies threats by their nature.

   * **Threat scenario classification**: The system relies on **more than 4,000** built\-in detection rules to monitor and match endpoint behaviors in real time. Each preset rule is associated with a specific attack type tag, such as AI Agent, cybercrime, remote control, APT, and phishing. Once a behavior matches a rule, the system automatically classifies its attributes and synchronizes the result to the category statistics dashboard at the top of the page. Dashboard values reflect the total number of threat behaviors in each scenario within the currently selected time range, helping administrators quickly assess threat nature and intent and prioritize alerts in key categories based on risk trends.

   * **ATT & CK attack phase matrix**: Click the **ATT & CK attack phase** on the right side of the dashboard to expand the full matrix view. Administrators can intuitively evaluate the attacker’s penetration depth through "highlighted" technique nodes.

* **Assessment Categories and Filtering Tools**

   Administrators can use various filtering tools to locate specific alerts from the large volume of threat behavior alerts.

   * **Multidimensional filtering**: Supports combined filtering by assessment status, alarm name, alert subject, tag, ATT&CK attack phase, user information, device information, OS, and other dimensions.

   * **Customization capabilities**: Supports customizing the display of **Custom Filter** items and adjusting the list field display logic through **Columns**.

* **Threat Behavior List**

   The list displays detailed information about aggregated threat behaviors and supports the following operations:

   * **Assessment**: Click to determine the nature of an alert and mark it as "Real", "False positive", or "Others".

   * **Details**: Click to view the attack chain of the threat, associated logs, and execute specific response instructions for risk entities.


<span id="6843c383"></span>
## Threat Behavior Details Analysis

Click **Details** in the **Action** column of the Threat Behavior list to enter the in\-depth analysis page. This page integrates the threat assessment conclusion, risk item cleanup, and evidence tracing in a single view, helping administrators complete the closed loop from analysis to handling.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fceb225a37644098b71000c11fd31ec~tplv-goo7wpa0wc-image.image) </span>

<span id="27bf9d9d"></span>
### Risk Characteristic Overview

The top of the page displays key information about the threat behavior to help administrators evaluate the risk level.


* **Rule information**: Displays the Rule ID that triggered the alert, Confidence (high, medium, or low), and associated parent and child process names.

* **Quick assessment**: The **Assessment** button is provided in the upper\-right corner. If an assessment is found to be incorrect, administrators can re\-classify the threat as "Real", "False positive", or "Others" at any time.


<span id="099dded6"></span>
### Associated Handling List

Based on semantic analysis, the system automatically extracts and classifies risk entities directly associated with the threat.


* **Classified handling**: The list displays items by type, such as file, process, and service. Administrators can perform corresponding actions on individual entities.

   
   |Entity Type |Displayed Data |Handling Action |Logic |
   |---|---|---|---|
   |File |File name, file path |Isolation / Cancel isolation |Aggregates and displays records by "file path". Alerts with duplicate paths are merged into one record. |
   |Process |Process name (PID), executable file path |Finish / Cancel Finish |Aggregates and displays records by "process PID + executable file path". |
   |Service |Service name, executable file path |Disable service / Enable service |Aggregates and displays records by "service name". |
   |Scheduled task |Task name, startup program details |Delete scheduled task |Aggregates and displays records by "scheduled task name". |
   |Registry |Registry key, registry path |Delete registry |Aggregates and displays records by "registry path". |
   

* **Batch operations**: Supports selecting multiple risk entities and using the **Batch disposition** or **Batch restore** button at the bottom for efficient one\-click processing.

* **Response handling linkage mechanism**: After you click a handling action here (such as **Isolation** or **Finish**), the system issues handling instructions for the selected risk entities. This operation is converted into a response task and recorded on the **Endpoint Security \> Threat Response** page. After all risk items in the associated handling list are handled, the overall handling status of the threat behavior is updated from "Not Processed" or "Partially disposed" to "**All disposed**."


<span id="7f573593"></span>
### Evidence Tracing and Associated Investigation

The lower part of the page provides in\-depth investigation tools in tabs, allowing administrators to complete tracing without leaving the page.


* **Detailed log list**: Displays raw log records directly associated with the threat behavior.

   * **Embedded search**: Supports secondary filtering by log ID, event type, device name, and process file name within the details page.

   * **Log details redirection**: Click **View details** in the log **Action** column to further view the field attributes of the raw log.

* **User and device information**: Switch to this tab to quickly view detailed hardware information about the affected endpoint, the associated employee, and the employee’s organizational structure, helping evaluate the impact scope of the threat.
