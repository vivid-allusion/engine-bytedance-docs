---
title: "DescribeRegions - Query available Region list"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/DescribeRegions_-_Query_available_Region_list"
---

Call the DescribeRegions API to view the list of Regions.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This API limits requests to **100 times/second**. The per\-user request frequency limit is **20 times/second**.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeRegions&groupName=%E8%B5%84%E6%BA%90%E6%A3%80%E6%9F%A5&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|VNgbZL">必选</span> `Example value: DescribeRegions`

The action to perform, value: DescribeRegions.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|zJkESj">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the unique response parameters of this API are listed below. For more details, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Regions** <span data-label="purple">object[]</span> `Example value: /`

List of regions.


**RegionId** <span data-label="purple">string</span> `Example value: cn-shanghai`

Region ID.



**RegionName** <span data-label="purple">string</span> `Example value: cn-shanghai`

Region name.



**Description** <span data-label="purple">string</span> `Example: East China 2 (Shanghai)`

Region name (Chinese).



**Status** <span data-label="purple">string</span> `Example value: Available`

Region status.


* Available: enabled. You can view, create, and manage resources in this region.

* Unavailable: disabled.

   You cannot activate new services or purchase new products in a disabled region. Activated services will continue to be supported until they expire.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DescribeRegions&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********
{}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "20241101141727988C2AA36F88978689CB-18905c",
    "Action": "DescribeRegions",
    "Version": "2022-01-01",
    "Service": "RabbitMQ",
    "Region": "cn-shanghai"
  },
  "Result": {
    "Regions": [
      {
        "Description": "China (Shanghai)",
        "RegionId": "cn-shanghai",
        "RegionName": "cn-shanghai",
        "Status": "Available"
      },
      {
        "Description": "China (Beijing)",
        "RegionId": "cn-beijing",
        "RegionName": "cn-beijing",
        "Status": "Available"
      },
      {
        "Description": "China (Guangzhou)",
        "RegionId": "cn-guangzhou",
        "RegionName": "cn-guangzhou",
        "Status": "Available"
      },
      {
        "Description": "Asia Pacific (Johor)",
        "RegionId": "ap-southeast-1",
        "RegionName": "ap-southeast-1",
        "Status": "Available"
      }
    ]
  }
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists error codes related to this interface and business logic. Refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) section for common error codes.


|Status code |Error code |Error message |Specifications |
|---|---|---|---|
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |You do not have the required permissions. Authorize or switch accounts and try again. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
