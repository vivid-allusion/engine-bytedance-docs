---
title: "DescribeZones - Querying the ALB supported AZ List"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeZones"
---

Call the DescribeZones API to query the Availability Zones supported by ALB.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 40 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeZones&groupName=%E5%8F%AF%E7%94%A8%E5%8C%BA&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|DuGZwH">必选</span> `Example: DescribeZones`

Action to execute. Set the value to DescribeZones.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|foOVt6">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



**Zones ** <span data-label="purple">object[] </span>`Example: --`

List of availability zones where ALB can be deployed in the current region.


**ZoneType ** <span data-label="purple">string </span>`Example: standard`

Availability zone type.



**ZoneId ** <span data-label="purple">string </span>`Example: cn-beijing-a`

Availability zone.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeZones&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "754222ed-****-****-****-bf1beba4880b",
        "Action": "DescribeZones",
        "Version": "2020-04-01"
    },
    "Result": {
        "RequestId": "754222ed-****-****-****-bf1beba4880b",
        "Zones": [
            {
                "ZoneId": "cn-beijing-a"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
