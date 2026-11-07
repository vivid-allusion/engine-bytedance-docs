---
title: "Request content for a metric alert callback"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/request-content-of-metric-alarm-callback"
---

When an alert policy is triggered and an aggregation condition for sending an alert notification is met, Cloud Monitor sends a POST request to the specified URL through the alert callback API. The request content for a metric alert callback includes the callback request header (Header) and the callback request body (Body).

<span id="a0622d09"></span>
## Callback request header


|**Header Key** |**Header Value** |**Descriptions** |
|---|---|---|
|x\-volc\-trace\-id |Random UUID |This parameter is used for tracing the request. |
|x\-volc\-rule\-id |{ rule_id } |The policy ID. |


<span id="b2851ad1"></span>
## Callback request body

<span id="d4a50296"></span>
### Data type

The request body is of the `application/json` data type.

<span id="5eb24f4c"></span>
### Request body parameters


|**Parameters** |**Type** |**Sample value** |**Descriptions** |
|---|---|---|---|
|Type |String |Metric |The alert type.<br><br><br>* Metric: threshold alert<br><br>* Event: event alert<br><br>* MetricRecovered: alert recovery<br><br>* MetricsNoData: NoData alert<br><br>* NoDataRecovered: NoData alert recovery |
|AccountId |String |20\*\*\*\*\*007 |The account ID. |
|RuleName |String |Test alert policy |The policy name. |
|RuleId |String |1574726\*\*\*\*\*\*98880 |The policy ID. |
|Namespace |String |VCM_FileNAS |The service type. |
|SubNamespace |String |latency |The dimension. |
|Level |String |critical |The alert level. Valid values:<br><br><br>* critical<br><br>* warning<br><br>* notice |
|HappenedAt |String |2024\-04\-11 14:51:01(UTC+08:00) |The time when the alert is triggered. |
|RuleCondition |String |Multi\-metric alert (any):<br><br>Average CPU utilization \> 90% for consecutive 10 cycles (1 cycle = 1 minute)<br><br>Average memory utilization \> 90% for consecutive 10 cycles (1 cycle = 1 minute) |The details of the alert policy. |
|Resources |Array |\- |The resource details of the alert notification. For the specific format, refer to the **Resource structure** section of this topic. |
|RecoveredResources |Array |\- |The resource details of the alert recovery notification. For the specific format, refer to the **Resource structure** section of this topic. |
|NoDataResources |Array |\- |The resource details of the NoData alert. For the specific format, refer to the **Resource structure** section of this topic. |
|NoDataRecoveredResources |Array |\- |The resource details of the NoData alert recovery notification. For the specific format, refer to the **Resource structure** section of this topic. |


**Resource structure**


|**Parameters** |**Type** |**Sample value** |**Descriptions** |
|---|---|---|---|
|Id |String |enas\-cn04\*\*\*\*\*45d06f |The resource ID. |
|Name |String |enas\-cn04\*\*\*\*\*45d06f |The resource name. |
|Region |String |cn\-north\-3 |The region. |
|FirstAlertTime |Int |1664332705 |The time when the alert was triggered for the first time. |
|LastAlertTime |Int |1664332705 |The time when the alert is triggered. |
|Metrics |Object |\- |The resolved metrics. This field applies to threshold alerts. For the specific format, refer to the **Metric structure** section of this topic. |
|NoDataMetrics |Object |\- |The metric with no data reported. This field applies to NoData alerts. |
|DroppedMetrics |Object |\- |The unresolved metrics. For example, if this parameter is set to NaN, division is used for alert calculation in some scenarios, but the divisor is 0. As a result, the calculation result is deemed unresolvable. |
|AlertGroupId |String |673\*\*\*\*\*\*a06 |The ID of the alert record. |
|Dimensions |Object |\- |The resource dimension. For the specific format, refer to the **Dimension structure** section of this topic. |


**Metric structure**


