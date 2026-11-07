---
title: "Agent full link audit"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/agent-full-link-audit"
---

Agent Full Link Audit records employee interactions with Agents by task. It helps administrators view user inputs, model outputs, tool calls, and execution results within a task.

## Feature overview

When an employee asks an Agent to modify code, process files, or complete other tasks, a single task may include multiple conversation rounds and tool calls. When investigating abnormal operations, administrators usually need to understand the initial request, what the Agent did afterward, and which step produced the abnormal result.

After Agent Full Link Audit is enabled, the SealSuite client collects task interaction records from specified Agent tools every 30 minutes and reports them to the Admin Console. administrators can find tasks for the relevant employee in the task list, then view inputs, outputs, and tool execution results in session order. For example, when reviewing a file modification, administrators can check the employee's instructions and the results returned by tools called by the Agent to understand how the modification occurred. Audit data can also be forwarded to the enterprise log service for later analysis and forensics.

> **tip**

> The system collects and reports only Agent task interactions that occur while the feature is enabled. Historical tasks before the feature is enabled and task activity after it is disabled are not recorded.

## Prerequisites

Before enabling audit, make sure the following conditions are met.

* The enterprise has activated an **AI Security license**. For billing details, see [Billing items](https://docs.byteplus.com/en/docs/sealsuite/pricing).

* Employee endpoints have installed **SealSuite client 3.3.20 or later**.

* The required Agent supports full link audit. For the supported scope, see [AI Tool Control Capabilities List](https://docs.byteplus.com/en/docs/sealsuite/ai-tool-control-capabilities-list).

## Enable full link audit

Audit configurations specify the Agent tools to record and the users or devices to which the audit applies. After configuration, SealSuite reports task records to the Admin Console based on the collection cycle.

1. Log in to the SealSuite Admin Console.

2. Go to **AI Security \> Runtime Security \> Agent Full Link Audit**.

3. Click the behavior audit feature status in the upper\-right corner of the page to open the **Agent End\-to\-End Audit** configuration panel.

   If the feature is not enabled, **Behavior audit is not enabled.**  is displayed.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-28.png)

4. Enable **Agent End\-to\-End Auditing Feature**, complete the following configuration, and click **Confirm**.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-29.png)

   * **Agent tool**

      |Configuration item |Description |
      |---|---|
      |Agent tool |Select the tools to audit. For the supported AI tools, see [AI Tool Control Capabilities List](https://docs.byteplus.com/en/docs/sealsuite/ai-tool-control-capabilities-list). |

   * **Effective scope**

      |Configuration item |Description |
      |---|---|
      |Effective object |Select **All objects**, or use **Partial objects** to define the audit scope by employee or device. |
      |Excluded object |Exclude specific employees or devices from the selected scope so their tasks are not affected by this audit configuration. |

## View audit tasks

The audit list displays records by task. To review an employee's Agent operation, first filter tasks by time, employee, and tool. Then open the details to view the interaction process.

1. Go to **AI Security \> Runtime Security \> Agent Full Link Audit**.

2. Filter target tasks by **Task start time**, **Task update time**, **Employee**, **Department**, or **Agent name**. Click **Expand** to further filter by **Task name** or **Operating system**.

3. View the task list. To adjust displayed fields, click **Columns**.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-30.png)

|Field |Description |
|---|---|
|Task start time |The time when the task started. Use it to find tasks initiated during a specified time range. |
|Task update time |The time when the task was last updated. Use it to find tasks that still had interactions during a specified time range. |
|User information |The employee who initiated the task. |
|Task name |The name of this Agent task. |
|Agent name |The Agent tool that executed the task. |
|Working directory |The directory used by the Agent when executing the task. Use it to verify the location involved in the task. This field can be displayed through custom columns. |
|Device information |Information about the endpoint that executed the task. Use it to identify which device the task came from. This field can be displayed through custom columns. |
|Operating system |The operating system of the endpoint that executed the task. This field can be displayed through custom columns. |
|Action |Click **Details** to view basic task information and interaction content. |

## View task details

Task details consolidate conversations and tool execution records from the same task. administrators can first verify the task and employee, then view specific interactions to understand how the Agent executed the employee's request.

1. Find the target task in the task list and click **Details** in the **Action** column.

2. Verify the basic task information at the top of the details page.

   |Field |Description |
   |---|---|
   |Task name |The Agent task currently being viewed. |
   |Task ID |The unique identifier of the task. Use it to distinguish or locate the task. |
   |Associated user |The employee who initiated the task. |
   |Agent name |The Agent tool that executed the task. |
   |Working directory |The directory used by the Agent when executing the task. Use it to verify the location involved in the operation. |

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-31.png)

3. To view specific interactions, click **View Sensitive Content**, then click **Confirm View** in the confirmation dialog box.

   If the enterprise has enabled secondary authentication for administrator sensitive operations, complete identity verification as prompted.

   > **tip**

   > Actions where administrators view sensitive content are recorded in **Admin Log**.

4. View the task's conversations and tool execution records.

   Use the session navigation on the left to locate a specific interaction round, then view its details.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-32.png)

|Information |Description |
|---|---|
|Multi\-turn conversation records |Multi\-turn interaction context within the same task. Use it to understand how instructions changed over time and how interaction rounds relate to each other. |
|User input |Prompts or instructions entered by the employee in the task. |
|Model output |Content returned by the Agent. |
|Tool call |The specific tool called by the Agent during execution. |
|Execution result |The result returned by the tool call. Use it with the input and call process to verify whether the task ran as expected. |

## Log forwarding

To analyze Agent tasks centrally in the enterprise log platform or retain data for later forensics, forward Agent Full Link Audit Log in real time to enterprise\-owned Syslog or Elasticsearch services. For configuration steps, see [Configure log forwarding](https://docs.byteplus.com/en/docs/sealsuite/configure-log-forwarding).
