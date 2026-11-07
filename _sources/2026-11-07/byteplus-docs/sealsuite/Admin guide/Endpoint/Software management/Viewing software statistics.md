---
title: "Viewing software statistics"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-viewing-software-statistics"
---

**Software statistics** collects and reports information about software installed on employee endpoints, including basic software details and software license management information. Software statistics supports two types of software collection: **Application** and **Package**. It also provides deep identification and statistics for AI software and its associated extensions (such as OpenClaw and its Skills).

<span id="6f3b197c"></span>
# Notes


* Currently, only devices that have the SealSuite desktop client installed and logged in are supported, including macOS, Windows, and Linux devices.

* Software license management is only available on macOS and Windows.


<span id="0f6d4e86"></span>
# Viewing software statistics

<span id="12f28b11"></span>
## Enable software statistics


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Software** \> **Software List**.

3. When you access this feature for the first time, follow the on\-screen instructions to enable it and select the **software type** to collect.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfef2fd08e7f47fa90f80405010d8f8e~tplv-goo7wpa0wc-image.image) </span>

   * **Application**: Selected by default and cannot be cleared. When enabled, the system automatically collects standard office software and desktop clients running on endpoints (such as GUI\-based `.exe` or `.app` files) for basic asset inventory and license management.

   * **Package**: Optional. Use this option when you need to deeply identify and collect dependency libraries or command\-line tools running in specific environments (such as NPM packages, Python libraries, and so on).

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">In <strong>version 3.3.2</strong>, the package type only supports identifying and collecting <strong>OpenClaw</strong>. Starting from <strong>version 3.3.3</strong>, the package type supports deep scanning and collection of other development dependencies such as NPM packages and Python libraries.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Deep scanning of packages may consume a small amount of additional performance resources on endpoints. We recommend enabling this option only when your security management requirements call for it.      </div>
      


<span id="4daec728"></span>
## Viewing software statistics

After you enable software statistics, you can view the collected data on the **Software List** page.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When a device is active, the SealSuite client periodically collects software information from the endpoint and reports it to the cloud. To balance endpoint performance with data timeliness, data is updated <strong>once per hour</strong>, not in real time.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c017579dd2749daa0675ca36965404d~tplv-goo7wpa0wc-image.image) </span>

<span id="a1bebaed"></span>
### 1. Quickly locate and filter software

To help you find specific software in a large dataset, the page provides the following navigation and filtering capabilities:


* **Left category navigation**: SealSuite provides built\-in groups such as **AI Tools**, **Office Software**, and **Social Software**. Click a group to view its contents. Software that does not match any group rule is classified under **Ungrouped**.

* **Top quick filter bar**:

   * **Software type**: Quickly switch between viewing **All**, **Application**, or **Package** (if enabled).

   * **Operating system**: Select **Windows**, **Mac**, or **Linux** to view software distribution on a specific OS.

   * **Multi\-condition search**: Search by software name, Bundle ID / software publisher, current logged\-in user, department, or device information.


<span id="e290309c"></span>
### 2. Review the software statistics list

The main list provides an overview of the software that matches your current filter conditions, including the following key fields:


* **Basic software information**: Displays the full software name, operating system, and the software group it belongs to.

* **Software type and version**:

   * **Application**: Displays the current version number. When the system detects multiple versions of the same application, they are merged into a single record. Hover over the number to view all detected version numbers.

   * **Package**: The software type column additionally shows the specific package manager type (for example, `Type: python`).

* **Installation and usage coverage**: Displays the **number of endpoints with installation** (deduplicated by device), the **number of users with installation** (deduplicated by the employee currently logged in to the device), and the overall **installation rate** across the enterprise.


<span id="69a162e6"></span>
### 3. View software installation details

To focus on or troubleshoot specific software, click **Details** in the **Action** column to drill down into deeper installation metrics. The details page aggregates data to provide a comprehensive view across three dimensions:


* **Understand the global software overview**

   **Software information** tab displays basic attributes (such as version and official website), the first discovery time within the enterprise, and the total installation scale. If the software (such as Trae or OpenClaw) includes AI capabilities, the **Capability list** lets you quickly review which AI extensions (such as Skills) are installed. Click the statistics to trace these high\-risk or specific AI capabilities back to the exact devices and employees using them.

* **Troubleshoot specific device status**

   **Devices Installed** tab helps you locate specific software versions or identify devices with abnormal software states. Use the multi\-dimensional filters at the top (such as software version, AI capability name, or device status) to refine the list. You can view each device's installation time, running status, and specific installation path. Export this list for further security audits or verification.

* **Analyze employee usage distribution**

   **Users Installed** tab offers a personnel management perspective. Filter by department or role to understand how much specific teams rely on the software. The list shows each user's cumulative usage time and the number of endpoints where they installed the software. This data helps you evaluate procurement needs and establish employee usage guidelines.