|**Parameters** |**Type** |**Sample value** |**Descriptions** |
|---|---|---|---|
|Name |String |Nfsv3WriteLatency |The metric name. |
|Unit |String |ms |The metric unit. |
|Threshold |Float |1 |The metric threshold of the policy. |
|CurrentValue |Float |0.0001 |The current value of the metric. |
|Description |String |NFSv3 write latency |The description of the metric. |
|Warning |Bool |true |The metric triggers an alert. This parameter is available only when the metric triggers an alert. |


**Dimension structure**


|**Parameters** |**Type** |**Sample value** |**Descriptions** |
|---|---|---|---|
|Name |String |ResourceID |The metric dimension. |
|Value |String |enas\-cn04\*\*\*\*\*45d06f |The value of the dimension. |
|NameCN |String |Instance ID |The dimension name in Chinese. |


<span id="6d346a9c"></span>
### Sample request body

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can ignore parameters without descriptions in the received request body. These parameters do not prevent you from obtaining the details of the alert notification.</div>


<span id="cd3b19e2"></span>
#### alert notification request body

```Go
{
  "Type": "Metric",
  "AccountId": "20******007",
  "RuleName": "Test alert policy",
  "RuleId": "1574726******98880",
  "Namespace": "VCM_FileNAS",
  "SubNamespace": "latency",
  "Level": "critical",
  "HappenedAt":"2024-04-11 14:51:01(UTC+08:00)",
  "RuleCondition":"Multi-metric alert (any): Average CPU utilization > 90% for consecutive 10 cycles (1 cycle = 1 minute), Average memory utilization > 90% for consecutive 10 cycles (1 cycle = 1 minute)",
  "Resources": [
    {
      "Id": "enas-cn04*****45d06f",
      "Name": "enas-cn04*****45d06f",
      "Region": "cn-north-3",
      "FirstAlertTime": 1664332705,
      "LastAlertTime": 1664332705,
      "Metrics": [
        {
          "Name": "Nfsv3WriteLatency",
          "Unit": "ms",
          "Threshold":1,
          "CurrentValue": 0.0001,
          "Description": "NFSv3 write latency",
        }
      ],
      "AlertGroupId": "673******a06",
      "Dimensions": [
        {
          "Name": "ResourceID",
          "NameCN": "Instance ID",
          "Value": "enas-cn04*****45d06f"
        },
        {
          "Name": "Node",
          "NameCN": "Node",
          "Value": "enas-cn04*****45d06f-pod-0"
        }
      ]
    }
  ]
}
```


<span id="0dd4e3ac"></span>
#### Alert recovery notification request body

```Go
{
    "Type": "MetricRecovered",
    "AccountId": "20******007",
    "RuleName": "Test alert policy",
    "RuleId": "1574726******98880",
    "Namespace": "VCM_FileNAS",
    "SubNamespace": "latency",
    "Level": "critical",
    "HappenedAt":"2024-04-11 14:51:01(UTC+08:00)",
    "RuleCondition":"Multi-metric alert (any): Average CPU utilization > 90% for consecutive 10 cycles (1 cycle = 1 minute), Average memory utilization > 90% for consecutive 10 cycles (1 cycle = 1 minute)",
    "Resources":[],
    "RecoveredResources": [
        {
            "Id": "enas-cn04*****45d08k",
            "Name": "enas-cn04*****45d08k",
            "Region": "cn-north-3",
            "FirstAlertTime": 1664332705,
            "LastAlertTime": 1664332705,
            "Metrics": [
                {
                    "Name": "Nfsv3WriteLatency",
                    "Unit": "ms",
                    "Threshold":1,
                    "CurrentValue": 0.5,
                    "Description": "NFSv3 write latency"
                }
            ],
            "AlertGroupId": "673******a06",
            "Dimensions": [
                {
                    "Name": "ResourceID",
                    "NameCN": "Instance ID",
                    "Value": "enas-cn04*****45d06f"
                },
                {
                    "Name": "Node",
                    "NameCN": "Node",
                    "Value": "enas-cn04*****45d06f-pod-0"
                }
            ]
        }
    ]
}
```


<span id="37b24ca2"></span>
#### NoData alert notification request body

