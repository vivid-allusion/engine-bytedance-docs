---
title: "Set alarm rules"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Set_alarm_rules"
---

The message queue for RabbitMQ has been integrated with Cloud Monitor. In addition to routinely viewing various monitoring metrics, you can also set alarm policies based on these metrics to monitor key metrics in real time. You can promptly detect instance operation risks, and quickly troubleshoot and resolve issues.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before setting alarm policies, evaluate the expected business values of each metric according to your actual business scenarios to set appropriate alarm thresholds.

<span id=".5pON5L2c5q2l6aqk"></span>
## Operation steps


1. Log in to the [Cloud Monitor Console](https://console.byteplus.com/cloud-monitor).

2. Click **Cloud Service Monitor** in the left navigation pane, then select **RabbitMQ** in **Middleware** section.

3. Click the instance name, then click **Alarm strategy** in the top tab bar.

4. Click **Create alarm strategy**.

5. Set the specific alarm rules and click **Create**.

   The key steps to create an alarm strategy are as follows. For detailed operations, see [Creating an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

   1. Set the alarm name and description.

   2. Set the alarm target.

   3. Set the alarm rule.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">We recommend that you configure Cloud Monitor to trigger the alarm immediately when the raw values of the main monitored metrics exceed business expectations.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The message queue for RabbitMQ provides preset trigger conditions covering core metrics and alarm trigger policies for basic scenarios. After selecting <strong>use preset trigger conditions</strong>, the console automatically fills in the pre\-configured policy content.      </div>
      

   4. Set the alarm notification method.
