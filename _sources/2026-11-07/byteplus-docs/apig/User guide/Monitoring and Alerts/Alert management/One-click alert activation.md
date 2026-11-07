---
title: "One-click alert activation"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/One-click_alert_activation"
---

API Gateway supports one\-click quick activation of default alert notifications for instances or services using the default template based on the **APIG instance/service**, greatly simplifying the alert configuration process for users. This article introduces how to activate alerts with one click.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This article describes the general procedure for one\-click alert activation. For methods on activating instance default alerts when creating a new instance, please refer to <a href="https://docs.byteplus.com/en/docs/apig/Creating_an_instance">Creating an Instance</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An alerting notify policy has been created under the VMP target workspace; for more details, please refer to [Creating an alerting notify policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules).

* An alerting aggregation policy has been created under the VMP target workspace; for more details, please refer to [Creating an alerting aggregation policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Follow the steps below to access the **Monitoring Info** tab of the target instance or service.

   * Enter the **Monitoring Info** tab of the target instance.

      1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

      2. In the top navigation bar, select the target region.

      3. In the left **navigation bar**, click on the target instance name and enter the Overview page.

      4. Click **Monitoring** to switch to the **Monitoring** tab.

   * Enter the **Monitoring** tab of the target service.

      1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig).

      2. In the top navigation bar, select the target region.

      3. In the left navigation bar select **Route Management \> Service List**. In the service list, click on the target service name to enter the service Overview page.

      4. Click **Monitoring** to switch to the **Monitoring** tab.

2. In the Monitoring tab, click **Enble Default Alert Notification**.

3. In the pop\-up dialog, configure the parameters as required.

   
   |Parameter |Description |
   |---|---|
   |Prometheus workspace |Displays the APIG instance bound to the VMP workspace. |
   |alerting template |Displays the currently used alerting template. |
   |alerting aggregation policy |Configure the alerting aggregation policy, including the aggregation cycle and notification cycle. Designed to prevent alert storms caused by frequent alert triggers, which generate a large number of alert messages in a short time. For more details, please refer to [Alerting aggregation policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules). |
   |alerting notify policy |Configure the alerting notify policy. Used to specify the alert contact groups that need to receive the notifications when different levels of alerts occur. If not configured, only alert events are generated and no notifications are sent. For more details, please refer to [Alerting notify policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules). |
   

4. After configuration is complete, click **Confirm**.

   After creation is successful, the page will display the **alerting rule group** you created, the **alerting aggregation policy** used, and the **alerting notify policy**, supporting one\-click jump to view details.


<span id=".566h55CG5ZGK6K2m6KeE5YiZ"></span>
## Manage Alerting Rules

In the Monitoring tab of the APIG instance or Service, click **Enter VMP Manage Alert Notifications**, redirecting to the **alerting rule** page of the VMP Service Console. You can edit/delete alerting rule groups, or enable/disable/modify alert rules within the alerting rule group according to your business needs. For more details about actions, refer to [Managing alerting rule groups](https://docs.byteplus.com/en/docs/vmp/Managing-alerting-rule-groups).
