---
title: "Best practices for administrators assigning templates"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Best_practices_for_administrators_assigning_templates"
---

This topic describes how administrators can effectively manage user quotas from an enterprise cost\-control perspective.

<span id="po5PBHpr"></span>
## Prerequisites

ArkClaw has been activated, seats have been purchased, and other preliminary actions have been completed. For details, see [Activating ArkClaw](https://docs.byteplus.com/en/docs/ArkClaw/Activate_ArkClaw_Enterprise_edition_service).

<span id="datIQGCk"></span>
## Background

Enterprise A has activated BytePlus ArkClaw and has currently purchased 1,000 Starter seats, 500 Standard seats, 300 Premium seats, and 200 Ultimate seats. With 500 employees across R&D, Product Management, Administration, and HR requiring ArkClaw for daily work tasks, the administrator needs to optimize seat allocation to balance role\-specific needs with cost efficiency.

To enable rapid decision\-making aligned with business objectives, the administrator can leverage the following quota control scenarios‌:


<columns>
<columnsItem zoneid="LKHZXlCj">

&nbsp;


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

**Scenario 1: Unified safety\\-net quota control**


* The space\\-level quota settings serve as the default safety\\-net policy that governs the quota scope for all enterprise employees using ArkClaw. It uniformly tightens available resources and quotas at the space level.

* When the administrator wants to first restrict capability boundaries from a high\\-level view (space) before implementing granular internal controls, they can adopt this unified restriction policy for all employees in the enterprise. Space configurations determine the default resource scope, module toggles, and accessibility of high\\-risk capabilities within a space, acting as the outermost ‌safety net of the entire quota management framework.




</card>



</columnsItem>
<columnsItem zoneid="3dtuecmd">

&nbsp;


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

**Scenario 2: Granular seat allocation**


* This method manages eligible seat editions and quantities for designated employees to use ArkClaw. Seats can be flexibly allocated to employees based on actual business needs and job types to optimize resource utilization and reduce enterprise costs

* When the core requirement is controlling maximum allowable seat editions and quantities for employees, without initially differentiating ArkClaw configurations, the focus shifts to the ‌employee\\-to\\-seat ratio‌ rather than "employee\\-content" variations. In this scenario, we recommend configuring seat quotas to establish capacity boundaries.




</card>



</columnsItem>
<columnsItem zoneid="TAvQJfL6">

&nbsp;


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

**Scenario 3: Refined seat allocation and content settings**


* On top of seat restrictions, this scenario requires further governing ArkClaw configurations (such as personas and skills) to implement granular control over accessible content within predefined seat specifications and quantities.

* After using seat editions and quantities to define who can access ArkClaw, the administrator may impose ‌content\\-level quotas‌ for refined configuration limits. While seat restrictions remain active, the actual resources visible or operable to employees are determined by the combination of user attributes, user groups, and template\\-level quotas.

</card>



</columnsItem>
</columns>


<span id="UZM2ExIR"></span>
## Procedure

<span id="NtlrKAeR"></span>
### Step 1: Configure space settings


1. Log in to the [ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation bar​, click "Space Overview".

3. On the "Space Overview", set the available models and the number of seats that employees can request per edition.

4. Based on the number of seats purchased and the number of employees, set the number of seats that each employee can request per edition.

   * Starter edition: Each employee can request up to 2 seats.

   * Standard edition: Each employee can request up to 2 seats.

   * Premium edition: Each employee can request up to 1 seat.

   * Ultimate edition: Each employee can request up to 1 seat.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you need only broad quota restrictions for all ArkClaw users, you can skip subsequent steps. If you need more granular quota restrictions, proceed with the following steps.   </div>
   

<span id="FLQiwLDm"></span>
### Step 2: Import user information

As an administrator, you upload a CSV file to import users in batches into the ArkClaw system. Later, you can configure seats and templates for these users.


1. In the left navigation pane, click "Organizations" \> "Users".

2. Click "Import employee info".

3. Click "Download employee info template" to download a standardized CSV template.

4. Fill in the CSV file with information of 500 employ​ees according to the template requirements and then save the file.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Each import supports up to 500 rows of data.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To avoid file import failure, strictly follow the instructions in the first cell of the template when entering employee information.   </div>
   

5. Upload the file to the import window in the console and click "Confirm". The system will automatically create accounts in the user pool.


<span id="NcFzCtbO"></span>
### Step 3: Configure user seats

Configure seat quotas for designated users. For example, certain R&D members and product managers may require additional Premium or Ultimate seats. When the space\-level default maximum seats per employee proves insufficient, you can adjust seat quotas individually for these employees.


1. In the left navigation pane, click "Resource Configuration" \> "Seats".

2. Configure the number of seats per edition that specified users can request. For example, administrative and HR personnel are not allowed to apply for Ultimate seats, and the R&D team and product managers can apply for seats in advanced editions.

3. In the "Employee quota" section, select the "List" or "Groups" tab in the upper\-right corner of the list, select the target employees, and then click "Batch edit quota" at the bottom of the list.

4. Set the target quota and click "Confirm".

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If precise control over the counts of requestable seats for specific employees suffices, you can skip subsequent steps. To restrict ArkClaw content configuration for certain employees, assign properly configured templates to the employees.   </div>
   

<span id="yHr16UNC"></span>
### Step 4: Configure and assign templates

In addition to restricting seat editions for specified employees, you may also want to configure souls, built\-in skills, built\-in plugins, and other settings for those seat editions for certain employees. In this case, you can create individual templates and assign the templates to the target employees


1. In the left\-side navigation pane, click "Claw Template Center".

2. On the "Custom templates" tab, click "Create template" to configure a template for the target employees. For example, configure the "Administrative assistants on duty" template for the administration team, and the "HR" template for the HR team.

3. Click "Confirm" to complete template creation.

4. Click "..." \> "Manage assignees" in the upper\-right corner of the target template card.

5. On the left side of the "Manage assignees" page, select the checkbox in front of the employee to whom the template will be assigned. Click "Confirm" to assign the template to the specified employee.
