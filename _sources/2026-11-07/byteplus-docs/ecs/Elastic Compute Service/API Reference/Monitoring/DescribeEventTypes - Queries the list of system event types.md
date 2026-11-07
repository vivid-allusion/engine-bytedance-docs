---
title: "DescribeEventTypes - Queries the list of system event types"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeEventTypes"
---

Call the DescribeEventTypes operation to query the list of event types.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeEventTypes&groupName=%E7%9B%91%E6%8E%A7&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|ftxDHw">必选</span> `Sample value: DescribeEventTypes`

The action that you want to perform. Value: DescribeEventTypes.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|zpxM97">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ImpactLevel** <span data-label="purple">string</span> `Optional` `Sample value: Info - information`

The system event level. Value:


* Critical \- severe level

* Warning \- warning level

* Info \- information



**Kind** <span data-label="purple">string</span> `Optional` `Sample value: StateChange`

The system event category. Value:


* UnexpectedOperations: unexpected O&M event

* PlannedOperations: scheduled O&M event

* StateChange: status change event

* BalanceWarning: fee warning event

* TaskStatus: task status type event



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 20`

The number of entries returned on each page in a pagination query.


* Maximum value: 100

* Default value: 100



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**ResponseRequired** <span data-label="purple">boolean</span> `Optional` `Sample value: false`

Indicates whether a response is required. Value:


* true: Required.

* false (default): Not Required.



**Types.N** <span data-label="purple">string[]</span> `Optional` `Sample value: Types.1=DiskError_Redeploy&Types.2=CreateInstance`

The system event type. A maximum of 100 types is supported.


* Argument \- N: specifies the serial number of the event type.

* Separate multiple event types with &.

* Value:

   * SystemFailure_Stop: Stopped instance due to system failure.

   * SystemFailure_Reboot: Restarted instance due to system failure.

   * DiskError_Redeploy: Redeployed instance due to hard disk exception.

   * GpuError_Redeploy: Redeployed instance due to GPU exception.

   * SystemMaintenance_Redeploy: Redeployed instance due to system maintenance.

   * SystemMaintenance_StopAndRepair: Stopped instance with the system under maintenance.

   * SystemFailure_Repair: The system is under maintenance due to an exception.

   * SystemFailure_Redeploy: Redeployed instance due to system failure.

   * CreateInstance: Indicates instance creation.

   * RunInstance: Indicates instance start.

   * StopInstance: Indicates instance stop.

   * DeleteInstance: Indicates instance deletion.

   * SpotInstanceInterruption_Delete: Spot instance interrupted, instance released.

   * AccountUnbalanced_Stop: Instance stopped due to account arrears.

   * AccountUnbalanced_Delete: Account arrears, instance released.

   * InstanceChargeType_Change: The instance billing type is changed.

   * InstanceConfiguration_Change: The instance configuration is changed.

   * FileSystemReadOnly_Change: The file system becomes read\-only.

   * RebootInstance: Indicates instance restart.

   * InstanceFailure: Instance exception due to operating system errors.

   * ApplicationFailure: Application exception.

   * DeploymentSet_Modify: Instance deployment set is modified.

   * ServerMigrationTask: Server migration task.

   * ServerMigration_FirstSync: Server migration, full data synchronization.

   * ServerMigration_AdditionalSync: Server migration, incremental data synchronization.

   * GpuRiskDetected: GPU risk detected.

   * ElasticScheduledInstance_Create: ESI order creation.

   * ElasticScheduledInstance_Cancel: ESI order cancellation.

   * ElasticScheduledInstance_Deliver: ESI order delivery.

   * ElasticScheduledInstance_AutoRelease: Auto release of ESI.

   * ElasticScheduledInstance_Invalid: Invalid ESI order.

   * InfrastructureUpgrade_Redeploy: Instance redeployment due to infrastructure upgrade.

   * DiskErrorDetected: Hard disk error.

   * DiskError_ReplaceDisk: Hard disk replacement due to exception.

   * InstanceOOM: Instance memory OOM.

   * MemoryRiskDetected: Memory risk detected.

   * InstanceFileSystemFailure_StopAndRepair: Downtime repair of instance due to file system exception.

   * InstanceDiskStalled: Instance exception due to degraded volume performance.

   * SystemMaintenance_ReserveAndRepair: Instance downtime repair due to system maintenance.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**EventTypes** <span data-label="purple">object[]</span> `Sample value: --`

Information about the instance system event.


**ImpactLevel** <span data-label="purple">string</span> `Sample value: Info - information`

The system event level.



**Kind** <span data-label="purple">string</span> `Sample value: UnexpectedOperations`

The system event category.



**ResponseRequired** <span data-label="purple">boolean</span> `Sample value: false`

Indicates whether a response is required



**Status** <span data-label="purple">string[]</span> `Sample value: ["Executing", "Succeeded", "Failed"]`

The system event status.



**Title** <span data-label="purple">string</span> `Sample value: Hard disk failure caused instance redeployment`

The description of the system event.



**Type** <span data-label="purple">string</span> `Sample value: DiskError_Redeploy`

The system event type.




**NextToken** <span data-label="purple">string</span> `Sample value: 3tiegs1y963vj0******`

The query credentials value returned by this call. If null is returned, this page is the last page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeEventTypes&Version=2020-04-01&Types.1=DiskError_Redeploy&Types.2=CreateInstance HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202106111445100102252431000052****",
    "Action": "DescribeEventTypes",
    "Version": "2020-04-01",
    "Service": "ecs",
    "Region": "cn-beijing"
  },
  "Result": {
    "EventTypes": [
      {
        "Type": "DiskError_Redeploy",
        "Kind": "UnexpectedOperations",
        "Status": [
          "Executing",
          "Succeeded",
          "Failed"
        ],
        "ResponseRequired": "true",
        "Title": "Hard drive is abnormal, instance redeployed"
      },
      {
        "Type": "CreateInstance",
        "Kind": "StateChange",
        "Status": [
          "Executing",
          "Succeeded",
          "Failed"
        ],
        "ResponseRequired": "false",
        "Title": "Create Instance"
      }
    ],
    "NextToken": ""
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidKind.Malformed |The specified Kind is malformed. |The specified value of Kind is invalid. |
|400 |InvalidTypes.Malformed |The specified Types is malformed. |A specified type is invalid. |
|400 |LimitExceeded.MaximumTypes |You've reached the limit on the number of Types that you can set. |The number of specified types exceeds the limit. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
