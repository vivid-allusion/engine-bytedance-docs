---
title: "EDR Log Investigation and Analysis"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/edr-log-investigation-and-analysis"
---

**Log Investigation** is the core tracing center of the SealSuite EDR system. When investigating security events or assessing potential threats, the system provides basic filtering and advanced SQL\-like query capabilities to help security personnel quickly locate key evidence from massive endpoint behaviors, reconstruct attack chains, and achieve a security closed loop from alert discovery to root cause identification. This document describes how to use Log Investigation for efficient search and analysis.

<span id="74325750"></span>
## Log Search and Analysis

Go to **Endpoint Security** \> **Log Investigation**. Administrators can use filtering capabilities to search and analyze massive volumes of logs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f02906b589864e0c910751ed31c18f21~tplv-goo7wpa0wc-image.image) </span>

<span id="06abe0bb"></span>
### Filtering Modes

The system supports two filtering modes. The modes are **mutually exclusive**. After you switch modes, the currently effective filtering conditions are determined by the new mode.


* **Basic filter**: Provides fuzzy search for high\-frequency fields such as device name, event type, process/file name, and path. Click **Columns** to view all filter items and select the ones you want to add.

* **Advanced search**: Uses SQL\-like syntax for command\-based queries and supports more complex logical combinations. When you enter characters in the search box, the system automatically displays a code completion drop\-down list. When you use the up and down arrow keys (↑/↓) to preview candidate fields, you can view the **data type** and **detailed business meaning** of each field, helping administrators accurately build query statements.On the left side of the advanced search box, the following tools are provided for quickly managing query conditions:

   * **Favorites and management**: Click the "star" icon inside the search box to save the current complex statement to favorites. Click the "star" icon on the left side of the search box to view saved query statements.

   * **Query history**: Click the "clock" icon to quickly trace and reuse recent search conditions without rewriting the syntax.


<span id="369a5bf9"></span>
### Log List Interaction

By default, the log list is arranged in the order of "Time \> Subject \> Behavior \> Description" and supports highly customizable interactions:


* **Quick linkage menu**: Click a field value in a log record. The system displays a quick action menu:

   * **Copy**: Copy the specific value of the field to the clipboard with one click.

   * **Search**: Replace the value of the corresponding field in the current filtering conditions with this field value and start a new query.

   * **Add to search criteria**: Add this field value to the current filtering logic as an "AND" condition for progressive filtering.

   * **Exclude from search results**: Add this field value to the filtering logic as an "EXCLUDE" condition, allowing administrators to quickly remove operational noise or known safe items.

* **Customize field display**: Click **Columns** in the upper\-right corner of the list to select the fields to display and adjust their order.

* **View details**: Click **View details** in the **Action** column to enter the original log page.

   * **Log Information**: Displays grouped data that has been structured and normalized by the system. It is used for daily alert assessment and quick troubleshooting, helping security personnel intuitively understand the behavior context of core dimensions such as processes and files.

   * **Original Behavior Logs**: Displays the full underlying data collected by the probe in JSON format. This can be used for advanced threat hunting and detection rule tuning. Security personnel can extract uncommon hidden features or complete long payloads, and obtain accurate underlying field names (keys) to write advanced search statements or custom protection rules.

* **Export logs**: Click **Export logs** in the upper\-right corner of the page. The system generates a CSV file based on the current **Query result** and **Columns configuration**.


<span id="152860bf"></span>
### Understand Log Coordination

The Log Investigation page displays the most granular raw behavioral data of endpoints. To transform massive datasets into actionable security events, SealSuite automatically analyzes underlying data and distributes it to the corresponding high\-level security modules. During daily operations, administrators can leverage the following modules for closed\-loop remediation of detected security risks:


* **Dynamic behavior\-based alert interception**: When raw logs match specific attack models (such as cryptomining or ransomware), the system automatically aggregates the activity. Administrators can navigate to **Endpoint Security** \> **Threat Alerts** \> **Threat Behavior** to analyze aggregated attack chains and issue direct commands, such as "Terminate Process" or "Disable Service," to block threats. For more information, see [Threat Behavior Analysis and Management](https://docs.byteplus.com/docs/sealsuite/threat-behavior-analysis-and-management).

* **Static file\-based alert remediation**: While collecting endpoint file operation logs, the system extracts file hashes and compares them against the cloud Threat Intelligence database. If a malicious signature is matched, the system synchronizes the file to **Endpoint Security** \> **Threat Alerts** \> **Malicious Files** (the "Virus Scanning" list, with the data source labeled as "Threat Intelligence"). This allows administrators to perform physical remediation, such as isolation or deletion, from a unified interface. For more information, see [Malicious File Monitoring and Handling](https://docs.byteplus.com/docs/sealsuite/malicious-file-monitoring-and-handling).