<span id="a17f2497"></span>
### 4. Other management operations


* **Export reports**: Click **Export List** in the upper\-right corner. The system exports the statistics data that matches the current filter conditions to a `.csv` file for local archiving or further analysis.

* **Disable statistics**: If you no longer need to collect software data, click the **Software statistics enabled** button in the upper\-right corner, and then click **Disable** in the dialog box. After you disable the feature, employee devices will immediately stop reporting new software installation data.


<span id="9fea18ef"></span>
# Viewing top 20 software


1. Log in to the Admin Console.

2. In the left navigation bar, click **Dashboard**.

3. On the **Endpoints** tab, view the ranking of top 20 installed software.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecbf848e269c4cfe92f7692b7cc77287~tplv-goo7wpa0wc-image.image) </span>


<span id="e034c7de"></span>
# Managing software groups

SealSuite provides built\-in groups (such as AI Tools, Office Software, and Social Software). You can also create custom software groups tailored to your enterprise's needs to facilitate unified management and reporting.


1. Log in to the Admin Console.

2. In the left navigation pane, choose **Endpoint** \> **Software Management** \> **Software Statistics**.

3. At the bottom of the left group list, click  **+**  **New Software Grouping**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b48de4eed41b4a6792eb2b3bd291949f~tplv-goo7wpa0wc-image.image) </span>

4. On the **New Software Grouping** page, select a grouping method and configure the relevant parameters as described below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfcd80c6e03d4796a5464255ac082511~tplv-goo7wpa0wc-image.image) </span>

5. After completing the configuration, click **Confirm** to save.

   * You can find the newly created group in the left list at any time. Click  **...**  on the right to select **Edit Group** or **Delete Group**.

   * To manage a custom group, locate it in the left list, click  **…**  next to its name, and select **Edit group**, **Delete group**, or [Copying a group](https://docs.byteplus.com/docs/sealsuite/docs-viewing-software-statistics#7abd5725).

   * If the software group has software license management enabled, make sure you follow the corresponding license unbinding logic before editing or deleting the group.


<span id="618ef2f1"></span>
## Adding a group

<span id="fabebcbb"></span>
### Method 1: Automatic grouping

Use regular expressions or string matching rules to let the system automatically classify matching software into this group. This method is ideal for scenarios where software versions iterate quickly and naming conventions are consistent.


* **Group name**: Enter a custom group name.

* **Configure rules**: Select the target operating system (multiple selections allowed) and configure the matching rules for each system:

   * **Windows** / **Linux**: Match by **Full name of software** or **Software publisher**.

   * **macOS**: Match by **Bundle ID**.

* **Operator reference**: Supports **Include / Do not include**, **Match / Mismatch** (supports regular expressions), and **Belong to / Do not belong to** logic.

   
   |**Operator** |**Description** |**Example** |
   |---|---|---|
   |**Include / Do not include** |The actual string does / does not contain the string you define. |If you define "Contains Microsoft", the actual strings "Microsoft Corporation" and "com.Microsoft.Word" will both match "Contains". |
   |**Match / Mismatch** |The actual string does / does not conform to the string or regular expression you define. |If you define "Matches com.microsoft.\*", the actual string "com.microsoft.Powerpoint" will match "Matches". |
   |**Belong to / Do not belong to** |The actual string is / is not part of the set you define. |If you define "Belongs to com.microsoft.Powerpoint, com.microsoft.powerpoint", the actual string "com.microsoft.powerpoint" will match "Belongs to". |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you add multiple rules for the same operating system, the rules are combined with an <strong>OR</strong> operator. That is, software matching any one of the rules will be classified into this group.   </div>
   

<span id="15934984"></span>
### Method 2: Manual grouping

Directly select target software from the list of all software collected in your enterprise. This method is ideal for small\-scale, specific software classification.


* **Group name**: Enter a custom group name.

* **Operation**: In the shuttle box below, use the search bar on the left to find software by name. After you select the target software, the system automatically moves it to the "Selected" list on the right.


<span id="ac1befba"></span>
### Method 3: Built\-in group

Directly apply a classification label defined in the SealSuite cloud signature library to instantly group all software in your enterprise that matches that label.


* **Group name**: Select a built\-in category from the drop\-down list. Once selected, the group name cannot be modified.

* **Preview confirmation**: After you select a category, the list below automatically displays all software in your enterprise that **has been collected and matches the category criteria**, allowing you to confirm the results.


<span id="7abd5725"></span>
## Copying a group

Use the **Copy group** feature to create a new control group based on an existing one (either built\-in or custom) while allowing for minor software adjustments.


1. Locate the target group in the left list.

2. Click  **…**  next to the group name and select **Copy Group**.

3. In the dialog box, the system automatically populates the original group's software content. You can modify the group name and add or remove software to meet your specific control requirements.

4. Click **Confirm** to save the new group.
