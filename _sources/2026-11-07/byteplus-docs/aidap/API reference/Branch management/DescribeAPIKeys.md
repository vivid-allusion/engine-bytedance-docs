---
title: "DescribeAPIKeys"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeAPIKeys"
---

Call the DescribeAPIKeys API to query the Workspace API keys.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate the workspace using the Supabase engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |noble\-heath\-3a48\*\*\*\* |ID of the workspace. |
|BranchId |String |No |br\-bloom\-duck\-61c7\*\*\*\* |Branch ID. |
|Offset |Integer |No |5 |Starting point for paginated query, an integer greater than or equal to 0, default value is 0. |
|Limit |Integer |No |5 |Page query count, an integer value greater than or equal to 1, default is 20. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|APIKeys |Array of [APIKey](https://docs.byteplus.com/en/docs/330/84412#apikey) |Refer to the Sample response. |List of API keys for the workspace |
|Total |Integer |2 |Total number of results matching the query criteria. |


<span id="apikey"></span>
### APIKey


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|CreateTime |String |2025\-11\-26T03:13:58Z |The creation time of the key (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|Key |String |eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZS1wbGF0Zm9ybSIsInJvbGUiOiJhbm9uIiwiZXhwIjozNjYxNDcwODM4fQ.rSen77EKXOB_RkD6mhc4prbNND9a2Xel6EEI0kw\*\*\*\* |API key. |
|Name |String |AnonKey |Key name. Values are:<br><br><br>* `AnonKey`<br><br>* `ServiceRoleKey` |
|Type |String |Public |API key type. Values are:<br><br><br>* `Public` (when the Name value is `AnonKey`)<br><br>* `Service` (when the Name value is `ServiceRoleKey`) |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeAPIKeys&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "noble-heath-3a48****",
    "BranchId": "br-bloom-duck-61c7****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeAPIKeys",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "APIKeys": [
            {
                "CreateTime": "2025-11-26T03:13:58Z",
                "Key": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZS1wbGF0Zm9ybSIsInJvbGUiOiJhbm9uIiwiZXhwIjozNjYxNDcwODM4fQ.rSen77EKXOB_RkD6mhc4prbNND9a2Xel6EEI0kw****",
                "Name": "AnonKey",
                "Type": "Public"
            },
            {
                "CreateTime": "2025-11-26T03:13:58Z",
                "Key": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZS1wbGF0Zm9ybSIsInJvbGUiOiJzZXJ2aWNlX3JvbGUiLCJleHAiOjM2Njk3NzkwOTl9.Do8PXbFSvMUfsJlVM1SKbMBkLuP2kGd962yV8lo****",
                "Name": "ServiceRoleKey",
                "Type": "Service"
            }
        ]，
        "Total": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
