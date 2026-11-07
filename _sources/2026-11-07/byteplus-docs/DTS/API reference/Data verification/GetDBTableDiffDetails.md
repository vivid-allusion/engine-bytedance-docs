---
title: "GetDBTableDiffDetails"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/getdbtablediffdetails"
---

Call the GetDBTableDiffDetails interface to view the details of different database table data in the data verification task.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Only applicable to increment validation tasks.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskID |String |Yes |4d3d7e8353ba4d6d8358a7\*\*\*\*\*\*\*\* |Task ID.<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> API to query the task ID.</div><br> |
|DB |String |Yes |dtsDBName |Database name. |
|Table |String |Yes |my_table |Table name. |
|PageNumber |Integer |No |1 |Page number. The value range is 1 to 1000, with a default of 1. |
|PageSize |Integer |No |10 |Number of records per page. The value range is 1 to 1000, with a default of 10. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Items |Array of [DBTableDiffDetails](https://docs.byteplus.com/en/docs/57/47096#dbtablediffdetails) |Inconsistent data details. |inconsistent data details |
|Total |Long |1 |Total amount of inconsistent data. |


<span id="dbtablediffdetails"></span>
### DBTableDiffDetails


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Pk |Array of [PkItem](https://docs.byteplus.com/en/docs/57/47096#pkitem) |&nbsp;<br><br>```JSON```<br>```{```<br>```    "ColName":"id",```<br>```    "ColValue": "502867"```<br>```}```<br> |Details of the inconsistent primary key. |
|Column |Array of [ColumnItem](https://docs.byteplus.com/en/docs/57/47096#columnitem) |&nbsp;<br><br>```JSON```<br>```[```<br>```    {```<br>```        "ColName": "c",```<br>```        "DestValue": "80981261709-09674799628",```<br>```        "SrcValue": "18491802815-85936056201"```<br>```    }```<br>```]```<br> |Details of the inconsistent column. |
|SrcGTID |String |b42abb6e\-b6d9\-11ef\-bdf8\-52540bdc0a3f:16106313 |The GTID corresponding to the row when it is updated on the source end. |
|DestGTID |String |b42abb6e\-b6d9\-11ef\-bdf8\-52540bdc0a3f:1689754 |The GTID corresponding to the row when it is updated on the destination. |
|SrcEventTime |Long |1727233945000 |The time when the row is updated on the source end, in milliseconds timestamp format. |
|DestEventTime |Long |1727233945000 |The time when the row is updated on the target end, in milliseconds timestamp format. |


<span id="pkitem"></span>
### PkItem


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ColName |String |id |Primary key name |
|ColValue |String |502867 |Primary key value. |


<span id="columnitem"></span>
### ColumnItem


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ColName |String |c |Column name. |
|SrcValue |String |18491802815\-85936056201 |The value of the source column. |
|DestValue |String |80981261709\-09674799628 |The value of the target column. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=GetDBTableDiffDetails&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskID": "4d3d7e8353ba4d6d8358a7********",
    "PageNumber": 1,
    "PageSize": 10,
    "DB": "dtsDBName",
    "Table": "my_table"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202412181542138EE247090D8B81C0EBF9-063897",
        "Action": "GetDBTableDiffDetails",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Column": [
                    {
                        "ColName": "c",
                        "DestValue": "80981261709-09674799628",
                        "SrcValue": "18491802815-85936056201"
                    }
                ],
                "DestEventTime": 0,
                "DestGTID": "",
                "Pk": [
                    {
                        "ColName": "id",
                        "ColValue": "502867"
                    }
                ],
                "SrcEventTime": 1734422952000,
                "SrcGTID": "b42abb6e-b6d9-11ef-bdf8-52540bdc0a3f:16106313"
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
