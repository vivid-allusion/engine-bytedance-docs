---
title: "Configuring alerts based on custom templates"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates"
---

VKE provides comprehensive cluster monitoring and alert capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). The capabilities cover typical scenarios such as the control plane, nodes, networks, workloads, and AI training tasks. This topic describes how to configure alerts by using custom templates in VMP.

<span id="GhGynDfS"></span>
## **Prerequisites**


* The cloud\-native observability feature has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* An alert notification object or policy has been created. For details, see [Creating contacts](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-receivers), [Creating contact groups](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-receiver-groups), and [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Alert rules are defined by PromQL statements. We recommend that you first understand basic PromQL concepts and the meaning of the metrics exposed by monitoring targets. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/PromQL-quick-start">Getting started with PromQL</a>.</div>


<span id="0fdvyWI7"></span>
## Procedure

<span id="cQyNlOnX"></span>
### Step 1: Export a preset template


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, click **Alarm Center \> Alarm Rule Template**.

4. Click the **Preset template** tab, and select **Kubernetes Engine** from the **Template type** drop\-down list.

5. Select the target template and click **Export** to export the YAML file of the preset template to your local machine.


<span id="kUC5fkpX"></span>
### Step 2: Configure a custom template


1. Modify the content of the template YAML file based on your actual requirements.

   * Adjust the rule name, PromQL query, threshold, duration, and variable definitions in `items`.

   * Add or remove rule items to meet your own business requirements.

2. Click the **Custom template** tab and click **YAML file import** to import the modified template file.

3. Click **Next** to configure the basic information about the template.

4. Click **Confirm**.


<span id="BTuddTjn"></span>
### Step 3: Configure alerts using the custom template


1. In the list on the **Custom template** tab, find the custom template you imported, click **Apply template** in the **Actions** column, and use the custom template to configure alerts.

2. Configure alert rule group details.

   * Specify the basic information about the alert rule group.

   * Select the workspace bound to the cluster, alert notification policy, and variables.

   * Check whether each rule and its corresponding threshold meet your requirements. You can disable specified rules or modify the alert thresholds of specified rules.

3. Click **Confirm**. The system automatically generates the corresponding alert rule group.


<span id="Y6WU5Jpi"></span>
## Validate results

<span id="aA7gszA0"></span>
### View settings

After the alert rule is created, you can view the rule status in the alert rule list of the VMP console.

When an alert is generated, you can view the trigger records on the **Alert event** page and troubleshoot issues by referencing the add\-on status, Pod events, and logs in the VKE console.

<span id="RiRvByDm"></span>
### Receive alerts

After you have completed alert\-related configuration, when an alert that matches the defined rules is triggered, a notification will be sent through the specified alert channel. You will receive the alert notification details through the channel. 

<span id="m1JdMwUM"></span>
## Related documentation


* [Receiving alert notifications by email](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-email)

* [Receiving alert notifications by Feishu custom bot](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-Lark)

* [Receiving alert notifications by Feishu application bot](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Lark_application_robot)

* [Receiving alert notifications by DingTalk](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-DingTalk)

* [Receiving alert notifications by WeCom](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Wecom)

* [Receiving alert notifications by phone](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-mobile-phone)

* [Receiving alert notifications by text message](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-SMS)
