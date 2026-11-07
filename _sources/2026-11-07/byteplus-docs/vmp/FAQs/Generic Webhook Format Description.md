---
title: "Generic Webhook Format Description"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/general-webhook-format"
---

Vital Managed Service for Prometheus supports using Generic Webhook to receive alert information. This article introduces the format of the Generic Webhook.

<span id=".6IOM5pmv"></span>
## Background

You can create an alert notification policy in Vital Managed Service for Prometheus and specify using Generic Webhook to receive alert information. For more details, please refer to [Creating an Alert Notification Policy](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules).

In this scenario, how to parse the information format sent by the Generic Webhook on the receiving end and clarify the meaning of different fields is particularly important.

<span id=".5qC85byP56S65L6L"></span>
## Format Example

The following is an example of the Generic Webhook format.

```json
{
  "status": "firing",
  "alerts": [
    {
      "status": "firing",
      "labels": {
        "account_id": "200000000",
        "internal_label_alert_id": "7f55f4xxx",
        "internal_label_alert_level": "P0",
        "alertname": "aec4cc4a-5457-4a31-b378-0442d140e6b8", 
        "__name__": "container_memory_usage_bytes",        
        "node": "192.168.1.158"
      },
      "annotations": {
        "__alerting_resource_current_value__": "1",
        "__alerting_rule_levels__": "[{\"AlertingRuleID\":\"aec4cc4a-5457-4a31-b378-0442d140e6b8\",\"Level\":\"P0\",\"For\":\"0s\",\"Comparator\":\"\\u003c\",\"Threshold\":5},{\"AlertingRuleID\":\"aec4cc4a-5457-4a31-b378-0442d140e6b8\",\"Level\":\"P1\",\"For\":\"0s\",\"Comparator\":\"\\u003c\",\"Threshold\":6},{\"AlertingRuleID\":\"aec4cc4a-5457-4a31-b378-0442d140e6b8\",\"Level\":\"P2\",\"For\":\"0s\",\"Comparator\":\"\\u003c\",\"Threshold\":7}]",
        "__alerting_rule_query__": "{\"AlertingRuleID\":\"aec4cc4a-5457-4a31-b378-0442d140e6b8\",\"PromQL\":\"container_memory_usage_bytes{container=\\\"\\\"}\",\"WorkspaceID\":\"046afaa0-8dc4-446a-bf36-df2d7a8aab99\"}",
        "__alerting_rule_type__": "vmp/PromQL"
      },
      "startsAt": "2022-11-24T19:31:00+08:00",
      "endsAt": "0001-01-01T00:00:00Z",
      "generatorURL": "",
      "fingerprint": "81e649cc69c24b6d"
    }
  ],
  "groupLabels": {
    "internal_label_alert_level": "P0",
    "alertname": "aec4cc4a-5457-4a31-b378-0442d140e6b8"
  },
  "commonLabels": {
    "account_id": "200000000",
    "internal_label_alert_id": "7f55f4-0dd81796416f412f-c20ca4036a7f4260",
    "internal_label_alert_level": "P0",
    "alertname": "aec4cc4a-5457-4a31-b378-0442d140e6b8",
    "__name__": "container_memory_usage_bytes",       
    "node": "192.168.1.158"
  },
  "commonAnnotations": {
   "__alerting_resource_current_value__":"1",
    "__alerting_rule_levels__": "[{\"AlertingRuleID\":\"aec4cc4a-5457-4a31-b378-0442d140e6b8\",\"Level\":\"P0\",\"For\":\"0s\",\"Comparator\":\"\\u003c\",\"Threshold\":5},{\"AlertingRuleID\":\"aec4cc4a-5457-4a31-b378-0442d140e6b8\",\"Level\":\"P1\",\"For\":\"0s\",\"Comparator\":\"\\u003c\",\"Threshold\":6},{\"AlertingRuleID\":\"aec4cc4a-5457-4a31-b378-0442d140e6b8\",\"Level\":\"P2\",\"For\":\"0s\",\"Comparator\":\"\\u003c\",\"Threshold\":7}]",
    "__alerting_rule_query__": "{\"AlertingRuleID\":\"aec4cc4a-5457-4a31-b378-0442d140e6b8\",\"PromQL\":\"container_memory_usage_bytes{container=\\\"\\\"}\",\"WorkspaceID\":\"046afaa0-8dc4-446a-bf36-df2d7a8aab99\"}",
    "__alerting_rule_type__": "vmp/PromQL",
  },
  "alertingRuleName": "name"
}
```


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter Description

