---
title: "DescribeZones"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/DescribeZones"
---

Call DescribeZones to query availability zone information.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeZones&groupName=%E8%A7%84%E6%A0%BC%E7%9B%B8%E5%85%B3-%E5%85%AC%E5%BC%80&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|LDegOG">必选</span> `Example value: DescribeZones`

Action to execute, value: DescribeZones.



**Version**<span data-label="purple"> string</span><span data-api-tag="require|0dgZFo">必选</span> ` Example value: 2023-01-01`

API version, value: 2023\-01\-01.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Zones ** <span data-label="purple">object[] </span>`Example value: [{ "ZoneId": "cn-beijing-a", "ZoneName": "cn-beijing-a", "ZoneStatus": "AVAILABLE" }]`

List of supported availability zones.


**ZoneId ** <span data-label="purple">string </span>`Example value: cn-beijing-a`

Availability zone ID.



**ZoneName ** <span data-label="purple">string </span>`Example value: cn-beijing-a`

Availability zone name.



**ZoneStatus ** <span data-label="purple">string </span>`Example value: AVAILABLE`

Availability zone status.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DescribeZones&Version=2023-01-01 HTTP/1.1
Host: milvus.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251027T125158Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251027/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20251027205200157126214235C7B144",
    "Action": "DescribeZones",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "Zones": [
      {
        "ZoneId": "cn-beijing-a",
        "ZoneName": "cn-beijing-a",
        "ZoneStatus": "AVAILABLE"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |InternalServerError |InternalServerError |Internal server exception. |
