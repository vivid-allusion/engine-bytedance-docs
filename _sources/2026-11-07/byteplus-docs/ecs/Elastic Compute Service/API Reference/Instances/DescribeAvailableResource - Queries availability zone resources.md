---
title: "DescribeAvailableResource - Queries availability zone resources"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeAvailableResource"
---

You can call the DescribeAvailableResource operation to query the inventory of computing resources in an availability zone, such as regions and availability zones.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* You can query the inventory status of instance resources in an availability zone when creating an instance ([RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances)) or changing an instance type ([ModifyInstanceSpec](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceSpec)).

* This operation only supports queries of instance types available for sale in the specified availability zone. To query the configuration and performance of instance types, call the [DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) operation.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeAvailableResource&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|puwc2A">必选</span> `Sample value: DescribeAvailableResource`

The action that you want to perform. Value: DescribeAvailableResource.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|UpPmCv">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**DestinationResource** <span data-label="purple">string</span> <span data-api-tag="require|nc2oQP">必选</span> `Sample value: InstanceType`

The type of resource to be queried. Value:


* InstanceType: instance type

* VolumeType: volume type



**ElasticScheduledInstanceType** <span data-label="purple">string</span> `Optional` `Sample value: NoEsi`

The ESI type. Value:


* NoEsi (default): non\-ESI type

* Esi: ESI type

* Segmented: ESI\-Segmented


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>InstanceChargeType</code> is set to <code>PostPaid</code>, this parameter is effective.</div>


* <div data-tips="true" data-tips-type="tip">This feature is currently in Beta. If you need a trial, contact the account manager to apply.</div>




**InstanceChargeType** <span data-label="purple">string</span> `Optional` `Sample value: PostPaid`

Billing method of the instance. Value:


* PostPaid (default): pay\-as\-you\-go

* PrePaid: subscription

* ReservedInstance: Reserved Instances (RI)



**InstanceTypeId** <span data-label="purple">string</span> `Optional` `Sample value: ecs.g3i.large`

Specify the instance type or dedicated host specification to be queried.



**SpotStrategy** <span data-label="purple">string</span> `Optional` `Sample value: NoSpot`

Spot strategy for instance billed in pay\-as\-you\-go mode. Value:


* NoSpot (default): Instances are billed in pay\-as\-you\-go mode.

* SpotAsPriceGo: The system automatically offers a bidding price.​ This bidding price is based on the current market price for spot instances.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>InstanceChargeType</code> is set to <code>PostPaid</code>, this parameter is effective.</div>




**VolumeType** <span data-label="purple">string</span> `Optional` `Sample value: ESSD_PL0`

Specify the queried volume type. Value:


* ESSD_PL0: ESSD PL0

* ESSD_FlexPL: ESSD FlexPL



**ZoneId** <span data-label="purple">string</span> `Optional` `Sample value: cn-beijing-a`

Availability zone ID. You can call the [DescribeZones](https://docs.byteplus.com/en/docs/ecs/DescribeZones) operation to query the availability zones in one region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default value is empty. This indicates that for availability zones in the current region (RegionId), the information of all availability zones that meet conditions is to be returned.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AvailableZones** <span data-label="purple">object[]</span> `Sample value: --`

Information of resources that meet the requirements in the availability zone.


**AvailableResources** <span data-label="purple">object[]</span> `Sample value: --`

Detailed information of resources in the availability zone.


**SupportedResources** <span data-label="purple">object[]</span> `Sample value: --`

Detailed resource information.


**Status** <span data-label="purple">string</span> `Sample value: Available`

Inventory status of specific resources. Value:


* Available: The queried resource is available for sale.

* SoldOut: The queried resource is sold out.



**Value** <span data-label="purple">string</span> `Sample value: ecs.g3i.large`

The resource value. For example, when the resource type is `InstanceType`, this parameter refers to the value of instance type.




**Type** <span data-label="purple">string</span> `Sample value: InstanceType`

Resource type.




**RegionId** <span data-label="purple">string</span> `Sample value: cn-beijing`

ID of the region to which the availability zone belongs.



**Status** <span data-label="purple">string</span> `Sample value: Available`

Inventory status of any resource in the availability zone. This parameter indicates more than just the status of the target resource to be queried. Value:


* Available: The queried resource is available for sale.

* SoldOut: The queried resource is sold out.



**ZoneId** <span data-label="purple">string</span> `Sample value: cn-beijing-a`

Availability zone ID.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeAvailableResource&Version=2020-04-01&DestinationResource=InstanceType&ZoneId=cn-*****&InstanceTypeId=ecs.g2i.large HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeAvailableResource",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "AvailableZones": [{
            "AvailableResources": [{
                "SupportedResources": [{
                    "Status": "Available",
                    "Value": "ecs.g2i.large"
                }],
                "Type": "InstanceType"
             }],
             "RegionId": "cn-beijing",
             "Status": "Available",
             "ZoneId": "cn-beijing-a"
        }]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidDestinationResource |The specified DestinationResource is not valid, is unsupported, or can not be used. |The specified target resource type is invalid. |
|400 |InvalidElasticScheduledInstanceType.Malformed |The specified ElasticScheduledInstanceType is malformed. |The specified ESI type is invalid. |
|400 |InvalidInstanceChargeType |The specified InstanceChargeType is invalid. |The specified instance billing method is invalid. |
|400 |InvalidSpotStrategy |The specified SpotStrategy is invalid. |The specified spot strategy is invalid. |
|400 |InvalidVolumeType.Malformed |The specified VolumeType is malformed. |The specified volume type is invalid. |
|400 |MissingParameter.DestinationResource |The required parameter DestinationResource is not supplied. |The target resource type is not provided. |
|404 |InvalidInstanceType.NotFound |The specified InstanceType does not exist. |The specified instance type does not exist. |
|404 |InvalidZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
