---
title: "DescribeScheduledInstanceStock - Queries the reservation status of Elastic Scheduled Instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeScheduledInstanceStock"
---

Call the DescribeScheduledInstanceStock operation to query the available reservation time slots for Elastic Scheduled Instances (ESIs).

<span id=".6K-35rGC6K-05piO"></span>
## Request description

Currently, this operation only returns reservation status based on the resource delivery time period. The following table describes the return value.


|Return field |Reservation status |ESI ([Elastic Scheduled Instance](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview)) |
|---|---|---|
|Status (stock reservation status) |AVAILABLE |This time slot is not fully booked and is available for reservation. Call the [DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) operation to check whether instance stock is sufficient. |
||NOT_AVAILABLE |This time slot is fully booked and unavailable for reservation. Select another time slot. |
|ReleaseStatus (release reservation status) |AVAILABLE |No automatic release is involved. The return value is empty. |
||NOT_AVAILABLE ||


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeScheduledInstanceStock&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|J2Gm6C">必选</span> `Sample value: DescribeScheduledInstanceStock`

The operation that you want to perform. Valid value: DescribeScheduledInstanceStock.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|2uWPt1">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**DeliveryType** <span data-label="purple">string</span> `Optional` `Sample value: Reserve`

The delivery type of Elastic Scheduled Instances\-Segmented. Valid values:


* Reserve (default): Scheduled delivery

* Immediate: Immediate delivery


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>ElasticScheduledInstanceType</code> is set to <code>Segmented</code>, this parameter takes effect.</div>


* <div data-tips="true" data-tips-type="tip">This feature is currently in Beta. If you need a trial, contact the account manager to apply.</div>




**ElasticScheduledInstanceType** <span data-label="purple">string</span> `Optional` `Sample value: Esi`

The ESI type. Value:


* Esi (default): Elastic Scheduled Instances (ESI)

* Segmented: Elastic Scheduled Instances\-Segmented


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in Beta. If you need a trial, contact the account manager to apply.</div>




**InstanceTypeId** <span data-label="purple">string</span> `Optional` `Sample value: ecs.g3i.xlarge`

Instance type.

When `ElasticScheduledInstanceType` is set to `Segmented`, this parameter is required. This parameter specifies that the reservation and stock status of Elastic Scheduled Instances\-Segmented with the current instance type are queried.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in Beta. If you need a trial, contact the account manager to apply.</div>




**VolumeType** <span data-label="purple">string</span> `Optional` `Sample value: ESSD_PL0`

Specify the volume type to query. Valid values:


* ESSD_PL0: ESSD PL0

* ESSD_FlexPL: ESSD FlexPL



**ZoneId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing-a`

The ID of the availability zone where the instance is located.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in the same region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>ElasticScheduledInstanceType</code> is set to <code>Segmented</code>, this parameter is required.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**ScheduledInstanceStock** <span data-label="purple">object[]</span> `Sample value: --`

The information about the reservation that meets the conditions.


**ReleaseStatus** <span data-label="purple">string</span> `Sample value: AVAILABLE`

The release reservation status for the current time period. Valid values:


* AVAILABLE: Not fully booked. Reservation is allowed.

* NOT_AVAILABLE: Fully booked. Select another time period for reservation.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the value of <code>ElasticScheduledInstanceType</code> is <code>Esi</code>, the return value of this parameter is empty.</div>




**EndDeliveryAt** <span data-label="purple">string</span> `Sample value: 2024-01-04T18:30:00+08:00`

The end time for instance delivery.



**StartDeliveryAt** <span data-label="purple">string</span> `Sample value: 2024-01-04T18:20:00+08:00`

The start time for instance delivery.



**Status** <span data-label="purple">string</span> `Sample value: AVAILABLE`

The reservation status of stock for the current time period. Valid values:


* AVAILABLE: Not fully booked. Reservation is allowed.

   * If the value of `ElasticScheduledInstanceType` is `Esi`, you also need to call [DescribeAvailableResource](https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource) to query whether the instance stock is sufficient.

   * If the value of `ElasticScheduledInstanceType` is `Segmented`, whether a reservation can be made successfully when an order is placed also depends on the actual automatic release time selected.

* NOT_AVAILABLE: Fully booked. Select another time period for reservation.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeScheduledInstanceStock&Version=2020-04-01&ElasticScheduledInstanceType=Segmented&InstanceTypeId=ecs.g3i.xlarge&ZoneId=cn-beijing-a&VolumeType=ESSD_PL0 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202401041812061F86A29C5B0D3267****",
    "Action": "DescribeScheduledInstanceStock",
    "Version": "2020-04-01",
    "Service": "ecs",
    "Region": "cn-beijing"
  },
  "Result": {
    "ScheduledInstanceStock": [
      {
        "StartDeliveryAt": "2024-01-04T18:20:00+08:00",
        "EndDeliveryAt": "2024-01-04T18:30:00+08:00",
        "Status": "AVAILABLE",
        "ReleaseStatus": "AVAILABLE"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidDeliveryType.Malformed |The specified DeliveryType is malformed. |The specified delivery type is invalid. |
|400 |InvalidElasticScheduledInstanceType.Malformed |The specified ElasticScheduledInstanceType is malformed. |The specified ESI type is invalid. |
|400 |InvalidInstanceTypeId.Malformed |The specified InstanceTypeId is malformed. |The specified instance type ID is invalid. |
|400 |InvalidVolumeType.Malformed |The specified VolumeType is malformed. |The specified volume type is invalid. |
|400 |InvalidZoneId.Malformed |The specified ZoneId is malformed. |The specified availability zone ID is invalid. |
|404 |InvalidInstanceType.NotFound |The specified InstanceType does not exist. |The specified instance type does not exist. |
|404 |InvalidZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
