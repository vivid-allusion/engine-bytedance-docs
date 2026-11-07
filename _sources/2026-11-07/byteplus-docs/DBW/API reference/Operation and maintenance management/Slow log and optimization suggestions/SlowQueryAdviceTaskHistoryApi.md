---
title: "SlowQueryAdviceTaskHistoryApi"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/SlowQueryAdviceTaskHistoryApi"
---

Call the SlowQueryAdviceTaskHistoryApi API to obtain historical slow log diagnosis information.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |SlowQueryAdviceTaskHistoryApi |The purpose of this request. The value is `SlowQueryAdviceTaskHistoryApi`. |
|Version |String |Yes |2018\-01\-01 |API version number. The value is `2018-01-01`. |
|InstanceType |String |Yes |MySQL |Database type. Valid values are as follows:<br><br><br>* `MySQL`: instance for RDS for MySQL.<br><br>* `VeDBMySQL`: instance for veDB MySQL. |
|InstanceId |String |Yes |vedb\-xxxx |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances">DescribeDBInstances</a> API to query the instance ID of RDS for MySQL.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the instance ID of veDB MySQL.</div><br> |
|PageNumber |Integer |Yes |1 |Page number. The value range is between 1 and 200. |
|PageSize |Integer |Yes |10 |The number of records per page. The value range is between 1 and 100. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Total |Integer |0 |Total number of slow log diagnosis tasks. |
|ResList |Array of Object |[Array of ResList Object](https://docs.byteplus.com/en/docs/DBW/data-structure#array-of-reslist-object) |Slow log diagnosis history, sorted by creation time from newest to oldest. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=SlowQueryAdviceTaskHistoryApi&Version=2018-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20250626T033433Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250626/cn-beijing/dbw/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceType": "MySQL",
  "InstanceId": "mysql-84c8b6******",
  "PageNumber": 1,
  "PageSize": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20250626113444104080177020262C4F",
    "Action": "SlowQueryAdviceTaskHistoryApi",
    "Version": "2018-01-01",
    "Service": "dbw",
    "Region": "cn-beijing"
  },
  "Result": {
    "Total": 142,
    "ResList": [
      {
        "Db": "V",
        "Date": "20250427",
        "Status": "SUCCESS",
        "AdviceNum": 0,
        "SummaryId": "9853ae90-4052-4953-b117-b1f590358819",
        "SlowQueryNum": 0,
        "AdviceIndexNum": 0,
        "NoAdviceSQLNum": 142,
        "AdviceRewriteNum": 0
      }
    ]
  }
}
```


<span id="g9nBOLQJ"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
