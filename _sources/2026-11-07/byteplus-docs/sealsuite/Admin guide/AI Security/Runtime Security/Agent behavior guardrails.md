---
title: "Agent behavior guardrails"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-agent-behavior-guardrails-policy"
---

Agent Behavior Guardrail manage file access, network access, command execution, and registry access by Agents on endpoints. They help administrators protect local credentials, sensitive configurations, and system resources.

## Feature introduction

When employees use Agent tools such as Claude Code, Codex, and WorkBuddy to complete tasks, the Agent may need to read local files, access the network, or execute commands. Even if the tool itself is approved, some operations may exceed enterprise\-permitted boundaries. For example, the Agent may read SSH credentials or download and execute scripts from unknown sources.

Agent Behavior Guardrail use the SealSuite client to inspect these actions on the operating system side. They then audit or block actions based on the paths, addresses, and command rules configured by the administrator. administrators can first log rule\-matched actions to understand usage. They can also block related operations directly and send endpoint notifications to employees. Logs record the object the Agent attempted to access, the action performed, the matched policy, and the related users and devices, which helps with operation review.

Only one Agent Behavior Guardrail policy takes effect on each endpoint. Policies are not stacked or merged. If an endpoint matches multiple policies at the same time, the policy with the highest priority value is enforced. If the values are the same, the policy most recently added or modified is enforced.

## Prerequisites

The enterprise has enabled **AI Security license**. For detailed billing information, see [Billable items](https://docs.byteplus.com/en/docs/sealsuite/pricing). For the control abilities supported by different Agents, see [AI tool control ability list](https://docs.byteplus.com/en/docs/sealsuite/ai-tool-control-capabilities-list).

## Add an Agent Behavior Guardrail policy

A guardrail policy specifies the Agents to control, the objects that must not be accessed or executed, and how matched rules are handled. Create a policy based on the resources to protect and the applicable users.

1. Log in to the SealSuite Admin Console.

2. Go to **AI Security \> Runtime Security \> Agent Behavior Guardrail**.

3. Switch to the **Policy Management** tab, and click **Create Policy**.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-26.png)

