---
title: "Configure custom alert rules"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules"
---

VKE provides comprehensive cluster monitoring and alert capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). The capabilities cover typical scenarios such as the control plane, nodes, networks, workloads, and AI training tasks. This topic describes how to manually create custom alert rules and configure alert trigger conditions and notification policies in the VMP console.

<span id="AWLb7foK"></span>
## **Prerequisites**


* The cloud\-native observability feature has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* An alert notification object or policy has been created. For details, see [Creating contacts](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-receivers), [Creating contact groups](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-receiver-groups), and [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Alert rules are defined by PromQL statements. We recommend that you first understand basic PromQL concepts and the meaning of the metrics exposed by monitoring targets. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/PromQL-quick-start">Getting started with PromQL</a>.</div>


<span id="4rOZJDod"></span>
## Procedure

When neither preset templates nor custom templates can meet your specific business requirements, you can manually create independent alert rules by directly writing PromQL statements and trigger policies. This method does not rely on template reuse and applies to one‑time, temporary alert scenarios tailored for specific businesses. Procedure:


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, click **Alarm Center \> Alarm Rule**. Click **Create** \> **Create manually**.

4. Configure the alert rule details.

   * Configure basic information for the alert rule.

   * Configure alert trigger conditions.

   
   |**Parameter** |**Description** |
   |---|---|
   |Workspace |Select a workspace associated with the cluster from the drop\-down list. |
   |Query statement |Use standard PromQL statements to configure monitoring objects or metrics. |
   |Trigger policy |Configure alert trigger policies. Specify the alert level, condition, threshold, and condition duration.<br><br><br>* Select P0, P1, or P2 to set different alert levels. If you do not select an option, alerts at this level are not configured.<br><br>* **Comparison condition**: Specify the comparison condition between the PromQL statement and the threshold. You can configure multiple comparison conditions, including **Greater than**, **Greater than or equal to**, **Less than**, **Less than or equal to**, **Equal to**, and **Not equal to**.<br><br>* **Threshold**: Set the threshold of the metric.<br><br>* **Condition duration**: Configure the duration for which the metric meets the condition. Valid values:<br><br>   * **Trigger immediately**: An alert is triggered immediately if the alerting condition is met.<br><br>   * **Custom duration**: Select an alert trigger time. Available options include 1 minute, 2 minutes, 5 minutes, 10 minutes, 20 minutes, 30 minutes, 1 hour, 3 hours, 6 hours, and 12 hours. For example, 1 minute means that the alert will be triggered after the condition has been met for 1 minute. |
   

   * Configure alert notifications. You can choose notification policies and aggregation policies in the unified Alert Center or the Alert policy module of the VMP console. The notification policy specifies which contacts or contact groups receive alerts and through which channels. The aggregation policy controls whether multiple alerts are merged and sent, reducing repeated notifications.

5. Click **Confirm**.


<span id="wPLLJN5C"></span>
## Validate results

<span id="NkbVTA4f"></span>
### View settings

After the alert rule is created, you can view the rule status in the alert rule list of the VMP console.

When an alert is generated, you can view the trigger records on the **Alert event** page and troubleshoot issues by referencing the add\-on status, Pod events, and logs in the VKE console.

&nbsp;

<span id="2sM4IfvJ"></span>
### Receive alerts

After you have completed alert\-related configuration, when an alert that matches the defined rules is triggered, a notification will be sent through the specified alert channel. You will receive the alert notification details through the channel. 

<span id="uqhGHPND"></span>
## Related documentation


* [Receiving alert notifications by email](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-email)

* [Receiving alert notifications by Feishu custom bot](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-Lark)

* [Receiving alert notifications by Feishu application bot](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Lark_application_robot)

* [Receiving alert notifications by DingTalk](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-DingTalk)

* [Receiving alert notifications by WeCom](https://docs.byteplus.com/en/docs/vmp/Receiving_alerting_notifications_through_Wecom)

* [Receiving alert notifications by phone](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-mobile-phone)

* [Receiving alert notifications by text message](https://docs.byteplus.com/en/docs/vmp/Receiving-alerting-notifications-through-SMS)
