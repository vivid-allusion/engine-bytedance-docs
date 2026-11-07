---
title: "DescribePreCheckDetail"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/describePreCheckDetail"
---

Call the DescribePreCheckDetail API to query the pre\-check results of a ticket.

<span id="8TQczRTO"></span>
## Request type

Synchronous request

<span id="Aew0VabR"></span>
## Request parameters


|**Name** |**Type** |**Is it required?**  |**Description** |**Sample** |
|---|---|---|---|---|
|TicketId |String<br><br> |Yes |Ticket ID. |2013522829558\*\*\*\*\*\*<br><br> |


<span id="fx67i6C3"></span>
## Response parameters

When the response parameters AllPass, EnableSubmitTicket, and PrecheckFinished are all set to true, it indicates the pre\-check has passed.


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|AllPass |Boolen |Indicates whether the current operation has passed all preset check rules. Possible values are:<br><br><br>* `true`: Indicates all preset check rules have been passed.<br><br>* `false`: Indicates some preset check rules have failed. |true |
|EnableSubmitTicket |Boolen |Whether the ticket is submitted successfully. Valid values:<br><br><br>* `true`: The ticket is submitted successfully.<br><br>* `false`: The ticket failed to be submitted. |true |
|IsContainDDL |Boolen |Indicates whether the pre\-check SQL statement contains DDL. Possible values are:<br><br><br>* `true`: Indicates the SQL statement contains DDL, such as CREATE, ALTER, DROP, etc.<br><br>* `false`: Indicates the SQL statement only includes DML, such as SELECT, INSERT, UPDATE, DELETE. |true |
|PreCheckDetails |Array of string |Pre\-check item details. For details, see [PreCheckDetailes](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=zh#q8Dcvm5A). |```JSON```<br>```[```<br>```    {```<br>```        "IsItemCanBeIgnore": false,```<br>```        "IsItemIgnored": false,```<br>```        "ItemDetails": [```<br>```            {```<br>```                "Result": "0",```<br>```                "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('王五', 28, '13800138000');"```<br>```            },```<br>```            {```<br>```                "Result": "0",```<br>```                "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138001');"```<br>```            },```<br>```            {```<br>```                "Result": "0",```<br>```                "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '138001380022');"```<br>```            },```<br>```            {```<br>```                "Result": "0",```<br>```                "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138003');"```<br>```            }```<br>```        ],```<br>```        "ItemName": "影响行数(系统统计值,实际影响行数仍然以SQL执行为准!)",```<br>```        "PreCheckItem": "Explain",```<br>```        "PreCheckState": "Success",```<br>```        "Result": "0"```<br>```    }```<br>```]```<br> |
|PrecheckFinished |Boolen |Whether the system has completed all pre\-checks for the SQL statement. The values are as follows:<br><br><br>* `true`: Indicates the system has completed all pre\-checks for the SQL statement (e.g., syntax, permissions, performance, security) and generated the inspection results. For details of the pre\-check results, see [PreCheckDetails](https://docs.byteplus.com/en/docs/DBW/data-structure?lang=zh#q8Dcvm5A).<br><br>* `false`: Indicates the system has not yet completed all pre\-checks for the SQL statement, including cases where pre\-checks have not started, are in progress, or were interrupted due to anomalies. |true |
|Step |Integer |Indicates the current workflow stage or execution step number of the operation. |6 |
|TicketId |String |Ticket ID. |2013522829558\*\*\*\*\*\* |
|TotalNeedCheck |Integer |Total number of pre\-check items required for the current ticket. |6 |


<span id="TlteJlJS"></span>
## Request example

```SQL
POST /?Action=DescribePreCheckDetail&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.volcengineapi.com
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "TicketId": "2013522829558******"
}
```


<span id="7hX8BJYF"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260225105133E397870590FACAD82A4E-f162e3",
        "Action": "DescribePreCheckDetail",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "AllPass": true,
        "EnableSubmitTicket": true,
        "IsContainDDL": false,
        "PreCheckDetails": [
            {
                "IsItemCanBeIgnore": false,
                "IsItemIgnored": false,
                "ItemDetails": [
                    {
                        "Result": "0",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('王五', 28, '13800138000');"
                    },
                    {
                        "Result": "0",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138001');"
                    },
                    {
                        "Result": "0",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '138001380022');"
                    },
                    {
                        "Result": "0",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138003');"
                    }
                ],
                "ItemName": "影响行数(系统统计值,实际影响行数仍然以SQL执行为准!)",
                "PreCheckItem": "Explain",
                "PreCheckState": "Success",
                "Result": "0"
            },
            {
                "IsItemCanBeIgnore": false,
                "IsItemIgnored": false,
                "ItemDetails": [
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('王五', 28, '13800138000');"
                    },
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138001');"
                    },
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '138001380022');"
                    },
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138003');"
                    }
                ],
                "ItemName": "语法检查",
                "PreCheckItem": "Syntax",
                "PreCheckState": "Success",
                "Result": "Pass"
            },
            {
                "IsItemCanBeIgnore": false,
                "IsItemIgnored": false,
                "ItemDetails": [
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('王五', 28, '13800138000');"
                    },
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138001');"
                    },
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '138001380022');"
                    },
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138003');"
                    }
                ],
                "ItemName": "权限检查",
                "PreCheckItem": "Permission",
                "PreCheckState": "Success",
                "Result": "Pass"
            },
            {
                "IsItemCanBeIgnore": false,
                "IsItemIgnored": false,
                "ItemDetails": [
                    {
                        "Result": "",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('王五', 28, '13800138000');"
                    },
                    {
                        "Result": "",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138001');"
                    },
                    {
                        "Result": "",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '138001380022');"
                    },
                    {
                        "Result": "",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138003');"
                    }
                ],
                "ItemName": "安全规则检查",
                "PreCheckItem": "SecurityRule",
                "PreCheckState": "Success",
                "Result": "Pass"
            },
            {
                "IsItemCanBeIgnore": false,
                "IsItemIgnored": false,
                "ItemDetails": [
                    {
                        "Result": "Instance Status is Running",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('王五', 28, '13800138000');"
                    },
                    {
                        "Result": "Instance Status is Running",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138001');"
                    },
                    {
                        "Result": "Instance Status is Running",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '138001380022');"
                    },
                    {
                        "Result": "Instance Status is Running",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138003');"
                    }
                ],
                "ItemName": "实例状态检查",
                "PreCheckItem": "Instance",
                "PreCheckState": "Success",
                "Result": "Instance Status is Running"
            },
            {
                "IsItemCanBeIgnore": true,
                "IsItemIgnored": false,
                "ItemDetails": [
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('王五', 28, '13800138000');"
                    },
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138001');"
                    },
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '138001380022');"
                    },
                    {
                        "Result": "Pass",
                        "SQL": "INSERT INTO `tb1`  (name, age, phone) VALUES ('张三', 28, '13800138003');"
                    }
                ],
                "ItemName": "参数检查",
                "PreCheckItem": "Param",
                "PreCheckState": "Success",
                "Result": "Pass"
            }
        ],
        "PrecheckFinished": true,
        "Step": 6,
        "TicketId": "2013522829558******",
        "TotalNeedCheck": 6
    }
}
```


<span id="Hzl8yge8"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