The parameter descriptions in the Generic Webhook are shown in the table below.


|Field name |Type |Sample Values |Description |
|---|---|---|---|
|status |string |firing |Status of the Webhook, values:<br><br><br>* **firing**: alerting<br><br>* **resolved**: resolved |
|alerts |list [Alert](https://docs.byteplus.com/en/docs/vmp/general-webhook-format) | |Alert event content. |
|groupLabels |map<string,string\> |\- |Labels for aggregated notifications sent by the Webhook. |
|commonLabels |map<string,string\> |\- |Common labels of alert events. |
|commonAnnotations |map<string,string\> |\- |Common annotations of alert events. |
|alertingRuleName |string |CPU usage exceeds 80%. |Name of the alert rule. |


<span id="Alert"></span>
### Alert

The structure of alert is shown in the table below.


|**Field name** |**Type** |**Sample Values** |**Description** |
|---|---|---|---|
|status |string |firing |Status of the alert event, values:<br><br><br>* **firing**: alerting<br><br>* **resolved**: resolved |
|labels |map<string,string\> |```json```<br>```{```<br>```    "account_id": "200000000",```<br>```    "internal_label_alert_id": "7f55f4xxxx",```<br>```    "internal_label_alert_level": "P1",```<br>```    "alertname": "aec4cc4a-5457-4a31-b378-0442d140e6b8",```<br>```    "__name__": "container_memory_usage_bytes",```<br>```    "node": "192.168.1.158",```<br>```    "job": "kubelet-cadvisor"```<br>```}```<br> |* Alert event metadata, including:<br><br>   * Built\-in information.<br><br>      * `account_id`: BytePlus account (root user) ID.<br><br>      * `alertname`: alert rules ID.<br><br>      * `internal_label_alert_id`: current alert event ID.<br><br>      * `internal_label_alert_level`: current alert event level.<br><br>   * Labels of the PromQL query result, e.g.:<br><br>   ```json```<br>```   "__name__": "container_memory_usage_bytes"```<br>```   "node": "192.168.1.158"```<br>```   "job": "kubelet-cadvisor"```<br>```   ```<br>    |
|annotations |map<string,string\> |```json```<br>```{```<br>```    "__alerting_resource_current_value__": "1",```<br>```    "__alerting_rule_levels__": "[{\"AlertingRuleID\":\"aec4cc4axxxx"}]",```<br>```    "__alerting_rule_query__": "{\"AlertingRuleID\":\"aec4cc4axxx"}",```<br>```    "__alerting_rule_type__": "vmp/PromQL"```<br>```}```<br> |* Alert event metadata, including:<br><br>   * Rule metadata.<br><br>      * `__alerting_rule_levels__`: Alert rules level configuration.<br><br>      * `__alerting_rule_query__`: PromQL configuration of alert rules.<br><br>      * `__alerting_rule_type__`: Alert rules type.<br><br>   * `__alerting_resource_current_value__`: Current value of the event. |
|startsAt |string |2022\-11\-24T19:31:00+08:00 |The time when the alert event was triggered. |
|endsAt |string |0001\-01\-01T00:00:00Z |The end time of the alert event.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <code>status</code> of the alert event is <code>firing</code>, <code>endsAt</code> is default <code>0001-01-01T00:00:00Z</code>, then this value has no actual meaning.</div><br> |
