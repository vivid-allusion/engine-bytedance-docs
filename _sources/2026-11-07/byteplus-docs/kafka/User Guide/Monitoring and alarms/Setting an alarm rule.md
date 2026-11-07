---
title: "Setting an alarm rule"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/setting-alarm-rule"
---

Message Queue for Kafka is integrated with CloudMonitor. You can not only view metrics during routine monitoring but also set alarm strategies based on these metrics. This allows real\-time monitoring of changes in key metrics and helps you timely detect instance operation risks and promptly troubleshoot and resolve issues.

<span id="前提条件"></span>
## Before you begin

Before setting alarm strategies, assess the expected values of various metrics based on the actual business situation. This ensures the appropriate setting of alarm thresholds.

<span id="操作步骤"></span>
## Procedure


1. Log on to the CloudMonitor console.

2. In the left\-side navigation pane, click **Cloud Service Monitor**, find the **Middleware** pane, and select **Kafka**.

3. Click the instance name, then click **Alarm strategy** in the top menu bar.

4. Click **Create alarm strategy**.

5. Set a specific alarm rule and click **OK**.

   The following key steps are used to create an alarm rule.

   1. Specify an alarm name and a description.

   2. Specify an alarm object.

   3. Set the alarm rule.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you configure VCM to instantly trigger an alarm when the original value of a key metric exceeds its expected business value.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Message Queue for Kafka offers default trigger conditions covering core metrics and alarm triggering strategies for common scenarios. Selecting <strong>Use preset trigger conditions</strong> automatically populates the console with default strategy content.   </div>
   

   4. Configure an alarm notification method.
