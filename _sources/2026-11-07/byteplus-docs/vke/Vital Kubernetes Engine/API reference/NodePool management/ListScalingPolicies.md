---
title: "ListScalingPolicies"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListScalingPolicies"
---

Query the list of elastic scheduled scaling rules for node pools.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListScalingPolicies&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListScalingPolicies&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListScalingPolicies |The API name. The name of the current API is `ListScalingPolicies`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [ListScalingPoliciesFilter](https://docs.byteplus.com/en/docs/90/73597#listscalingpoliciesfilter) |No |\- |The filter for elastic scheduled scaling rules. |
|PageNumber |Integer |No |1 |The starting page number when querying. The default number is 1. |
|PageSize |Integer |No |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="listscalingpoliciesfilter"></span>
### ListScalingPoliciesFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |No |["spco2o8q2nvp211b\*\*\*"] |Use scaling policy IDs for filtering to implement precise querying. |
|Types |Array of String |No |["Scheduled"] |Use scaling policy types for filtering to implement precise querying. Valid values:<br><br><br>* **Scheduled**: CronJob<br><br>* **Recurrence**: Periodic jobs |
|ClusterIds |Array of String |No |["cc5silumrsfeqxxxx"] |Use cluster IDs for filtering to implement precise querying. |
|NodePoolIds |Array of String |No |["pc51i0m6rsfenxxxx"] |Use node pool IDs for filtering to implement precise querying. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=ListScalingPolicies&Version=2022-05-12
Content-Type: application/json
{
    "Filter": {
        "Ids": [
            "spco2o8q2nvp211b***"
        ],
        "Types": [
            "Scheduled"
        ],
        "ClusterIds": [
            "cc5silumrsfeqxxxx"
        ],
        "NodePoolIds": [
            "pc51i0m6rsfenxxxx"
        ]
    },
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [ScalingPolicy](https://docs.byteplus.com/en/docs/90/73597#scalingpolicy) |\- |The list of elastic scheduled scaling rules. |
|TotalCount |Integer |100 |The total number of elastic scheduled scaling rules that meet the conditions. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |10 |Number of records displayed per page. |


<span id="scalingpolicy"></span>
### ScalingPolicy


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |spco2o8q2n\*\*\*\*\*\*\*\* |The ID of the elastic scheduled scaling rule. |
|Type |String |Scheduled |The type of elastic scheduled scaling rule. Values:<br><br><br>* **Scheduled**: CronJob<br><br>* **Recurrence**: Periodic jobs |
|Enabled |Boolean |false |Whether the scaling policy is enabled. Valid values:<br><br><br>* **true**: Yes<br><br>* **false**: Disable |
|ClusterId |String |cc5silum\*\*\*\*\*\*\*\* |Cluster ID. |
|NodePoolId |String |pc51i0m6\*\*\*\*\*\*\*\* |The node pool ID. |
|AdjustmentValue |Integer |1 |Number of nodes to be added during node pool autoscaling. |
|ScheduledPolicy |Object of [ScheduledPolicyResponse](https://docs.byteplus.com/en/docs/90/73597#scheduledpolicyresponse) |\- |The CronJob or periodic job configuration. |
|ScheduledInstancePolicy |Object of [ScheduledInstancePolicyResponse](https://docs.byteplus.com/en/docs/90/73597#scheduledinstancepolicyresponse) |\- |The configurations of the elastic scheduled scaling policy. |
|CreateClientToken |String |BusinessRequest12345 |The string used during creation to ensure request idempotency.. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|UpdateClientToken |String |BusinessRequest12345 |Update the string used to ensure request idempotency. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|Name |String |test\-policy |The name of the elastic scheduled scaling rule. |


<span id="scheduledpolicyresponse"></span>
### ScheduledPolicyResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|LaunchTime |String |2022\-04\-01T16:00Z |The starting time of the job. The time follows the UTC standard and is accurate down to minutes. |
|RecurrenceType |String |Daily |The recurrence cycle of periodic jobs. Valid values:<br><br><br>* **Daily**: Execute once every few days.<br><br>* **Weekly**: Execute once per selected day of the week.<br><br>* **Monthly**: Execute once per selected day of the month. |
|RecurrenceValue |String |1 |The number of recurrences for periodic jobs. |
|RecurrenceEndTime |String |2022\-04\-02T16:00Z |The end time of the periodic job. The time follows the UTC standard and is accurate down to minutes. |


<span id="scheduledinstancepolicyresponse"></span>
### ScheduledInstancePolicyResponse


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|ElasticScheduledInstanceType |String |Esi |The type of elastic scheduled instances. Valid values:<br><br><br>* **Esi**: General\-purpose elastic scheduled instances<br><br>* **Segmented**: Segmented ESI |
|DeliveryType |String |Reserve |The delivery type for time period\-based elastic scheduled instances. Valid values:<br><br><br>* **Reserve**: Scheduled delivery<br><br>* **Immediate**: Immediate delivery |
|AutoReleaseTime |String |2022\-04\-01T18:10Z |Time of automatic release of scheduled instances. The time follows the UTC standard and is accurate down to minutes. This field has a value when the scheduling type is **Segmented ESI**. |
|StartDeliveryTime |String |2022\-04\-01T16:00Z |The start time of the delivery of the elastic scheduled instance. The time follows the UTC standard and is accurate down to minutes. |
|EndDeliveryTime |String |2022\-04\-01T16:10Z |The end time of the delivery of the elastic scheduled instance. The time follows the UTC standard and is accurate down to minutes. |
|BestEffort |Boolean |true |Whether to reserve as many instances as possible when the inventory of elastic scheduled instances cannot fully meet the reservation requirements.<br><br><br>* **false:**  At most one scheduled order will be generated.<br><br>* **true:**  When a single reservation order cannot meet the requirements, multiple reservation orders will be submitted. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104********",
        "Action": "ListScalingPolicies",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Id": "spco2o8q2********",
                "Name": "test-policy",
                "Type": "Scheduled",
                "Enabled": true,
                "ClusterId": "cc5silum********",
                "NodePoolId": "pc51i0m6********",
                "AdjustmentValue": 1,
                "ScheduledPolicy": {
                    "LaunchTime": "2022-04-01T16:00Z",
                    "RecurrenceType": "Daily",
                    "RecurrenceValue": "1",
                    "RecurrenceEndTime": "2022-04-02T16:00Z"
                },
                "CreateClientToken": "BusinessRequest12345",
                "UpdateClientToken": "BusinessRequest12345",
                "ScheduledInstancePolicy": {
                    "BestEffort": true,
                    "DeliveryType": "Reserve",
                    "AutoReleaseTime": "2022-04-01T18:10Z",
                    "EndDeliveryTime": "2022-04-01T16:10Z",
                    "StartDeliveryTime": "2022-04-01T16:00Z",
                    "ElasticScheduledInstanceType": "Esi"
                }
            }
        ],
        "TotalCount": 100,
        "PageNumber": 1,
        "PageSize": 10
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
