---
title: "Creating alert policies"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_alert_policies"
---

NDB for MySQL has been connected to cloud monitoring. In addition to daily monitoring and checking of various monitoring indicators, you can also set alarm policies based on monitoring items to monitor changes in key indicators in real time, promptly perceive instance operation risks, and quickly troubleshoot and solve problems.

<span id="前提条件"></span>
## Prerequisites

Before setting an alarm strategy, please first reasonably evaluate the business expectations of various indicators based on the actual business situation in order to set appropriate alarm thresholds.

<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. Click the **Monitoring** tab at the top of the page.

5. At the top right of the page click **Create an alert policy**.

6. Set the alarm rule and click **OK**.

   The key steps to create an alarm rule are as follows, see [Create an alert policy](https://www.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy) for details.

   1. Set the alarm name and description.

   2. Set up the alarm object.

   3. Set up alarm rules.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">It is recommended to set up cloud monitoring to trigger an alarm when the original value of the primary monitoring item exceeds the business expectation.      </div>
      

   4. Set the notification method for alarms.
