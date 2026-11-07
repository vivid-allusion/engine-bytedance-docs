---
title: "DescribeSystemEvents - Queries system events"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents"
---

Call the DescribeSystemEvents operation to query system events of an instance.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

For operation instructions and precautions, refer to [Querying and handling events](https://docs.byteplus.com/en/docs/ecs/Querying-and-handling-events?TagIDs=2,87,70,69).

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSystemEvents&groupName=%E7%9B%91%E6%8E%A7&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|65ojfz">必选</span> `Sample value: DescribeSystemEvents`

The action that you want to perform. Value: DescribeSystemEvents.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|42jQbM">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**Category** <span data-label="purple">string</span> `Optional` `Sample value: ResourceEvent`

The system event category. Value:


* ResourceEvent: resource\-targeted event

* TaskEvent: task\-related event



**CreatedAtEnd** <span data-label="purple">string</span> `Optional` `Sample value: 2021-06-29T18:11:46+08:00`

Filters events created before the time specified for CreatedAtEnd. Default value: current time. Format: RFC3339.



**CreatedAtStart** <span data-label="purple">string</span> `Optional` `Sample value: 2021-06-28T18:29:38+08:00`

Filters events created after the time specified for CreatedAtStart. The default value is 24h before the time specified for CreatedAtEnd (see the part of the request parameter CreatedAtEnd). Format: RCF3339.



**EventIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: EventIds.1=e-3ti9101aju3vj0******&EventIds.2=e-r4911sfaa9ts******`

The event ID. A maximum of 100 event IDs are supported. You can use the [event notification](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications) feature or call this operation to query and obtain the event ID.


* Argument \- N: specifies the serial number of the event.

* Separate multiple event IDs with `&`.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 20`

The number of entries per page.


* Maximum value: 100

* Minimum value: 0

* Default value: 20



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: --`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the `NextToken` parameter to the value returned by the previous API call.



**ResourceIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: ResourceIds.1=i-3ti9101aju3vj0******&ResourceIds.2=i-tws01a56ydh0******`

The resource ID. A maximum of 100 resource IDs are supported. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation to query the instance ID.


* Argument \- N: specifies the serial number of the resource.

* Separate multiple resource IDs with `&`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the supported resource type is ECS instances.</div>




**Status.N** <span data-label="purple">string[]</span> `Optional` `Sample value: Status.1=Executing&Status.2=Inquiring`

The status of the system event. Up to 10 statuses are supported.


* Argument \- N: specifies the serial number of the event type.

* Separate multiple event types with `&`.

* Value:

   * UnknownStatus: unknown status

   * Executing: in progress

   * Succeeded: successful execution

   * Failed: failed execution

   * Inquiring: pending response

   * Scheduled: scheduled execution

   * Rejected: execution refused by the user

   * Cancelled: cancelled

   * Pending: suspended

   * Recovered: restored



**Types.N** <span data-label="purple">string[]</span> `Optional` `Sample value: Types.1=SystemFailure_Reboot&Types.2=DiskError_Redeploy`

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

   * SystemFailure_Redeploy: Redeployed instance due to system failure.

   * SystemFailure_Repair: System under maintenance due to exception.

   * CreateInstance: Indicates instance creation.

   * RunInstance: Indicates instance start.

   * StopInstance: Indicates instance shutdown.

   * DeleteInstance: Indicates instance deletion.

   * SpotInstanceInterruption_Delete: Spot instance interrupted, instance released.

   * AccountUnbalanced_Stop: Instance shutdown due to account arrears.

   * AccountUnbalanced_Delete: Instance release due to account arrears.

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

   * ElasticScheduledInstance_Create: Creation of ESI order.

   * ElasticScheduledInstance_Cancel: Cancellation of ESI order.

   * ElasticScheduledInstance_Deliver: Delivery of ESI order.

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



**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RC******`

The query credentials value returned by this call. If null is returned, this page is the last page.



**SystemEvents** <span data-label="purple">object[]</span> `Sample value: --`

Information about the instance system event.


**Category** <span data-label="purple">string</span> `Sample value: ResourceEvent`

The event category.



**CreatedAt** <span data-label="purple">string</span> `Sample value: 2022-08-29T18:11:46+08:00`

The creation time of the system event.



**ExtraInfo** <span data-label="purple">object</span> `Sample value: {"VolumeId": "vol-3tiegs1y963vj***","Serial": "ysw2flxa****"}`

The additional information about the system event.



**Id** <span data-label="purple">string</span> `Sample value: e-3tiegs1y963vj0******`

The system event ID.



**ImpactLevel** <span data-label="purple">string</span> `Sample value: Info - information`

The system event level. Value:


* Critical \- severe level

* Warning \- warning level

* Info \- information



**OperatedEndAt** <span data-label="purple">string</span> `Sample value: 2022-08-30T15:11:46+08:00`

The end time of the O&M time window.



**OperatedStartAt** <span data-label="purple">string</span> `Sample value: 2022-09-10T18:11:46+08:00`

The start time of the O&M time window.



**ResourceId** <span data-label="purple">string</span> `Sample value: i-3tiegs1y963vj0******`

The resource ID.



**Status** <span data-label="purple">string</span> `Sample value: Executing`

The system event status.



**Type** <span data-label="purple">string</span> `Sample value: SystemFailure_Stop`

The system event type.



**UpdatedAt** <span data-label="purple">string</span> `Sample value: 2022-08-30T18:11:46+08:00`

The update time of the system event.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeSystemEvents&Version=2020-04-01&EventIds.1=e-3ti9101aju3vj0****** HTTP/1.1
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
    "Action": "DescribeSystemEvents",
    "Version": "2020-04-01",
    "Service": "ecs",
    "Region": "cn-beijing"
  },
  "Result": {
    "SystemEvents": [
      {
        "Id": "e-3ti9101aju3vj0******",
        "Category": "ResourceEvent",
        "CreatedAt": "2022-06-15T16:34:34+08:00",
        "UpdatedAt": "2022-06-15T16:34:49+08:00",
        "ResourceId": "i-3ti9101aju3vj0******",
        "Type": "DiskError_Redeploy",
        "Status": "Succeeded",
        "OperatedStartAt": "2022-08-30T15:11:46+08:00",
        "OperatedEndAt": "2022-09-10T18:11:46+08:00",
        "ExtraInfo": {
          "Serial": "ysw2flxa****",
          "VolumeId": "vol-3tiegs1y963vj0******"
        }
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
|400 |InvalidCategory.Malformed |The specified Category is malformed. |The specified value of Category is invalid. |
|400 |InvalidCreatedAtEnd.Malformed |The specified CreatedAtEnd is malformed. |The end time specified for CreatedAtEnd is invalid. |
|400 |InvalidCreatedAtStart.Malformed |The specified CreatedAtStart is malformed. |The specified creation time is invalid. |
|400 |InvalidResourceIds.Malformed |The specified ResourceIds is malformed. |The specified value of ResourceIds is invalid. |
|400 |InvalidStatus.Malformed |The specified Status is malformed. |The specified value of Status is invalid. |
|400 |InvalidTypes.Malformed |The specified Types is malformed. |A specified type is invalid. |
|400 |LimitExceeded.MaximumEventIds |You've reached the limit on the number of EventIds that you can set. |The specified number of event IDs exceeds the limit. |
|400 |LimitExceeded.MaximumMaxResults |The number of specified MaxResults exceeds the maximum limit. |The value specified for MaxResults exceeds the upper limit. |
|400 |LimitExceeded.MaximumResourceIds |You've reached the limit on the number of ResourceIds that you can set. |The specified number of resource IDs exceeds the limit. |
|400 |LimitExceeded.MaximumStatus |You've reached the limit on the number of Status that you can set. |The specified number of statuses exceeds the limit. |
|400 |LimitExceeded.MaximumTypes |You've reached the limit on the number of Types that you can set. |The number of specified types exceeds the limit. |
|400 |LimitExceeded.MinimumMaxResults |The number of specified MaxResults exceeds the minimum limit. |The value specified for MaxResults exceeds the lower limit. |
|404 |InvalidActionOrVersion |Could not find operation %s for version %s. |The operation does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
