---
title: "Handle user feedback"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-user-feedback"
---

User feedback provides a centralized view of issues, diagnostic results, and logs submitted by employees from the client. Administrators can search feedback records, view details, download client logs, and record processing results.

## Overview

After employees submit client issues or provide logs for troubleshooting, Administrators can centrally search related records in **User FeedBack**. They can analyze faults based on issue descriptions, network diagnostic results, and attached logs. Use conditions such as feedback path, time, employee, and device to locate the information required for troubleshooting. Logs uploaded separately are identified by the **Upload Logs** path.

Administrators can view details, download logs, and mark records as **Resolved** or **Ignored** based on the actual handling status. During processing, contact the employee who submitted the feedback to understand the issue and confirm the result. Backend records are used to store feedback information and processing status.

## Feedback sources

User feedback from the following sources is recorded in the SealSuite Admin Console for Administrators to view.

* **Feedback**: An employee clicks **Feedback** in the client, selects an **Problem type**, enters an **Problem description**, and submits an issue that requires IT administrator assistance.

* **Network Diagnostics**: An employee goes to **Lab \> Network diagnostics**, and the page automatically starts diagnostics. If diagnostics detect an issue, the employee clicks **Feedback** to report the diagnostic results to the Admin Console.

* **Upload Logs**: When logs are required for troubleshooting, an employee goes to **About SealSuite \> Upload logs**, selects an issue type, enters an issue description, and submits the logs. The **Feedback source** in the backend record is displayed as **Upload Logs**.

## View and handle feedback

After receiving a troubleshooting request from an employee, locate the record based on the submission time and employee information. Then view details or download logs. Follow these steps:

1. Log in to the SealSuite Admin Console.

2. In the left navigation pane, choose **Enterprise Settings \> Management center \> User feedback**.

3. Set filter conditions to find the feedback records to handle.

   Search records by issue type, employee information, and feedback time. To locate logs uploaded separately, click **Expand** and select **Upload Logs** in **Feedback source**. Further narrow the search by **OS**, **Device information**, and the client version filter.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/feedback-en-20261027/feedback-filters.png)

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cda937e7a99b412ca517478f5a022268~tplv-goo7wpa0wc-topic.webp)

1. In the **Action** column of the target record, perform the following actions as needed for troubleshooting:

   * **View information**: View the specific feedback submitted by the employee and the network diagnostic results provided in the record, including whether the network connection, network proxy, VPN service, and intranet and internet access are normal.

   * **Download log**: Download the SealSuite client logs from the employee endpoint to your local device, and continue troubleshooting based on the issue description.

   * **Resolved** or **Ignored**: Update the handling result based on the actual feedback processing status.

2. Contact the employee who submitted the feedback to discuss the troubleshooting progress and confirm the issue resolution result.
