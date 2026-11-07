---
title: "Configure feedback"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configure-feedback"
---

SealSuite lets employees submit usage issues and upload client logs, helping enterprise IT administrators troubleshoot issues. This article describes how to manage the feedback entry point, how employees submit feedback, and how to upload logs.

## Overview

When employees encounter client or network issues that they cannot resolve, they can submit the issue to enterprise IT administrators through feedback. IT Assistant directs employees to existing enterprise support channels. Feedback records issues directly in the SealSuite Admin Console. Administrators can also obtain the employee's client logs without asking the employee for troubleshooting details one by one.

When client logs are required to help IT administrators troubleshoot issues, employees can also use the **Upload Logs** entry point under **About SealSuite** to enter issue information and submit client logs. Log upload and standard feedback use different entry points. In the backend, **Feedback source** identifies the record source. After the feedback entry point is disabled, employees can still submit client logs through **About SealSuite \> Upload Logs**.

## Enable the feedback entry point

The feedback switch controls the feedback entry point on desktop and mobile clients. After an administrator turns off the switch, the related entry points are hidden after the client obtains the new configuration. After the switch is turned on, they appear again. This switch does not control the **Upload Logs** entry point. Employees can still upload client logs after it is turned off. To configure the switch, follow these steps:

1. Log in to the Admin Console. In the left navigation pane, choose **Settings** \> **IT Tools**.

2. In the **Services & help** area, find the **Feedback** card.

3. Use the switch on the card to show or hide the feedback entry point.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/feedback-en-20261027/feedback-switch.png)

This switch controls the feedback entry points in Toolbox, Lab, and Help on the desktop client home page. It also controls the feedback entry points in the avatar menu, About SealSuite, VPN quick switch, and Toolbox on mobile clients. Different entry points may be displayed as **Feedback**, **Feedback Suggestions**, or **Feedback**.

## Client experience and usage

### Submit feedback

|**Feedback method** |**Submission method and issue type** |**Client feedback entry point** |
|---|---|---|
|Issue feedback |Employees click **Feedback** in the client, select **Problem type**, enter **Problem description**, and submit an issue that requires assistance from an IT administrator.<br><br>Employees select the issue type based on the actual issue, such as optimization suggestions, VPN connection failure, or inability to access a specific website. The type describes the issue category, not the feedback source. |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/275e618dbd8c461396d86ed53fda43c9~tplv-goo7wpa0wc-topic.webp) |
|Network diagnostics |Employees go to **Lab \> Network Diagnostics**. The page automatically starts diagnostics. If diagnostics detect an issue, employees click **Feedback** to report the diagnostic results to the Admin Console.<br><br>Network diagnostics submits diagnostic results. The technical solution classifies diagnostic exceptions as the network diagnostics exception type. Specific exceptions are available in the detection results under details. |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe2cab15451a4a8c834edf8092c7f966~tplv-goo7wpa0wc-topic.webp) |

### Upload client logs

When IT administrators need client logs to analyze faults, employees can submit logs in the client and include issue information, helping administrators locate the corresponding record. Follow these steps:

1. Log in to the SealSuite client, go to **About SealSuite**, and click **Upload Logs**.

2. Select **Problem type** based on the actual fault, and enter **Problem description**.

   **Problem type** identifies the fault category. **Problem description** provides the time of occurrence, steps taken, and symptoms. For example, if an internal website cannot be accessed after connecting to the VPN, enter the website address, time of occurrence, and error message.

3. Submit the logs and wait for the upload result. Avoid duplicate submissions during upload. If the upload fails, follow the page prompts to check the network and try again.

4. Contact the IT administrator and provide the submission time and fault symptoms, so the administrator can find the record in **User FeedBack**.

Records created by log upload show **Upload Logs** as the **Feedback source**.

## View and handle feedback

After employees submit issues or logs, Administrators can locate records by submission time and employee information, view details, and download logs. For more information, see [Handle user feedback](https://docs.byteplus.com/docs/sealsuite/docs-user-feedback).
