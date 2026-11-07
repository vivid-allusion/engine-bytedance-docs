---
title: "DescribeNodeAvailableSpecsV2"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/DescribeNodeAvailableSpecsV2"
---

Get node available configuration list (version 2).

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required? |Example value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeNodeAvailableSpecsV2 |Action to execute, value: DescribeNodeAvailableSpecsV2. |
|Version |String |Yes |2023\-01\-01 |API version, value: 2023\-01\-01. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameter |Type |Example value |Description |
|---|---|---|---|
|ConfigurationCode |String |es.standard |Configuration code. |
|NodeAvailableSpecs |Array of Object |\- |Available specifications corresponding to the node. |
|ResourceSpecs |Array of Object |\- |All compute specifications. |
|StorageSpecs |Array of Object |\- |Full storage specifications. |
|NetworkSpecs |Array of Object |\- |All network specifications. |
|AZAvailableSpecsSoldOut |Object |\- |Sold\-out information (deprecated). |
|ZoneSupportSpecList |Array of Object |\- |The specification information corresponding to the Region. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DescribeNodeAvailableSpecsV2&Version=2023-01-01 HTTP/1.1
Host:   
Content-Type: application/json; charset=UTF-8
X-Date: 20251216T115225Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251216/cn-beijing/escloud_test/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "2025121619523007314912220381CDF7",
    "Action": "DescribeNodeAvailableSpecsV2",
    "Version": "2023-01-01",
    "Service": "escloud_test",
    "Region": "cn-beijing"
  },
  "Result": {
    "ConfigurationCode": "es.standard",
    "NodeAvailableSpecs": [
      {
        "ResourceSpecNames": [
          "Us"
        ],
        "StorageSpecNames": [
          "5JNcB"
        ],
        "Type": "Master"
      }
    ],
    "ResourceSpecs": [
      {
        "Description": "Kibana专用-1C2G节点",
        "DisplayName": "1核2GiB",
        "Memory": 2,
        "Name": "kibana.x2.small",
        "CPU": 1
      }
    ],
    "StorageSpecs": [
      {
        "Description": "标准版-高性能云盘-pl0",
        "DisplayName": "ESSD-PL0",
        "MaxSize": 10000,
        "MinSize": 20,
        "Name": "es.volume.essd.pl0",
        "Size": 0,
        "Type": "jBevf",
        "Limit": "单盘 IOPS 基准性能上限 1 万"
      }
    ],
    "NetworkSpecs": [
      {
        "NetworkRole": "Elasticsearch",
        "SpecName": "es.eip.bgp_fixed_bandwidth"
      }
    ],
    "AZAvailableSpecsSoldOut": {},
    "ZoneSupportSpecList": [
      {
        "ZoneName": "cn-guilin-c",
        "SpecNames": [
          "kupQ4oPP"
        ],
        "SoldOutSpecNames": [
          "ccxPlkd2O"
        ]
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|200 |Unauthorized |unauthorized error |User lacks permission to call the interface. |
|200 |IllegalParameter |illegal parameter |Invalid parameter. The reason may be a missing parameter or noncompliance with API requirements. |
|200 |InternalServerError |Internal server exception |The service exited due to an exception and cannot complete the interface request operation. |
