---
title: "Creating silence policies"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Creating_silence_policies"
---

Silence policies are primarily used to suppress frequent but low\-priority alerts, preventing them from overwhelming more important alerts and allowing recipients to focus on issues that truly matter. This topic describes how to create a silence policy.

<span id="CpZnNwDp"></span>
## Limits


* Currently, you can create up to 1,000 silence policies.

* You can create up to 10 match conditions.


<span id="xwJcF9wN"></span>
## Procedure


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select "**Alert Center \-\> Silence Policy**" to go to the "Silence Policy" page.

3. Select the **Custom policy ** tab, click ** Create suppression policy**, and configure the silence policy parameters as needed.

   
   |Parameter |Description |
   |---|---|
   |Policy name |Specify a name for the silence policy, which serves as a unique identifier. Duplicate names are not allowed. |
   |Silent matching |The rules of the silence policy. Configuration items vary by product. You can configure the rules based on the selected suppression type. |
   ||When the suppression type is set to Cloud Monitor, configure the following parameters:<br><br><br>* **Resource type**: The cloud service to be suppressed.<br><br>* **Alert policy**: Specify the alert policy to be suppressed. If you do not specify an alert policy, notifications are not suppressed based on alert policies.<br><br>* **Suppressed resource**: The scope of resources whose alert notifications are suppressed. You can select all resources or specific resources. When you select **Partial resources**, you can configure the relationship between match rules, including:<br><br>   * **All are met**: Individual match rules have a logical **AND ** relationship. All the specified rules must be satisfied to trigger this silence policy.<br><br>   * **Anyone is met**: Individual rules have a logical **OR** relationship. Any match rule satisfied will trigger this silence policy. |
   ||When the suppression type is set to Cloud Service Event, configure the following parameters:<br><br><br>* **Event source**: The event source to be suppressed.<br><br>* **Event type**: Specify the event type to be suppressed.<br><br>* **Event rule**: Specify the event rule to be suppressed. If you do not specify an event rule, notifications are not suppressed based on event rules.<br><br>* **Suppressed resource**: The scope of resources whose event notifications are suppressed. You can select all resources or specific resources. When you select **Partial resources**, you can configure the relationship between match rules, including:<br><br>   * **All are met**: Individual match rules have a logical **AND ** relationship. All the specified rules must be satisfied to trigger this silence policy.<br><br>   * **Anyone is met**: Individual rules have a logical **OR** relationship. Any match rule satisfied will trigger this silence policy. |
   ||When the suppression type is set to VMP or Server\-side Monitoring, configure the following parameters:<br><br><br>* **Shielded region**: Specify the region to which the suppressed notifications belong.<br><br>* **Alert policy**: Specify the alert policy of the notifications to be suppressed.<br><br>* **Match condition**: Use the labels included in the alerts to match the alert events to be suppressed. Example: `job:kubernetes-etcd`. You can configure multiple label groups. Each label group can contain multiple labels.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The logical <strong>OR</strong> relationship applies between label groups. The logical <strong>AND</strong> relationship applies between labels within a label group.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In addition to the labels in alert events, the <code>__alerting_rule_id</code> label (alert rule ID) is also supported. You can use this label to search for the target alert rule.</div><br> |
   |Effective time |The effective time of the silence policy, which can be configured as needed.<br><br><br>* **Suppression at absolute time**: The silence policy applies within the specified, fixed period of time.<br><br>* **Suppression at relative time**: The silence applies periodically within the specified cycle.<br><br>* **Suppress permanently**: No specific suppression time is required. As long as the silence policy is effective, suppression is enabled. To disable suppression when this configuration is selected, manually stop the corresponding silence policy. |
   |Time range |If you select ** Suppression at absolute time** for Effective period, configure the time range during which suppression takes effect. The time range is a subset of the effective period. You can use this parameter to specify a specific period during which the silence policy takes effect. |
   |Cyclic time type |If you select ** Suppression at relative time ** for Effective period, you also need to configure Cyclic time type for suppression. The time range is a subset of the effective period. You can use this parameter to specify a specific period during which the suppression policy takes effect.<br><br><br>* **Cycle permanently**: Configure a specific time period on a daily, weekly, or monthly basis during which the silence policy takes effect.<br><br>* **Cycle in specified days**: Specify a date range, and then configure a specific time period on a daily, weekly, or monthly basis during which the silence policy takes effect. |
   


&nbsp;
