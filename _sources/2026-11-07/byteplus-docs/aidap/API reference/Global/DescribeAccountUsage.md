---
title: "DescribeAccountUsage"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeAccountUsage"
---

Call the DescribeAccountUsage API to query resource usage information under the tenant account.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ProjectName |String |No |default |Specify the items to query. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|AccountId |String |210036\*\*\*\* |Account ID. |
|AccountUsage |Object of [AccountUsage](https://docs.byteplus.com/en/docs/330/84402#accountusage) |Refer to the return example. |Account usage details of various resources under the specified project. |
|EngineUsages |JSON Map |Refer to the sample response. |Usage details of each engine. |


<span id="accountusage"></span>
### AccountUsage


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|BranchComputeTimeSeconds |Double |198783 |Branch used compute duration. Unit is second. |
|BranchCreatedNum |Double |230 |Number of branches created.   |
|ComputeTimeSeconds |Double |198783 |Used compute time. Unit is second. |
|DataSizeTotalBytes |Double |\-1 |Storage size. Unit is byte.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Return value <code>-1</code> indicates unlimited.</div><br> |
|DataSizeUsedBytes |Double |180493721600 |Used data storage size. Unit is byte. |
|StatTime |String |2025\-10\-13T03:46:01Z |Data statistics time (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |


<span id="engineusages"></span>
### EngineUsages


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|StatTime |String |2025\-10\-13T03:46:01Z |Data statistics time (UTC time). Format: `yyyy-MM-ddTHH:mm:ssZ`. |
|BranchCreatedNum |Double |230 |Number of branches created.   |
|DataSizeUsedBytes |Double |180493721600 |Used data storage size. Unit is byte. |
|ComputeTimeSeconds |Double |198783 |Used compute time. Unit is second. |
|DataSizeTotalBytes |Double |\-1 |Storage size. Unit is byte.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Return value <code>-1</code> indicates unlimited.</div><br> |
|BranchComputeTimeSeconds |Double |198783 |Branch used compute duration. Unit is second. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6LLTI="></span>
### Sample request

```JSON
POST /?Action=DescribeAccountUsage&Version=2025-10-01 HTTP/1.1
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "ProjectName": "default"
}
```


<span id=".6L-U5Zue56S65L6LLTI="></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeAccountUsage",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "AccountId": "210036****",
        "AccountUsage": {
            "BranchComputeTimeSeconds": 0,
            "BranchCreatedNum": 230,
            "ComputeTimeSeconds": 0,
            "DataSizeTotalBytes": -1,
            "DataSizeUsedBytes": 180493721600,
            "StatTime": "2025-10-09T12:36:00Z"
        },
        "EngineUsages": {
            "PostgreSQL": {
                "BranchComputeTimeSeconds": 0,
                "BranchCreatedNum": 230,
                "ComputeTimeSeconds": 0,
                "DataSizeTotalBytes": -1,
                "DataSizeUsedBytes": 180493721600,
                "StatTime": "2025-10-09T12:36:00Z"
            }
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
