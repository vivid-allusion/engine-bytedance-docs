---
title: "Configuring alerts through preset templates"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_alerts_through_preset_templates"
---

VKE provides comprehensive cluster monitoring and alert capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). The capabilities cover typical scenarios such as the control plane, nodes, networks, workloads, and AI training tasks. This topic describes how to configure alerts by using preset templates from VMP.

<span id="ha1dXCky"></span>
## **Prerequisites**


* The cloud\-native observability feature has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* An alert notification object or policy has been created. For details, see [Creating contacts](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-receivers), [Creating contact groups](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-receiver-groups), and [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Alert rules are defined by PromQL statements. We recommend that you first understand basic PromQL concepts and the meaning of the metrics exposed by monitoring targets. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/PromQL-quick-start">Getting started with PromQL</a>.</div>


<span id="RevIm0Cg"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, click **Alarm Center \> Alarm Rule Template**.

4. Click the **Preset template** tab, and select **Kubernetes Engine** from the **Template type** drop\-down list.

5. In the **preset templates** list, find the target template and click **Apply template** in the **Actions** column to use the template to create alert rules.

6. Click **Next** to configure the details of the alert rule group.

   * Specify the basic information about the alert rule group.

   * Select the workspace bound to the cluster, alert notification policy, and variables.

   * Check whether each rule and its corresponding threshold meet your requirements. You can disable specified rules or modify the alert thresholds of specified rules.

7. Click **Confirm**. The system automatically generates the corresponding alert rule group.


<span id="TG1XdLiq"></span>
## Validate results

<span id="hH8QhuDO"></span>
### View settings

After the alert rule is created, you can view the rule status in the alert rule list of the VMP console.

When an alert is generated, you can view the trigger records on the **Alert event** page and troubleshoot issues by referencing the add\-on status, Pod events, and logs in the VKE console.

<span id="M0CdU93f"></span>
### Receive alerts

After you have completed alert\-related configuration, when an alert that matches the defined rules is triggered, a notification will be sent through the specified alert channel. You will receive the alert notification details through the channel. 

<span id="nzTaMuTW"></span>
## Related documentation


* [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates)

* [Receiving alert notifications by email](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-email)

* [Receiving alert notifications by Feishu custom bot](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-Lark)

* [Receiving alert notifications by Feishu application bot](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Lark_application_robot)

* [Receiving alert notifications by DingTalk](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-DingTalk)

* [Receiving alert notifications by WeCom](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Wecom)

* [Receiving alert notifications by phone](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-mobile-phone)

* [Receiving alert notifications by text message](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-SMS)
