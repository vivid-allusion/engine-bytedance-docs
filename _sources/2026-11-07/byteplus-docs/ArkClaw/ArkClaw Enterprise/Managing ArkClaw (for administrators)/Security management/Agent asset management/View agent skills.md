---
title: "View agent skills"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_risky_skills"
---

During the daily operation of AI assistants, skills (Skill/Plugin) may introduce security risks due to malicious code, unauthorized calls, or logical vulnerabilities.

Through the "Skills" asset dashboard on this interface, you can centrally view all skill assets associated with AI assistants under the current tenant, quickly understand the security detection status of each skill (such as whether it contains high\-risk issues), and trace the affected AI assistant instances.

<span id="tCCKR7tI"></span>
## Prerequisites

You have connected the assistant to the ClawSentry service. For connection methods, see [Enable security protection](https://docs.byteplus.com/en/docs/ArkClaw/Enable_security_protection?lang=en).

<span id="K1jESOLc"></span>
## Procedure


1. Log in to the [ArkClaw Enterprise Edition console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation bar, select **Security management**.

3. In the **Skills** list, view all skills associated with the connected AI assistants.

   * Query and filter:

      * Search by name: Enter the skill name in the search box at the top to quickly locate the target skill.

      * Filter by status: Click the "Status" dropdown to filter the list of skills currently in a specific security state (such as High Risk / Safe).

      * Click the ↻ button on the right to refresh the list at any time and obtain the latest scan results.

   * View high\-risk details: If a skill's status is displayed as red "High Risk", you can click the Details button next to the status to enter the risk details page and view specific risk information.

   * Trace impact scope: Click the blue hyperlink below the skill description (such as "Associated assistant: 1") to drill down and view the list of AI assistants currently using this skill, for targeted policy blocking or deactivation.


<span id="QimWmj44"></span>
## Field descriptions

The following are the field descriptions for the skills list:


|Field name |Field description |
|---|---|
|Skill information |Includes the skill name, function description, applicable scenarios, and other core metadata to help you quickly understand the skill's business purpose. |
|Associated assistant |Displays the number of AI assistants that have this skill mounted and are currently configured. Click the number to view a detailed list of associated assistants. |
|Status |The security rating of the skill after ClawSentry performs static scanning or dynamic detection. |
|Scan time |The timestamp of the most recent security scan performed by the system on this skill’s code or configuration. |
