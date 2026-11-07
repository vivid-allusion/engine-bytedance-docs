---
title: "Configuring an alert policy"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Configuring-an-alarm-strategy"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

​​By configuring alert policies for your PrivateLink, you can promptly detect anomalies in its monitoring metrics, ensuring the stable operation of your business.​​ You can create custom alert policies for your Endpoint Services and Endpoints, or use the pre\-configured alert templates provided by PrivateLink.

We recommend using the pre\-configured templates. This not only improves configuration efficiency but also allows you to copy a template and adjust it flexibly according to your needs.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

IAM users may be unable to directly configure alert policies. To configure, see [Why can't IAM users view monitoring data](https://docs.byteplus.com/en/docs/privatelink/FAQs). Grant CloudMonitor administrative permissions to the IAM user.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the Cloud Monitor console.

2. In the left navigation pane, select **Alarm Center \> Alarm Template**.

3. Select the **Preset alert template** tab.

4. In the search box, specify the search condition **Name**, and input **PrivateLink** to find the target template.

5. You can click the name of the preset template, such as **PrivateLink \- Endpoint preset alert template**, to view detailed rule information for triggering alerts and confirm whether the template meets your alert requirements.

6. Click the switch in the **Enable** column to the right of the template, or click **Enable** on the template details page to enable the alert template.

7. In the **Configure contact groups** pop\-up window, specify the alert channel where you expect to receive notifications.

8. Click **Apply** to complete configuration.