4. On the **New Strategy** page, complete the following configurations, and click **OK**.

   * **Basic information**

      |Configuration item |Description |
      |---|---|
      |Policy name |Enter a custom name to identify the current policy. |
      |Policy description |Additional information about the policy purpose. This field is not used for logical judgment. You can enter up to 100 characters. |
      |Priority |The value ranges from 0 to 100. A larger value indicates a higher priority. If an endpoint matches multiple policies at the same time, only the policy with the highest priority is enforced. If the values are the same, the policy most recently added or modified is enforced. |

   * **Control action**

      |Configuration item |Description |
      |---|---|
      |Audit |Allows the Agent to perform the action that matches this policy and generates an audit log. Employees can continue the operation, and administrators can review the related action in logs. |
      |Block |Blocks the Agent action that matches this policy and generates an audit log. |

   * **Control object**

      |Configuration item |Description |
      |---|---|
      |Applicable Agent |Select AI tools based on control requirements. For the tools currently supported for control and the abilities supported by each tool, see [AI tool control ability list](https://docs.byteplus.com/en/docs/sealsuite/ai-tool-control-capabilities-list). |

   * **Protection abilities**

      Enable the required protection abilities based on control requirements. Multiple selections are supported.

      > **说明**

      > macOS endpoints require Full Disk Access permission in **System Settings \> Privacy & Security**. File access control, network access control, and command execution control all require this permission. Network access control also requires Network Extension permission. Related control policies cannot take effect until the required permissions are granted.

      |Configuration item |Description |
      |---|---|
      |File access control |Controls Agent access to system files or directories. Select the operating system to control, and enter the file path to protect. If the control action is **Block**, files that match the path cannot be read, modified, or transferred outbound.<br><br>Wildcards and variables are supported. Hover over the question mark icon next to the file path to view the input rules. To control an entire directory, end the Windows path with `\*` and the macOS path with `/*`.<br><br>For example, protect the user's SSH configuration and credential directory:<br><br><br>* Windows: `%USERPROFILE%\.ssh\*`.<br><br>* macOS: `~/.ssh/*`. |
      |Network access control |Controls Agent access to specified IP addresses or domain names. Select the address type, and enter the IP address or domain name to control. If the control action is **Block**, matched network requests are blocked. The following input formats are supported.<br><br><br>* Single IP address: `192.168.1.10`.<br><br>* IP range: `192.168.1.10-192.168.1.50`.<br><br>* CIDR block: `192.168.1.0/24`.<br><br>* Exact domain name: `example.com`.<br><br>* Wildcard domain name: `*.example.com`. |
      |Command execution control |Controls Agent execution of specified commands, such as downloading scripts, changing permissions, or modifying the system. Select the operating system to control, and enter the system command to control. If the control action is **Block**, matched commands cannot be executed.<br><br>Wildcards and variables are supported. Hover over the question mark icon next to the system command to view details. For example:<br><br><br>* Windows: `powershell *.ps1`.<br><br>* macOS: `curl * \| bash`. |
      |Registry access control |Only Windows is supported. Controls Agent access to specified registry paths. If the control action is **Block**, only read operations are allowed, and write operations are denied. For built\-in Agents, read and write operations on the tool's own registry are allowed by default and are not affected by this policy.<br><br>The system provides high\-risk registry paths by default. Use them directly or adjust them as needed. Click **Restore default** to restore the preset paths.<br><br>For example: `HKCU\Software\Microsoft\Windows\CurrentVersion\Run*`. |

   * **Notification**

      |Configuration item |Description |
      |---|---|
      |Endpoint notification |This item can be configured only when the control action is **Block**. After it is enabled, the endpoint sends an Agent behavior risk alert to the employee. Click **Configure** on the right to go to the **Notification pop\-up template** page, and create or reuse an Agent behavior control notification template. For details, see [Configure notification pop-up templates](https://docs.byteplus.com/en/docs/sealsuite/docs-configure-the-data-distributed-auditing-rule#72d521ed). |

   * **Effective objects**

      |Configuration item |Description |
      |---|---|
      |Effective objects |Specifies the users or devices to which the policy applies. Select **All objects**, or select **Partial objects** to specify the scope by employee or device. |
      |Excluded objects |Excludes specific employees or devices from the selected effective objects, so that the policy does not apply to them. |

## Manage policies

Go to **AI Security \> Runtime Security \> Agent Behavior Guardrail \> Policy Management** to check policy deployment status, filter policies, and adjust control rules.

The top of the page displays the number of effective devices and the configuration synchronization progress. **Server configuration version** is the global version identifier of the current policy library. After any policy is added, edited, or deleted, this version is automatically updated. If an endpoint successfully pulls the latest server version, the policy configuration matched by the endpoint has been synchronized to the latest state. administrators can use this information to determine whether the configuration has been deployed.

Filter policies by effective status, employee or department, device name, policy ID, or Agent name. Sort policies by edit time, priority, or creation time. Use **All**, **Audit**, and **Block** to quickly filter policies with the same control action. The following operations are available in the list.

|Operation |Description |
|---|---|
|Adjust priority |Click the priority value of a policy to adjust the policy matching order. A larger value indicates a higher priority. |
|Enable or disable |Use the **Status** switch to enable or disable a policy. After the policy is disabled, affected endpoints match the next applicable policy by priority. |
|Copy |Create a new policy based on an existing policy. |
|Edit |Modify policy parameters, control actions, or effective objects. |
|Delete |Remove a policy that is no longer needed. A deleted policy cannot be restored. Before you delete a policy, confirm the impact on effective endpoints. |

## View audit logs

After an Agent action matches a guardrail policy, SealSuite records the occurrence time, the object on which the operation was attempted, and the handling result. administrators can use this information to check which operations were audited or blocked, and which employees and endpoints were involved.

1. Go to **AI Security \> Runtime Security \> Agent Behavior Guardrail**, and select the **Audit Log** tab.

2. Filter records by control action (**All**, **Audit**, or **Block**), time, policy name, employee or device, operating system, behavior type, and Agent name.

3. View the behavior information in the list.

   Click **Columns** in the upper\-right corner to configure the displayed fields.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/ai-security-en-20261104/image-27.png)

|Field |Description |
|---|---|
|Occurrence time |The time when the Agent action triggered the policy. |
|Control action |The result of auditing or blocking this action. |
|Behavior type |The triggered control type: file access, network access, command execution, or registry access. |
|Target object |The file path, website URL, IP address, domain name, registry path, or command that the Agent attempted to access or execute. Click the copy icon to copy the specific content. |
|Matched policy |The guardrail policy that handled this action. Click the policy name to view the rules. |
|Agent name |The Agent tool that triggered the control. |
|User information |The employee who used the Agent. Hover over this column to view employee details. |
|Device information |The endpoint on which this action occurred. Hover over this column to view device details. |
|Operating system |The operating system of the endpoint on which this action occurred. |

## Forward logs

To include guardrail logs in enterprise\-wide analysis or retain them for a longer period, forward Agent Behavior Guardrail logs in real time to a Syslog or Elasticsearch service owned by your enterprise. For configuration steps, see [Configure log forwarding](https://docs.byteplus.com/en/docs/sealsuite/configure-log-forwarding).
