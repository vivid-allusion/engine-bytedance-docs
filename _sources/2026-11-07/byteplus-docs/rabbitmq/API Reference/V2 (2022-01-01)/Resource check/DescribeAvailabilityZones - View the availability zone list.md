---
title: "DescribeAvailabilityZones - View the availability zone list"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/DescribeAvailabilityZones_-_View_the_availability_zone_list"
---

Call the DescribeAvailabilityZones API to view the availability zone list.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This API limits requests to **100 times/second**; the per\-user request frequency limit is **20 times/second**.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeAvailabilityZones&groupName=%E8%B5%84%E6%BA%90%E6%A3%80%E6%9F%A5&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|Un5lq6">必选</span> `Example value: DescribeAvailabilityZones`

Actions to execute, value: DescribeAvailabilityZones.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|6wsXDc">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**RegionId** <span data-label="purple">string</span> `Optional` `Example value: cn-beijing`

Region ID, queryable via [DescribeRegions](https://docs.byteplus.com/en/docs/rabbitmq/DescribeRegions_-_Query_available_Region_list)



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the unique response parameters of this API are listed below. For more details, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RegionId** <span data-label="purple">string</span> `Example value: cn-beijing`

Region ID.



**Zones** <span data-label="purple">object[]</span> `Example value: /`

availability zone list.


**ZoneId** <span data-label="purple">string</span> `Example value: cn-beijing-a`

availability zone ID



**ZoneName** <span data-label="purple">string</span> `Example value: availability zone A`

availability zone name.



**Status** <span data-label="purple">string</span> `Example value: Normal`

Availability zone status includes the following states:


* Normal: available for sale.

* Soldout: sold out.

* Unavailable: disabled.

   You can not activate new services or purchase new products in a disabled availability zone. Activated services will continue to be supported until they expire.



**Description** <span data-label="purple">string</span> `Example value: availability zone A`

Region availability zone Chinese name.



**ZoneStatus** <span data-label="purple">string</span> `Example value: Normal`

Status of the availability zone, including the following states:


* Normal: available for sale.

* Soldout: sold out.

* Unavailable: disabled.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You cannot activate new services or purchase new products in a disabled availability zone. Activated services will continue to be supported until they expire.   </div>
   




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=DescribeAvailabilityZones&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "RegionId": "cn-beijing"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "20230220220602D15D163D781CC7D82128",
        "Action": "DescribeAvailabilityZones",
        "Version": "2022-01-01",
        "Service": "RabbitMQ",
        "Region": "cn-beijing"
    },
    "Result": {
        "RegionId": "cn-beijing",
        "Zones": [
            {
                "Description": "Availability Zone A",
                "Status": "Normal",
                "ZoneId": "cn-beijing-a",
                "ZoneName": "cn-beijing-a"
            },
            {
                "Description": "Availability Zone B",
                "Status": "Normal",
                "ZoneId": "cn-beijing-b",
                "ZoneName": "cn-beijing-b"
            }
        ]
    }
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists error codes related to this interface and business logic. Refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) section for common error codes.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |You do not have the required permissions. Authorize or switch accounts and try again. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
