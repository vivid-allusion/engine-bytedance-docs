---
title: "CreateScalingPolicy"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateScalingPolicy"
---

Create an elastic scheduled scaling rule for a node pool.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateScalingPolicy&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateScalingPolicy&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateScalingPolicy |The API name. The name of the current API is `CreateScalingPolicy`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |cc5silum\*\*\*\*\*\*\*\* |Cluster ID.<br><br>Cluster IDs can be obtained by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in the <code>{Running,[Ok]}</code> or <code>{Updating,[Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to obtain the current status of the cluster.</div><br> |
|NodePoolId |String |Yes |pc51i0m6\*\*\*\*\*\*\*\* |The node pool ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The node pool must be in the <code>{Running,[*]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListNodePools">ListNodePools</a> API to obtain the current status of the node pool.</div><br> |
|Type |String |Yes |Scheduled |The type of the elastic scheduled scaling rule. Values:<br><br><br>* **Scheduled**: CronJob<br><br>* **Recurrence**: Periodic jobs |
|AdjustmentValue |Integer |Yes |1 |The number of nodes to be added during node pool autoscaling. The value is an integer. Valid values: 1 to 500. |
|ScheduledPolicy |Object of [ScheduledPolicyRequest](https://docs.byteplus.com/en/docs/90/73596#scheduledpolicyrequest) |Yes |\- |The CronJob or periodic job configuration. |
|ScheduledInstancePolicy |Object of [ScheduledInstancePolicyRequest](https://docs.byteplus.com/en/docs/90/73596#scheduledinstancepolicyrequest) |Yes |\- |The configurations of the elastic scheduled scaling policy. |
|Enabled |Boolean |No |false |Whether to enable the elastic scheduled scaling rule. Values:<br><br><br>* **true**: Enable scaling policies.<br><br>* **false**: (Default) Disable scaling policies. |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|Name |String |No |test\-policy |The name of the elastic scheduled scaling rule.<br><br><br>* It can contain Chinese characters, letters, numbers, underscores (`_`), and hyphens (`-`). Other special characters are currently not supported.<br><br>* It can start only with a Chinese character or a letter.<br><br>* The length can be 1 to 128 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The rule name must be unique within the same node pool.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not explicitly configure it, the system automatically names the elastic scheduled scaling rule in the format of <code>vke-{ClusterId}-{NodePoolId}</code>.</div><br> |


<span id="scheduledpolicyrequest"></span>
### ScheduledPolicyRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|LaunchTime |String |Yes |2022\-04\-01T16:00Z |The start time of the job. The time follows the UTC standard and is accurate down to minutes. This parameter is valid and required only if the `Type` parameter is set to `Scheduled` or `Recurrence`.<br><br><br>* If the `Type` parameter is set to `Scheduled`, it indicates the trigger time of the CronJob.<br><br>* If the `Type` parameter is set to `Recurrence`, it indicates the start time of the periodic job.<br><br>* The value must be greater than the current time, and you need to set the value to a time point within 90 days after the creation or modification time.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To ensure that the scheduled scale\-out request is submitted, we recommend that you set the <code>LaunchTime</code> parameter to a value at least 1 minute later than the current time.</div><br> |
|RecurrenceType |String |No |Daily |The interval at which the periodic job is performed. This parameter is valid and required only if the `Type` parameter is set to `Recurrence`. Valid values:<br><br><br>* **Daily**: Execute once every few days.<br><br>* **Weekly**: Execute once per selected day of the week.<br><br>* **Monthly**: Execute once per selected day of the month. |
|RecurrenceValue |String |No |1 |The number of recurrences for periodic jobs. This parameter is valid and required only if the `Type` parameter is set to `Recurrence`.<br><br><br>* If the `RecurrenceType` parameter is set to `Daily`, you can enter only one value within the range from 1 to 31.<br><br>* If the `RecurrenceType` parameter is set to `Weekly`, you can enter multiple values, and you need to separate these values with commas (`,`). The values that correspond to days of the week are as follows: Monday to Sunday are represented by 1, 2, 3, 4, 5, 6, and 7, respectively.<br><br>* If the `RecurrenceType` parameter is set to `Monthly`, the value is in the format of `A-B`. Both A and B range from 1 to 31, and B must be greater than or equal to A. |
|RecurrenceEndTime |String |No |2022\-04\-02T16:00Z |The end time of the periodic job. The time follows the UTC standard and is accurate down to minutes. This parameter is valid and required only if the `Type` parameter is set to `Recurrence`.<br><br>The value must be greater than or equal to `LaunchTime` and must be a time point within 365 days after the creation or modification time. |


<span id="scheduledinstancepolicyrequest"></span>
### ScheduledInstancePolicyRequest


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|ElasticScheduledInstanceType |String |Yes |Esi |The type of elastic scheduled instances. Valid values:<br><br><br>* **Esi**: General\-purpose elastic scheduled instances<br><br>* **Segmented**: Segmented ESI |
|DeliveryType |String |No |Reserve |The delivery type for Segmented ESI. Valid values:<br><br><br>* **Reserve**: Scheduled delivery<br><br>* **Immediate**: Immediate delivery<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid and required only if the <code>ElasticScheduledInstanceType</code> parameter is set to <code>Segmented</code> (<strong>Segmented ESI</strong>).</div><br> |
|AutoReleaseTime |String |No |2022\-04\-01T18:10Z |The time when the scheduled instances are automatically released. The time follows the UTC standard and is accurate down to minutes. This parameter is valid and required only if the `ElasticScheduledInstanceType` parameter is set to `Segmented` (**Segmented ESI**). The time must be a 10‑minute mark.<br><br><br>* If the `DeliveryType` parameter is set to `Reserve`, which indicates **scheduled delivery**, this time must be at least one hour later than the scheduled delivery time.<br><br>* If the `DeliveryType` parameter is set to `Immediate`, which indicates **immediate delivery**, the earliest release time is the next 10\-minute mark after the current time. For example, if the current time is 5:02, the earliest automatic release time is 5:20. |
|StartDeliveryTime |String |No |2022\-04\-01T16:00Z |The start time of the delivery of the elastic scheduled instance. The time follows the UTC standard and is accurate down to minutes. The time must be a 10‑minute mark. Valid values:<br><br><br>* If the `ElasticScheduledInstanceType` parameter is set to `Esi` (**general‑purpose elastic scheduled instance**), this parameter is required and valid.<br><br>   * The value must be between 4 and 8 hours after the start time (`LaunchTime`) of the periodic job.<br><br>* If the `ElasticScheduledInstanceType` parameter is set to `Segmented` (**Segmented ESI**):<br><br>   * If the `DeliveryType` parameter is set to `Reserve`, which indicates scheduled delivery, this parameter is required and valid. The value must be within 24 hours after the start time (`LaunchTime`) of the periodic job.<br><br>   * If the `DeliveryType` parameter is set to `Reserve`, which indicates immediate delivery, you do not need to specify this parameter. |
|EndDeliveryTime |String |No |2022\-04\-01T16:10Z |The end time of the delivery of the elastic scheduled instance. The time follows the UTC standard and is accurate down to minutes. The time must be a 10‑minute mark, and the interval between this time and `StartDeliveryTime` must be exactly 10 minutes. Valid values:<br><br><br>* If the `ElasticScheduledInstanceType` parameter is set to `Esi` (**general‑purpose elastic scheduled instance**), this parameter is required and valid.<br><br>   * The value must be between 4 and 8 hours after the start time (`LaunchTime`) of the periodic job.<br><br>* If the `ElasticScheduledInstanceType` parameter is set to `Segmented` (**Segmented ESI**):<br><br>   * If the `DeliveryType` parameter is set to `Reserve`, which indicates scheduled delivery, this parameter is required and valid. The value must be within 24 hours after the start time (`LaunchTime`) of the periodic job.<br><br>   * If the `DeliveryType` parameter is set to `Reserve`, which indicates immediate delivery, you do not need to specify this parameter. |
|BestEffort |Boolean |No |true |Specify whether to reserve as many instances as possible when the inventory of elastic scheduled instances cannot fully meet the reservation requirements.<br><br><br>* **false**: (Default) At most one scheduled order will be generated.<br><br>* **true:**  When a single scheduled order cannot meet the requirements, multiple scheduled orders will be submitted. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=CreateScalingPolicy&Version=2022-05-12
Content-Type: application/json
{
    "ClusterId": "cc5silum********",
    "NodePoolId": "pc51i0m6********",
    "Name": "test-policy",
    "Type": "Scheduled",
    "AdjustmentValue": 1,
    "ScheduledPolicy": {
        "LaunchTime": "2022-04-01T16:00Z",
        "RecurrenceType": "Daily",
        "RecurrenceValue": "1",
        "RecurrenceEndTime": "2022-04-02T16:00Z"
    },
    "ScheduledInstancePolicy": {
        "BestEffort": true,
        "DeliveryType": "Reserve",
        "AutoReleaseTime": "2022-04-01T18:10Z",
        "EndDeliveryTime": "2022-04-01T16:10Z",
        "StartDeliveryTime": "2022-04-01T16:00Z",
        "ElasticScheduledInstanceType": "Esi"
    },
    "Enabled": false,
    "ClientToken": "BC028527-33B9-4990-A633-84E9F9******"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |spco2o8q2n\*\*\*\*\*\*\*\* |The scaling rule ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "CreateScalingPolicy",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "spco2o8q2n********"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For public error codes, see [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied.ClusterStatus |The action is forbidden due to cluster status {{statusPhase}} and {{statusConditions}}. |The current status of the specified cluster does not support this operation. Please confirm the required cluster status for this API and try again. |
|400 |OperationDenied.NodePoolStatus |The action is forbidden on node pool {{nodePoolId}} due to node pool status {{statusPhase}} and {{statusConditions}}. |The current status of the specified node pool does not support this operation. Please confirm the required node pool status for this API and try again. |
|400 |NotSupportScalingPolicy.NodePoolConfig |The specified nodepool config does not support scaling policy. |The specified node pool configurations do not support scaling policies. Specify the parameter and try again. |
|400 |LimitExceeded.MaximumScalingPolicies |You have reached the limit of the number of scaling policies that you can create. |The number of scaling policies that can be created exceeds the upper limit. You can create at most 10 scaling rules per node pool. |
|400 |LaunchTimeMismatch.StartDeliveryTime |The specified StartDeliveryTime and LaunchTime are mismatched. |The specified delivery start time does not match the job trigger time. |
|400 |LaunchTimeMismatch.EndDeliveryTime |The specified EndDeliveryTime and LaunchTime are mismatched. |The specified delivery end time does not match the scheduled order submission time. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |StartDeliveryTimeMismatch.EndDeliveryTime |The specified EndDeliveryTime and StartDeliveryTime are mismatched. |The specified delivery end time does not match the delivery start time. The interval between the two time points must be 10 minutes. Specify the parameter and try again. |
|400 |LimitExceeded.AdjustmentValue |You have reached the limit on the size of AdjustmentValue. |The AdjustmentValue value of scaling exceeds the upper limit. Specify the parameter and try again. |
|400 |EndDeliveryTimeMismatch.AutoReleaseTime |The specified EndDeliveryTime and AutoReleaseTime are mismatched. |The specified automatic release time does not match the delivery end time. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |LaunchTimeMismatch.AutoReleaseTime |The specified AutoReleaseTime and LaunchTime are mismatched. |The specified automatic release time does not match the scheduled order submission time. Specify appropriate parameter values based on the parameter descriptions and try again. |
|400 |InvalidRegionForScheduledInstance.Unsupported |The specified region does not support scheduled instance. |The specified region does not support ESIs. For details on supported regions, see [ESI overview](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview). |
|409 |Conflict.Name |The specified name conflicts with existing {{resourceType}}. |A resource with the same name exists in the specified node pool. Update the resource name and try again later. |
