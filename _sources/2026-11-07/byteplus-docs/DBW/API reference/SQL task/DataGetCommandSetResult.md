---
title: "DataGetCommandSetResult"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/datagetcommandsetresult"
---

Call the DataGetCommandSetResult API to query the execution results of the asynchronous execution command set.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The execution result can not be retrieved when the command set has not completed execution.</div>


* <div data-tips="true" data-tips-type="warning">After the command set is executed, the execution results are retained for only 5 minutes. Call the DataGetCommandSetResult API promptly to retrieve the execution result data.</div>


* <div data-tips="true" data-tips-type="warning">After the command set is executed, the DataGetCommandSetResult API can be called only once to retrieve the results. A subsequent API call within 5 minutes returns a duplicate query prompt. After this period, it indicates that the result is unavailable.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Called the [DataExecCommandSetAsync](https://docs.byteplus.com/en/docs/DBW/dataexeccommandsetasync) API to asynchronously execute a set of commands.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronize request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|CommandSetId |String |Yes |178887541272244\*\*\*\* |Command set ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/DBW/dataexeccommandsetasync">DataExecCommandSetAsync</a> API to get the command set ID.</div><br> |
|FilterType |String |No |Success |Execution status of SQL statements in the command set. The values are as follows:<br><br><br>* `Success`: Indicates the SQL statements that are executed successfully in the query command set.<br><br>* `Failed`: Indicates the SQL statements that failed to be executed in the query command set.<br><br>* `Cancel`: Indicates the command set whose query execution is canceled.<br><br>* `All`: (Default) Indicates that all command sets are queried. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Results |Array of [Result](https://docs.byteplus.com/en/docs/DBW/data-structure#result) |```json```<br>```[```<br>```    {```<br>```        "ColumnNames": [```<br>```            "Database"```<br>```        ],```<br>```        "CommandStr": "show databases;",```<br>```        "ReasonDetail": "",```<br>```        "RowCount": 2,```<br>```        "Rows": [```<br>```            {```<br>```                "Cells": [```<br>```                    "information_schema"```<br>```                ]```<br>```            },```<br>```            {```<br>```           "Cells": [```<br>```                    "sys"```<br>```                ]```<br>```            }```<br>```        ],```<br>```        "RunTime": 1715396681000,```<br>```        "State": "Success"```<br>```    }```<br>```]```<br> |A collection of command set execution results. For details, refer to [Result](https://docs.byteplus.com/en/docs/DBW/data-structure#result). |
|FilterType |String |Success |Conditions for filtering the execution status of SQL statements in the command set. The values are as follows:<br><br><br>* `Success`: Indicates that the query is for SQL statements that were executed successfully in the command set.<br><br>* `Failed`: Indicates that the query is for SQL statements that failed to execute in the command set.<br><br>* `Cancel`: Indicates that the query is for SQL statements that were canceled in the command set.<br><br>* `All`: Indicates that the query is for all SQL statements in the command set. |


<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DataGetCommandSetResult&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
     "CommandSetId": "178887541272244****",
     "FilterType": "All"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example


* The following shows an example of the return result for the first API query within 5 minutes after the command set is executed.

   ```JSON
   {
       "ResponseMetadata": {
           "RequestId": "2024051116125243C401426335B0927AD5-3223f0",
           "Action": "DataGetCommandSetResult",
           "Version": "2018-01-01",
           "Service": "dbw",
           "Region": "cn-beijing"
       },
       "Result": {
           "FilterType": "All",
           "Results": [
               {
                   "ColumnNames": [
                       "Database"
                   ],
                   "CommandStr": "show databases;",
                   "ReasonDetail": "",
                   "RowCount": 2,
                   "Rows": [
                       {
                           "Cells": [
                               "information_schema"
                           ]
                       },
                       {
                           "Cells": [
                               "sys"
                           ]
                       }
                   ],
                   "RunTime": 1715396681000,
                   "State": "Success"
               }
           ]
       }
   }
   ```
   

* The following shows an example of the result returned when the command set is not executed, or when the time exceeds 5 minutes after the command set is executed.

   ```JSON
   {
       "ResponseMetadata": {
           "RequestId": "20250811155627DA66FE54BA3182023484-16e659",
           "Action": "DataGetCommandSetResult",
           "Version": "2018-01-01",
           "Service": "dbw",
           "Region": "cn-beijing"
       },
       "Result": {
           "Results": [
               {
                   "ColumnNames": [],
                   "CommandStr": "",
                   "ReasonDetail": "No results found now, pls wait commands been executed or command set results have been retrieved or expired, you cannot fetch it again.",
                   "RowCount": 0,
                   "Rows": [],
                   "RunTime": 0,
                   "RunningInfo": {
                       "Info": "",
                       "IsOnlineDDL": false,
                       "Progress": "",
                       "TaskID": ""
                   },
                   "State": "Success"
               }
           ]
       }
   }
   ```
   

* The following shows an example of the result returned when the API is called again within 5 minutes after the command set is executed.

   ```JSON
   
   "Results": [
               {
                   "ColumnNames": [],
                   "CommandStr": "",
                   "ReasonDetail": "CommandSet Results have been retrieved. To fetch the data, please rerun DataExecCommandSetAsync",
                   "RowCount": 0,
                   "Rows": [],
                   "RunTime": 0,
                   "RunningInfo": {
                       "Info": "",
                       "IsOnlineDDL": false,
                       "Progress": "",
                       "TaskID": ""
                   },
                   "State": "Success"
               }
           ]
   ```
   


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
