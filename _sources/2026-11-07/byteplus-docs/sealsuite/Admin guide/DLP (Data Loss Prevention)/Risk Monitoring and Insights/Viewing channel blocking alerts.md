---
title: "Viewing channel blocking alerts"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/Viewing_channel_block_alerts"
---

When a file\-sharing action is blocked by an application blocking policy, you can investigate the incident by viewing the alert logs. This guide provides instructions on how to locate, filter, and export channel blocking logs to effectively audit security events and understand policy enforcement.

<span id="7a876119"></span>
# Prerequisite

To view channel blocking alerts, you must first configure and activate the application blocking policy. For instructions on how to configure the application blocking policy, please refer to [Configuring block policy for application](https://docs.byteplus.com/docs/sealsuite/Configuring_block_policy_for_application).

<span id="9d5d58a7"></span>
# Procedure

When a user shares a file from their device and the action is blocked by a SealSuite application blocking policy, the SealSuite client sends an alert to the Admin Console. You can view these alerts in the alerts list.


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Investigation Audit** \> **Audit Log** \> **Channel Blocking Log**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48adc51a755143a083b5b2296a9c5564~tplv-goo7wpa0wc-image.image) </span>

3. On the **Log** page, you can perform the following actions.

   * Find specific audit alerts by using filters. To use multiple filter criteria, you can click **Custom Filter** to select other filters such as **Department**, **OS**, **Role**, and more.

   * View the alert list. By default, fields such as **Blocked Time**, **Employee**, **Channel**, and **Policy Name** are displayed in the list.

      * To view detailed information about users, hover over the **Employee** name.

      * In the **Policy Name** column, click the link to view the corresponding application blocking policy, if any.

      * In the upper right corner of the list, select the columns to display in the list by clicking **Columns**.

      * In the upper right corner of the list, click **Export List** to export the alerts from the current list.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3"><strong>Administrator operation audit note</strong>: To meet compliance audit requirements, the system automatically records the administrator’s action of exporting channel blocking logs in the <strong>Admin Log</strong>.         </div>
