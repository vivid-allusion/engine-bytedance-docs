---
title: "DescribeNonWhiteSessionList"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeNonWhiteSessionList"
---

Call the DescribeNonWhiteSessionList API to query the non\-allowlisted sessions of an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["mysql\-18554151\*\*\*\*"] |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can pass a maximum of 10 instance IDs at a time.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Use a comma (,) to separate instance IDs.</div><br> |
|DisassociateAllowListInfos |Array of [DisassociateAllowListInfo](https://docs.byteplus.com/en/docs/40/92660#disassociateallowlistinfo) |No |See the request example. |Information about the instance and allowlists for the non\-allowlist session. |


<span id="disassociateallowlistinfo"></span>
### DisassociateAllowListInfo


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-18554151\*\*\*\* |Instance ID. |
|AllowListIds |Array of String |Yes |["acl\-3e1a4959c48040f38c06089d87f5\*\*\*\*"] |The ID of the allowlist to disassociate. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|NonWhiteSessions |Array of [NonWhiteSessionInfo](https://docs.byteplus.com/en/docs/40/92660#nonwhitesessioninfo) |Refer to the Sample response. |List of non\-allowlist sessions. |
|TotalCount |Integer |3 |Total number of non\-allowlist sessions. |


<span id="nonwhitesessioninfo"></span>
### NonWhiteSessionInfo


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Command |String |SELECT SLEEP(3600) |SQL statements involved in the session. |
|DB |String |testdb01 |Name of the database involved in the session. |
|Host |String |11. ** *.* ** .1:47016 |The IP address of the client that initiated the session. |
|InstanceId |String |mysql\-18554151\*\*\*\* |Instance ID. |
|SessionId |String |41144 |Session ID. |
|Time |String |288 |Session duration. |
|User |String |tester |The user name that initiates the session. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeNonWhiteSessionList&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceIds": [
        "mysql-18554151****"
    ],
    "DisassociateAllowListInfos": [
        {
            "InstanceId": "mysql-18554151****",
            "AllowListIds": [
                "acl-3e1a4959c48040f38c06089d87f5****"
            ]
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202603111153341C8F8DC25B228826A25F-2d4a80",
        "Action": "DescribeNonWhiteSessionList",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "NonWhiteSessions": [
            {
                "Command": "SELECT SLEEP(3600)",
                "DB": "testdb01",
                "Host": "11.***.***.1:47016",
                "InstanceId": "mysql-18554151****",
                "SessionId": "41144",
                "Time": "288",
                "User": "testuser"
            },
            {
                "Command": "SELECT SLEEP(3600)",
                "DB": "testdb01",
                "Host": "11.***.***.1:47032",
                "InstanceId": "mysql-18554151****",
                "SessionId": "41145",
                "Time": "288",
                "User": "testuser"
            },
            {
                "Command": "SELECT SLEEP(3600)",
                "DB": "testdb01",
                "Host": "11.***.***.1:47038",
                "InstanceId": "mysql-18554151****",
                "SessionId": "41146",
                "Time": "288",
                "User": "testuser"
            }
        ],
        "TotalCount": 3
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