```Go
{
    "Type": "MetricsNoData",
    "AccountId": "21*****168",
    "RuleName": "test",
    "RuleId": "18039******80320",
    "Namespace": "VCM_ECS",
    "SubNamespace": "Instance",
    "HappenedAt": "2024-07-12 00:43:06(UTC+08:00)",
    "RuleCondition": "Multi-metric alert (any):\nAverage out-of-band CPU utilization!=12% for 1 cycle (1 cycle = 1 minute)\nAverage CPU utilization!=14% for 1 cycle (1 cycle = 1 minute)\nNIC maximum outbound rate!=11 bit/s for 1 cycle (1 cycle = 1 minute)",
    "Level": "warning",
    "NoDataResources": [
        {
            "Id": "i-ycd1********dfy01t",
            "Name": "cloudmonitor-test-project",
            "Region": "cn-guilin-boe",
            "FirstAlertTime": 1720704066,
            "LastAlertTime": 1720716186,
            "Metrics": [
                {
                    "Name": "Instance_CpuBusy",
                    "Unit": "%",
                    "Threshold": 12,
                    "CurrentValue": 0.0583,
                    "Description": "Out-of-band CPU utilization",
                    "Warning": true,
                },
                {
                    "Name": "CpuTotal",
                    "Unit": "%",
                    "Threshold": 14,
                    "CurrentValue": 0.03,
                    "Description": "CPU utilization",
                    "Warning": true,
                }
            ],
            "NoDataMetrics": [
                {
                    "Name": "NetworkPerNicOutRate",
                    "Unit": "bit/s",
                    "Threshold":0,
                    "CurrentValue":0,
                    "Description": "NIC outbound rate"
                }
            ],
            "AlertGroupId": "673******a06",
            "Dimensions": [
                {
                    "Name": "ResourceID",
                    "Value": "i-ycd1********fy01t",
                    "Description": "Instance"
                },
                {
                    "Name": "IP.Inside",
                    "Value": "192.168.**.**",
                    "Description": "Private network"
                },
                {
                    "Name": "IP.Outside",
                    "Value": "10.249.**.**",
                    "Description": "Public Network"
                }
            ]
        }
    ]
}
```


<span id="c05b8e72"></span>
#### NoData alert recovery notification request body

```Go
{
    "Type": "NoDataRecovered",
    "AccountId": "21******00",
    "RuleName": "test_custom",
    "RuleId": "18076********524992",
    "Namespace": "VCM_CloudMonitor_Metrics_Test_Tool",
    "SubNamespace": "base",
    "HappenedAt": "2024-07-02 15:27:03(UTC+08:00)",
    "RuleCondition": "Multi-metric alert (all): \nMaximum seconds of the minute-level cycle\u003e1ms for consecutive 1 cycle (1 cycle = 1 minute) \nMaximum hours\u003e1ms for consecutive 1 cycle (1 cycle = 1 minute)",
    "Level": "critical",
    "NoDataRecoveredResources": [
        {
            "Id": "1784**********92608",
            "Name": "Test random",
            "Region": "cn-taiwan-boe",
            "FirstAlertTime": 1719902340,
            "LastAlertTime": 1719905223,
            "Metrics": [
                {
                    "Name": "graph_seconds_of_minutes",
                    "Unit": "ms",
                    "Threshold":1,
                    "CurrentValue": 60000,
                    "Description": "The seconds of the minute-level cycle"
                }
            ],
            "AlertGroupId": "673******a06",
            "Dimensions": [
                {
                    "Name": "ResourceID",
                    "Value": "1784*********92608",
                    "Description": "base"
                },
                {
                    "Name": "Status",
                    "Value": "Running",
                    "Description": "Status"
                }
            ],
            "DroppedMetrics": [
                {
                    "Name": "graph_hours_of_days",
                    "Unit": "ms",
                    "Threshold":1,
                    "CurrentValue": "NaN",
                    "Description": "Hours",
                    "Reason": "float64 NaN can not encoded by JSON"
                }
            ]
        }
    ]
}
```
