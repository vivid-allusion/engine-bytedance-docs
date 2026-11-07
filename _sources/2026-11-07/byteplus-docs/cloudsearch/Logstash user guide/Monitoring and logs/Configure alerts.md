---
title: "Configure alerts"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Configure_alerts"
---

Logstash is now integrated with Cloud Monitor. You can create alert policies or configure one\-click alerts in the Cloud Monitor console. When an abnormal resource status is detected, an alert notification is sent to improve your O&M efficiency. This document describes how to create alert policies and configure one\-click alerts in Cloud Monitor.

<span id="fLeBjNng"></span>
## Create alert policies


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the left\-side navigation pane, select **Data Processing** \> **Logstash**.

3. On the Logstash Instances page, click the name of the target instance to go to the **Basic Information** tab.

4. In the left\-side navigation pane, select **Observability** \> **Monitoring Overview** and click **Create Alert Policy**.

   You will be redirected to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/alert/strategy/create). Follow the subsequent steps to create an alert policy.

5. On the **Create Alert Policy** page, select **Database** \> **Cloud Search** for Resource Type, and then refer to [Create alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy) to configure other parameters.


<span id="0CImsKEY"></span>
## Configure one\-click alerts


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the left navigation pane, select **data processing** \> **Logstash**.

3. In the Logstash Instances list, click the name of the target instance to open the **basic information** tab.

4. In the left\-side navigation pane, select **observability** \> **monitoring overview**, and then click **one\-click alert**.

5. On the **preset alert templates** page of the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor), click the switch in the **enable** column for the **Cloud Search Logstash preset alert template**.

   Enable the preset template to quickly apply alert policies for common Logstash exceptions without configuring each one manually.

6. In the **configure contact group** dialog box, configure the parameters, and then click **Apply**. For detailed instructions, refer to [Enable preset alert templates](https://docs.byteplus.com/en/docs/cloudmonitor/Enabling-a-preconfigured-alarm-template).
