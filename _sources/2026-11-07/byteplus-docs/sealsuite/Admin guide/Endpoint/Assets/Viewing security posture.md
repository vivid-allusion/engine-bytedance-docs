---
title: "Viewing security posture"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-risk-events"
---

When users connect to the corporate network through SealSuite clients, SealSuite collects user's device information and displays the security status of the devices through the **Risk Events** function in the Admin Console. This article introduces how to view the collected device information and the security status of devices using the **Risk Events** function.

<span id="b8a60371"></span>
# Viewing the security status of devices


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Assets** \> **Security Posture**.

3. On the **Security Posture** page, you can perform the following actions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ee7857cd83e44c4bcf385327cb6f926~tplv-goo7wpa0wc-image.image) </span>

   * Search for specific devices by using filters.

   * View the security status of devices.

      * Click the device name to view the device details on the pane that appears.

         The description of device detailed information:

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can only view the matching rules and the risk detection items on the condition that rules for device baseline detection, data leakage protection or antivirus detection have been enabled and configured, and a risk event that satisfies any of the above rules has been detected.         </div>
         

         * The **Risk Events** tab: Displays the results of risk event detection for device baselines, application\-related risks, process\-related risks, and computer viruses.

         * The **Events** tab: Displays details of detected risk events, which are divided into the events associated with device baselines, application\-related risks, process\-related risks, virus\-related risk and data leakage. You can view specific risk events under the corresponding tabs of this option.

         * The **Logs** tab: Displays details of risk remediation for events that satisfy existing rule groups.

      * **Effective Rule**: Rule information of the current endpoint device risk item detected, including DLP rule, device baseline detection rule, and endpoint anti\-virus rule.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can only view the matching rules and the risk detection items on the condition that rules for device baseline detection, data leakage protection or antivirus detection have been enabled and configured, and a risk event that satisfies any of the above rules has been detected.         </div>
         

      * **Action**: In the event that the use of specific functions is restricted on a managed device resulting from risk remediation, you need to make sure all risk events that occur on the device have been remediated and click **Restore** in the **Action** column to restore the use of these functions.
