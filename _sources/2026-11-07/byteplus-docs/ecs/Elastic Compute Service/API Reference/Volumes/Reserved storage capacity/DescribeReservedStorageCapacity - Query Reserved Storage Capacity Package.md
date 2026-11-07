---
title: "DescribeReservedStorageCapacity - Query Reserved Storage Capacity Package"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Describereservedstoragecapacity"
---

Call the DescribeReservedStorageCapacity interface to query Reserved Storage Capacity information.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeReservedStorageCapacity&groupName=RSC&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Below are the request parameters specific to this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|ZsJhzm">必选</span> `Example value: DescribeReservedStorageCapacity`

The action to be performed: DescribeReservedStorageCapacity.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|DlIfOa">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**ReservedStorageCapacityName ** <span data-label="purple">string </span>`Optional` `Example value: cn-beijing-a`

Name of the reserved storage capacity package.



**ZoneId ** <span data-label="purple">string </span>`Optional` `Example value: cn-xxx-a`

The availability zone where the reserved storage capacity package is located.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default region for the reserved storage capacity package is the Region specified in the request, i.e., the Region in the Header.</div>




**VolumeType ** <span data-label="purple">string </span>`Optional` `Example value: ESSD_PL0`

Specifications for the reserved storage capacity in cloud volumes, are defined as follows:


* ESSD_PL0: Extreme\-Speed SSD volume, PL0 specification

* ESSD_FlexPL: Extreme\-Speed SSD volume, FlexPL specification



**Status ** <span data-label="purple">string </span>`Optional` `Example value: available`

Description of the status of the Reserved Storage Capacity Package:


* creating: In creation

* available: In effect

* terminated: Expired



**PageNumber ** <span data-label="purple">string </span>`Optional` `Example: 1`

Page number for queries.



**PageSize ** <span data-label="purple">string </span>`Optional` `Example value: 100`

Number of rows per page set during pagination querying.



**ReservedStorageCapacityIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|di4Zet">必选</span> `Example value: rsc-3vpnts78dk3x35cj****`

Reserved storage capacity package ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

The parameters listed below are unique to this API. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">integer </span>`Example: 100`

Number of rows per page.



**PageNumber ** <span data-label="purple">integer </span>`Example value: 1`

Current page number.



**TotalCount ** <span data-label="purple">integer </span>`Example value: 5`

Number of Reserved Storage Capacity Packages.



**RscInfo ** <span data-label="purple">object[] </span>`Example value: -`

Information about the Reserved Storage Capacity Package.


**Id ** <span data-label="purple">string</span> Example: rsc\-3vpnts78dk3x35cj\*\*\*\*

`

Reserved storage capacity package ID.



**Name ** <span data-label="purple">string </span>`Example: rsc01`

Name of the reserved storage capacity package.



**ZoneId ** <span data-label="purple">string </span>`Example: cn-beijing-a`

Reserved storage capacity package's availability zone.



**Type ** <span data-label="purple">string </span>`Example value: ESSD_PL0`

Specifications for the reserved storage capacity in cloud volumes, are defined as follows:


* ESSD_PL0: Extreme\-Speed SSD volume, PL0 specification

* ESSD_FlexPL: Extreme\-Speed SSD volume, FlexPL specification



**AccountId ** <span data-label="purple">string </span>`Example: 21000****`

Account ID associated with the reserved storage capacity package.



**Status ** <span data-label="purple">string </span>`Example value: available`

Description of the status of the Reserved Storage Capacity Package:


* creating: In creation

* available: In effect

* terminated: Expired



**TakeEffectTime ** <span data-label="purple">string </span>`Example value: 2024-06-24T14:00:00+08:00`

Activation time for the reserved storage capacity package.



**ExpiredTime ** <span data-label="purple">string </span>`Example value: 2024-07-24T23:59:59+08:00`

Expiration time of the reserved storage capacity package.



**Size ** <span data-label="purple">long </span>`Example value: 600`

Capacity of the Reserved Storage Capacity Package.



**RemainingSize ** <span data-label="purple">integer </span>`Example value: 50`

The unused proportion of the reserved storage capacity is calculated by the used duration divided by the total purchased duration.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=DescribeReservedStorageCapacity&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```text
{
    "ResponseMetadata": {
        "RequestId": "ca07101e-d33a-4e38-8240-cfcf10dc****",
        "Action": "DescribeReservedStorageCapacity",
        "Version": "2020-04-01",
        "Service": "EBS",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 15,
        "RscInfo": [
            {
                "AccountId": "21000****",
                "ExpiredTime": "2024-08-04T23:59:59+08:00",
                "Id": "rsc-3vpnts78dk3x35cj****",
                "LoseEffectTime": "",
                "Name": "zgl-test",
                "RemainingSize": 100,
                "Size": 40,
                "Status": "available",
                "TakeEffectTime": "2024-07-04T16:00:00+08:00",
                "Type": "ESSD_PL0",
                "ZoneId": "cn-xxx-a"
            }
        ],
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to the business logic of this API. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidRequest |The operation is not permitted due to the request is invalid. |Invalid request. |
|404 |InstanceNotFound |Instance not found. |The instance does not exist. |
