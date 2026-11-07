---
title: "Configure Alert Center"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-alert-center"
---

SealSuite Alert Center helps employees view security alerts related to them. This topic describes how administrators configure alert display types, users in scope, and client display rules.

## Overview

After an enterprise enables security policies related to files, desktop applications, or peripherals, some employee actions may be blocked. Employees usually cannot identify the cause of failure from the action itself. Alert Center centrally displays these blocking alerts in the SealSuite client. Employees can see which actions are controlled and provide specific details when contacting IT administrators.

Alerts are divided into three categories: file blocking, desktop application blocking, and peripheral blocking. administrators can enable them as needed and specify visible departments, roles, or members for each alert category. For example, file blocking alerts can be displayed to all employees, while peripheral blocking alerts are displayed only to the R&D department.

Alert Center only determines which alerts are displayed and who can view them. It does not affect blocking enforcement. To adjust blocking conditions, modify the corresponding security policies.

## Configuration procedure

The alert type determines which blocking alerts the client can display. The effective target determines which employees can view that type of alert. Follow these steps to select alert types and configure the display scope:

1. Log in to the Admin Console. In the left navigation pane, choose **Settings** \> **IT Tools**.

2. In the **Services & help** section, click **Alert Center**.

3. Enable the following alert types as needed.

   |Alert type |Displayed content |
   |---|---|
   |**File Sharing Blocking Alert** |Alerts generated when file operations trigger blocking by the corresponding security policy. |
   |**Desktop Application Blocking Alert** |Alerts generated when desktop application operations trigger blocking by the corresponding security policy. |
   |**Removable Device Blocking Alert** |Alerts generated when peripheral usage triggers blocking by the corresponding security policy. |

4. Configure the **Scope** for each alert category.

   Effective targets specify which employees can view this type of alert in the client. Select departments, roles, or members under each alert category. Different alert types can have different targets.

5. Click **Confirm** to save the configuration, and confirm that the **Alert Center** switch is enabled on the IT tools page.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/it-tools-en-20261023/alert-admin-live.png)

## Client behavior

The client displays the corresponding alert types based on the administrator configuration. For employees who are not included in the users in scope of an alert type, the client does not display that type of alert. For example, if an employee is only within the scope of file blocking alerts, the employee can view file blocking alerts under this configuration. Other blocking alert types that do not apply to the employee are not displayed.
