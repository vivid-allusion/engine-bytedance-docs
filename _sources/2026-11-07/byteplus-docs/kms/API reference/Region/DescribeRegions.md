---
title: "DescribeRegions"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/DescribeRegions"
---

You can call the DescribeRegions API to query all regions that support the Key Management Service (KMS).

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=DescribeRegions&groupName=%E5%9C%B0%E5%9F%9F%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeRegions |The action you want to perform. Set the value to **DescribeRegions**. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|Regions |Array of Object |The data of the RegionInfo structure |The returned regions. |


<span id="request-example"></span>
## Request example

```text
GET /?Action=DescribeRegions&Version=2021-02-18 HTTP/1.1
Host: kms.byteplusapi.com
X-Date: 20240711T062123Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240711/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240711142138236180204047F6308E",
    "Action": "DescribeRegions",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "Regions": [
      {
        "RegionId": "cn-beijing"
      }
    ]
  }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes of the current API related to business logic. For common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|HttpCode |Error Code |Error Message |Description |
|---|---|---|---|
|403 |Reject.Throttling.Action |The request of Action: %s upper limit is exceeded. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
