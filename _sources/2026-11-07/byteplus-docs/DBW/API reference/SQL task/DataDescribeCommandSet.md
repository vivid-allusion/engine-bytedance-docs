---
title: "DataDescribeCommandSet"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DataDescribeCommandSet"
---

Call the DataDescribeCommandSet interface to query the execution status of the command set.

<span id="1J4ZtlZL"></span>
## Prerequisites

The [DataExecCommandSetAsync](https://docs.byteplus.com/en/docs/DBW/dataexeccommandsetasync) interface has been called to execute the command set asynchronously.

<span id="HL7iLFeG"></span>
## Request type

Synchronous request.

<span id="7cBvsakj"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|CommandSetId |String |Yes |195480409964392\*\*\*\* |Command set ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/DBW/dataexeccommandsetasync">DataExecCommandSetAsync</a> interface to obtain the command set ID.</div><br> |


<span id="zaOG6CqZ"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Results |JSON |&nbsp;<br><br>```JSON```<br>```{```<br>```    "CommandSuccessNum": 6,//Number of successful executions```<br>```    "EndTime": 1754896592534, //Execution end time```<br>```    "Progress": 100,//Execution progress```<br>```    "SetContent": "select * from testdb;",//Executed command```<br>```    "SetState": "Finish", //Execution status (Completed)```<br>```    "StartTime": 1754896590564  //Execution start time```<br>```}```<br><br><br> |Execution status of the command set. |


<span id="lfShdiH4"></span>
## Request example

```JSON
POST /?Action=DataExecCommands&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{"CommandSetId": "195480409964392****"}
```


<span id="ItN9kBQV"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20250811151642E81E5592841727A5F118-870b2f",
        "Action": "DataDescribeCommandSet",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "CommandSuccessNum": 6,
        "EndTime": 1754896592534,
        "Progress": 100,
        "SetContent": "select * from testdb;",
        "SetState": "Finish",
        "StartTime": 1754896590564
    }
}
```
