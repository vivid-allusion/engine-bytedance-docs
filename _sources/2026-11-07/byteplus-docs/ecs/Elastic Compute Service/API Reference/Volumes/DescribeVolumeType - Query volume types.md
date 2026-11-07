---
title: "DescribeVolumeType - Query volume types"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Describevolumetype"
---

Call the DescribeVolumeType API to query the volume types supported for creation in different regions and availability zones

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeVolumeType&groupName=%E4%BA%91%E7%9B%98&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only the unique request parameters and some common parameters for this API are listed below For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|uSwZav">必选</span> `Example value: DescribeVolumeType`

Operation to perform: DescribeVolumeType.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|DajwQX">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**ZoneId ** <span data-label="purple">string </span>`Optional` `Example: ap-southeast-1-a`

Available zone ID.



**VolumeTypeIds.N ** <span data-label="purple">string[] </span>`Optional` `Example: VolumeTypeIds.1=ESSD_PL0`

Types of volumes to query. Usage details are as follows:


* PTSSD: Performance SSD.

* ESSD_PL0: High\-speed SSD volume of PL0 specification.

* Extreme Speed SSD Cloud volume, FlexPL specification.

* TSSD_TL0: Throughput SSD volume.

   All volume types are queried by default.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed information on volume specifications, see <a href="https://docs.byteplus.com/en/docs/ecs/Volume-specifications">volume specifications</a>.</div>




**PageNumber ** <span data-label="purple">integer </span>`Optional` `Example value: 1`

Starting page number, default is 1.



**PageSize ** <span data-label="purple">integer </span>`Optional` `Example value: 20`

Page size, up to 100. Default is 50.



**Filter ** <span data-label="purple">string </span>`Optional` `Example: /`

Filter. This parameter is deprecated. Do not use it.



**OrderBy ** <span data-label="purple">string </span>`Optional` `Example value: /`

Sort. This parameter is deprecated. Do not use it.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

Only the unique response parameters for this API are listed below For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

Page Size.



**PageNumber ** <span data-label="purple">integer </span>`Example value: 1`

Starting page number, default is 1.



**TotalCount ** <span data-label="purple">integer </span>`Example value: 2`

Total number of eligible volume types.



**VolumeTypes ** <span data-label="purple">object[] </span>`Example value: -`

Volume information that meets the criteria.


**Id ** <span data-label="purple">string </span>`Example value: ESSD_FlexPL`

The volume type to be queried. Here are the value details:


* PTSSD: Performance SSD.

* ESSD_PL0: High\-speed SSD volume of PL0 specification.

* Extreme Speed SSD Cloud volume, FlexPL specification.

* TSSD_TL0: Throughput\-type SSD volume.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about volume specifications, see <a href="https://docs.byteplus.com/en/docs/ecs/Volume-specifications">Volume Specifications</a>.</div>




**Zones ** <span data-label="purple">string[] </span>`Example value: g    cn-beijing-a`

The available zone for this volume type.



**ExtraPerformanceTypes ** <span data-label="purple">object[] </span>`Example value: -`

Additional performance information.


**Id ** <span data-label="purple">string </span>`Example: IOPS`

Additional performance type, with the following options:


* Balance: Balanced additional performance.

* IOPS: IOPS additional performance.

* Throughput: Throughput additional performance.



**MaxIops ** <span data-label="purple">string </span>`Example value: 1`

The maximum IOPS supported by this volume specification.



**MaxThroughput ** <span data-label="purple">string </span>`Example value: 1`

Maximum bandwidth supported by this volume specification.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=DescribeVolumeType&Version=2020-04-01&VolumeTypeIds.1=ESSD_FlexPL HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
    "ResponseMetadata": {
        "RequestId": "20240401115223DABE6F7F7C4EA281****,
        "Action": "DescribeVolumeType",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 99,
        "TotalCount": 1,
        "VolumeTypes": [
           {
                "Id": "ESSD_PL0",
                "Zones": [
                    "ap-southeast-1-a",
                    "ap-southeast-1-b",
                    "ap-southeast-1-c"
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this interface and business logic. For public error codes, see the [Public Error Code](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status Code |error code |error message |Create Volume |
|---|---|---|---|
|500 |InternalError |An internal error has occurred. |Internal error. Try again. If you fail after multiple attempts, submit a ticket. |
