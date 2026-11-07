---
title: "Creating alerting rules based on templates"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_alerting_rules_based_on_templates"
---

This article introduces how to quickly create a set of alerting rules based on the builtin alert templates of the API Gateway.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

The API Gateway provides several common alerting rule templates based on general Alerts and monitoring scenarios. You can log in to the [VMP console](https://console.byteplus.com/prometheus) and select **Alert center \> Alerting rule templates** from the navigation bar on the left, enter the alerting rule templates page, and view all the templates provided by the API Gateway as well as the details of the rules included in each template.


|Template types |Template name |Template description |
|---|---|---|
|Instance template |Default APIG instance template |Default alerting template for APIG instance monitoring metrics, preset with **APIG instance \- High ratio of 5XX requests** alerting rule. |
||APIG instance complete template |Full alerting template for APIG instance monitoring metrics, preset with **APIG instance \- High ratio of 4XX requests**, **APIG instance \- Average response time exceeds threshold**, **APIG instance \- P90 response time exceeds threshold**, **APIG instance \- P99 response time exceeds threshold**, **APIG instance \- HTTP request message size exceeds threshold**, **APIG instance \- HTTP response message size exceeds threshold**, **Public network inbound bandwidth exceeds threshold**, **Public network outbound bandwidth exceeds threshold**, **Number of new connections exceeds threshold** alerting rules. |
|Service template |Default APIG Service template |Default alert template for APIG service monitoring metric, preset **Service\- high ratio of 5XX requests** alerting rule. |
||Full APIG Service template |Complete alert template for APIG service monitoring metric, preset **Service\- high ratio of 4XX requests**, **Service\- average response time exceeds threshold**, **Service\- P90 response time exceeds threshold**, **Service\- P99 response time exceeds threshold**, **Service\- HTTP request message size exceeds threshold**, **Service\- HTTP response message size exceeds threshold** alerting rules. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An alerting notify policy has been created under the target workspace in VMP, for details please refer to [Creating an alerting notification policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules).

* An alerting aggregation policy has been created under the target workspace in VMP, for details please refer to [creating an alerting aggregation policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left **navigation bar**, click on the target instance name and enter the **Overview** page.

4. Click **Monitoring** to switch to the **Monitoring** tab.

5. In the **Monitoring area**, click **enter VMP management alerting notify**, redirect to the **alerting rule** page on the VMP console.

6. Click **create \> create based on template**, and enter the create alerting rule group page. For parameter description, refer to [Creating an alerting rule group](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rule-groups).
