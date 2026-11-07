---
title: "DescribeScenarios"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/DescribeScenarios"
---

Get scenario configurations.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required? |Example value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeScenarios |Operation to execute: DescribeScenarios. |
|Version |String |Yes |2023\-01\-01 |API version, value: 2023\-01\-01. |
|Id |String |No |general |Scenario ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameter |Type |Example value |Description |
|---|---|---|---|
|Scenarios |Array of Object |\- |Scene list. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DescribeScenarios&Version=2023-01-01 HTTP/1.1
Host:  
Content-Type: application/json; charset=UTF-8
X-Date: 20251216T115151Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251216/cn-beijing/escloud_test/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "20251216195157079151019168F36988",
    "Action": "DescribeScenarios",
    "Version": "2023-01-01",
    "Service": "escloud_test",
    "Region": "cn-beijing"
  },
  "Result": {
    "Scenarios": [
      {
        "Id": "vector",
        "Name": "向量搜索",
        "Description": "xxxxxx",
        "SupportedKernelMajorVersions": [
          "wodbc"
        ],
        "AvailableResourceSpecs": [
          {
            "ResourceSpecNames": [
              "BIWmUNITu"
            ],
            "Type": "Master"
          }
        ]
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|200 |Unauthorized |unauthorized error |User lacks permission to call the interface. |
|200 |IllegalParameter |illegal parameter |Invalid parameter. The reason may be a missing parameter or noncompliance with API requirements. |
|200 |InternalServerError |Internal server exception |The service exited due to an exception and cannot complete the interface request operation. |
