---
title: "DescribeManagedUsers"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeManagedUsers"
---

Call the DescribeManagedUsers API to query user information.

<span id="yft1nME6"></span>
## Request type

Synchronous request.

<span id="1l2TnTVg"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Description** |**Sample** |
|---|---|---|---|---|
|PageNumber |Integer |Yes |Page number. The value range is 1 to 1000, with a default of 1. |1 |
|PageSize |Integer |Yes |Number of records per page. The value range is 1 to 1000, with a default of 10. |10 |
|SearchParam<br><br> |Object[]<br><br> |No<br><br> |User information. |See the request example. |


<span id="gWOmCF8s"></span>
## Response parameters


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|[DbwUsers](https://docs.byteplus.com/en/docs/DBW/data-structure#JQfxpFO8) |Object[] |User information. |See the response example. |
|MaxExecuteCount |String |Maximum number of queries per day. |2,000 |
|MaxExecuteDuration |String |Valid duration for query count. |OneDayAvailable |
|MaxExecuteExpiredTime |String |Queries expiration time. |1736438399 |
|MaxResultCount |String |Daily query row limit. |2,000 |
|MaxResultDuration |String |Valid duration for query row count. |ThreeMonthAvailable |
|MaxResultExpiredTime |String |Queries expiration time. |1731999285 |
|RoleType |String |Role type. The values are as follows:<br><br><br>* ADMIN: Administrator<br><br>* USER: Normal user<br><br><br>For more information about roles, see [Role](https://docs.byteplus.com/en/docs/DBW/role-description). |ADMIN<br><br> |
|UserGroupType |String |User group type. |DEFAULT |
|UserId |String |User ID. |2100067216 |
|UserName |String |Username. |huahua |
|UserState |String |User status. |NORMAL |
|Total |Integer |The number of users returned. |1 |


<span id="vsrMwj9G"></span>
## Request example

```JSON
POST /?Action=DescribeManagedUsers&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "PageSize": 10,
    "PageNumber": 1,
    "SearchParam": {
        "UserName": "huahua"
    }
}
```


<span id="pntJHAXO"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025092415352459C572A1140886E5156D-939863",
        "Action": "DescribeManagedUsers",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "DbwUsers": [
            {
                "AccountType": "CHILD",
                "GroupDetails": [
                    {
                        "GroupId": "1962656497431244800",
                        "GroupName": "1111"
                    }
                ],
                "MaxExecuteCount": 2000,
                "MaxExecuteDuration": "OneDayAvailable",
                "MaxExecuteExpiredTime": 1736438399,
                "MaxResultCount": 2000,
                "MaxResultDuration": "ThreeMonthAvailable",
                "MaxResultExpiredTime": 1731999285,
                "RoleType": "ADMIN",
                "UserGroupType": "DEFAULT",
                "UserId": "2100067216",
                "UserName": "huahua",
                "UserState": "NORMAL"
            }
        ],
        "Total": 1
    }
}
```


<span id="TLm6eFms"></span>
## Error code

For more information, see [Error code](https://docs.byteplus.com/en/docs/DBW/error-codes).
