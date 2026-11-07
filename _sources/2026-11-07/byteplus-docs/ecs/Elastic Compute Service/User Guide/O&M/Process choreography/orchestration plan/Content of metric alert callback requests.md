---
title: "Content of metric alert callback requests"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Metric_alert_callback_request_content"
---

The content of a metric alert callback request includes callback request headers and the callback request body. [Learn more](https://docs.byteplus.com/en/docs/cloudmonitor/request-content-of-metric-alarm-callback).

<span id="v4trlFcc"></span>
## Callback request headers


|**Header key** |**Header value** |**Description** |
|---|---|---|
|x\-volc\-trace\-id |Random UUID |Used for request tracking. |
|x\-volc\-rule\-id |{ rule_id } |The policy ID. |


<span id="fhui7mys"></span>
## Callback request body

<span id="TNdvl4pW"></span>
### Data type

The data type of the request body is `application/json`.

<span id="Z7Onw3GD"></span>
### Request body parameters


|**Parameter​**  |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Type |String |Metric |The alert type. Valid value: Metric (threshold). |
|AccountId |String |210005\*\*\*\* |The account ID. |
|RuleName |String |Test alert policies |The policy name. |
|RuleId |String |193525924306958\*\*\*\* |The policy ID. |
|Namespace |String |VCM_FileNAS |The product type. |
|SubNamespace |String |latency |The dimension. |
|Level |String |critical |The alert level: Value:<br><br><br>* critical<br><br>* warning<br><br>* notice |
|HappenedAt |String |2024\-04\-11 14:51:01(UTC+08:00) |The time when the alert is triggered. |
|RuleCondition |String |An alert is triggered when any of the metrics reaches the threshold:<br><br>The average CPU usage exceeds 90% for 10 consecutive cycles (1 cycle = 1 minute).<br><br>The average memory usage exceeds 90% for 10 consecutive cycles (1 cycle = 1 minute). |The details of the alert policy. |
|Resources |Object |\- |The details of the resource for which the alert notification is sent. For the specific format, see **Resource structure**. |
|RecoveredResources |Object |\- |The details of the resource for which the alert cleared notification is sent. For the specific format, see **Resource structure**. |
|NoDataResources |Object |\- |The details of the resource for which the no data alert is triggered. For the specific format, see **Resource structure**. |
|NoDataRecoveredResources |Object |\- |The details of the resource for which the no data alert is cleared. For the specific format, see **Resource structure**. |


**Resource structure**


|**Parameter​**  |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Id |String |i\-ydvvy21se8r9cxxi\*\*\*\* |The resource ID. |
|Name |String |enas\-cn0445d06f\*\*\*\* |The resource name. |
|Region |String |cn\-beijing |The region. |
|FirstAlertTime |Int |1664332705 |The time when the alert is triggered for the first time. |
|LastAlertTime |Int |1664332705 |The time when the alert is triggered. |
|Metrics |Object |\- |The metrics for which parsing succeeded. For threshold alerts, see this field. For the specific format, see **Metric structure**. |
|NoDataMetrics |Object |\- |The metric for which no data points are collected. For more information about the no data alert, see this field. |
|DroppedMetrics |Object |\- |The metric for which parsing failed. For example, in numerical calculations related to alerts, a common scenario results in NaN: when the calculation logic involves division, if the dividend is 0, no valid number can be derived, and the system regards this result as unparsable. |
|AlertGroupId |String |68746e79885576cda23\*\*\*\* |The alert history ID. |
|Dimensions |Object |\- |The dimension information of the resource. For the specific format, see **Dimension structure**. |


**Metric structure**


|**Parameter​**  |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Name |String |Nfsv3WriteLat\*\*\*\* |The metric name. |
|Unit |String |ms |The unit of the metric. |
|Threshold |Float |1 |The threshold of the metric in this policy. |
|CurrentValue |Float |0.0001 |The current value of the metric. |
|Description |String |NFSv3 write latency |The description of the metric. |
|Warning |Bool |true |The alert triggered by the metric.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field exists only when the metric triggers an alert.</div><br> |


**Dimension structure**


|**Parameter​**  |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Name |String |ResourceID |The dimension of the metric. |
|Value |String |i\-ydvvy21se8r9cxxi\*\*\*\* |The value of the dimension. |
|NameCN |String |InstanceID |The Chinese name of the dimension. |


<span id="7xkdfWpJ"></span>
### Sample request body

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can skip parameters with no description in the actually received request body. These parameters do not affect your ability to obtain details of the alert notification.</div>


```JSON
{
  "AccountId": "210005****",
  "HappenedAt": "2025-07-22 20:24:44(UTC+08:00)",
  "Level": "warning",
  "Namespace": "VCM_ECS",
  "NoDataResources": [
    {
      "AlertGroupId": "68746e79885576cda23****",
      "Dimensions": [
        {
          "Description": "Instance",
          "Name": "ResourceID",
          "Value": "i-ydvvy21se8r9cxxi****"
        },
        {
          "Description": "Private Network",
          "Name": "IP.Inside",
          "Value": "192.xx.xx.17"
        },
        {
          "Description": "Public Network",
          "Name": "IP.Outside",
          "Value": "-"
        }
      ],
      "FirstAlertTime": 1752461461,
      "Id": "i-ydvvy21se8r9cxxi****",
      "LastAlertTime": 1753187084,
      "Name": "node-0000002",
      "NoDataMetrics": [
        {
          "CurrentValue": 0,
          "Description": "CPU Usage",
          "Name": "CpuTotal",
          "Threshold": 0,
          "Unit": "%"
        },
        {
          "CurrentValue": 0,
          "Description": "Memory Usage",
          "Name": "MemoryUsedUtilization",
          "Threshold": 0,
          "Unit": "%"
        }
      ],
      "ProjectName": "default",
      "Region": "cn-beijing",
      "Tags": {
        "volc:auto_scaling:scalingGroupId": "scg-ydvuyd19vml2a08a****",
        "volc:vke:cluster-id": "cd0imidbrtbp46pe4****",
        "volc:vke:created-by-cluster-id": "cd0imidbrtbp46pe4****",
        "volc:vke:createdby-vke-flag": "true",
        "volc:vke:nodepool-id": "pd0imidrrtbp46pe4****",
        "volc:vke:used-by-vke-cluster": "true",
        "volc:vke:vpc-id": "vpc-2byvea76anx8g2dx0een8****"
      }
    },
    {
      "AlertGroupId": "68746e79885576cda236****",
      "Dimensions": [
        {
          "Description": "Instance",
          "Name": "ResourceID",
          "Value": "i-ydvvcuyry8ygp2fc****"
        },
        {
          "Description": "Private Network",
          "Name": "IP.Inside",
          "Value": "192.xx.xx.3"
        },
        {
          "Description": "Public Network",
          "Name": "IP.Outside",
          "Value": "-"
        }
      ],
      "FirstAlertTime": 1752461461,
      "Id": "i-ydvvcuyry8ygp2fc****",
      "LastAlertTime": 1753187084,
      "Name": "node-0000001",
      "NoDataMetrics": [
        {
          "CurrentValue": 0,
          "Description": "CPU Usage",
          "Name": "CpuTotal",
          "Threshold": 0,
          "Unit": "%"
        },
        {
          "CurrentValue": 0,
          "Description": "Memory Usage",
          "Name": "MemoryUsedUtilization",
          "Threshold": 0,
          "Unit": "%"
        }
      ],
      "ProjectName": "default",
      "Region": "cn-beijing",
      "Tags": {
        "volc:auto_scaling:scalingGroupId": "scg-ydvuyd19vml2a08a****",
        "volc:vke:cluster-id": "cd0imidbrtbp46pe4****",
        "volc:vke:created-by-cluster-id": "cd0imidbrtbp46pe4****",
        "volc:vke:createdby-vke-flag": "true",
        "volc:vke:nodepool-id": "pd0imidrrtbp46pe4****",
        "volc:vke:used-by-vke-cluster": "true",
        "volc:vke:vpc-id": "vpc-2byvea76anx8g2dx0een8****"
      }
    }
  ],
  "Project": "default",
  "RuleCondition": "No data alarm :\nCPU usage rate: no data for 10 cycles (1 cycle = 1 minute)\memory usage rate: no data for 10 cycles (1 cycle = 1 minute)",
  "RuleId": "193525924306958****",
  "RuleName": "instance_test&test",
  "SubNamespace": "Instance",
  "Type": "MetricsNoData"
}
```
