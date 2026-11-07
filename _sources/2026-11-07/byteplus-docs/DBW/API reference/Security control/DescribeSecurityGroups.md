---
title: "DescribeSecurityGroups"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeSecurityGroups"
---

Call the DescribeSecurityGroups API to query security rule sets.

<span id="Wq7xxfFx"></span>
## Request type

Synchronous request.

<span id="ExYhJcje"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Description** |**Sample** |
|---|---|---|---|---|
|PageNumber |Integer |Yes |Page number. The value range is 1 to 1000, with a default of 1. |10 |
|PageSize |Integer |Yes |Number of records per page. The value range is 1 to 1000, with a default of 10. |1 |
|[SecGroupSearchParam](https://docs.byteplus.com/en/docs/DBW/data-structure#asZRTdoy) |Object[] |No<br><br> |Filter criteria for the security rule set.<br><br> |See the request example. |


<span id="DKZeVp1W"></span>
## Response parameters


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|[SecurityGroups](https://docs.byteplus.com/en/docs/DBW/data-structure#QBXnQNLj)<br><br> | JSON<br><br> |Object[]<br><br> |See the response example. |
|Total |String |The number of Security rule sets returned. |7 |


<span id="LwbubDsC"></span>
## Request example

```JSON
POST /?Action=DescribeSecurityGroups&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "PageSize": 10,
    "PageNumber": 1,
    "SecGroupSearchParam": {
        "InstanceType": "MySQL",
        "Keyword": "mysql default"
    }
}
```


<span id="d1nfLELd"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2025090317335918DB6C82690D0ACF90E5-de1f85",
        "Action": "DescribeSecurityGroups",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "SecurityGroups": [
            {
                "AssociatedInstanceNum": 10,
                "Category": "Default",
                "Comment": "auto created by trigger 2100067216",
                "ID": "1740264867044012032",
                "InstanceType": "MySQL",
                "Name": "mysql default",
                "UpdateTime": "1703746451"
            },
            {
                "AssociatedInstanceNum": 1,
                "Category": "Default",
                "Comment": "auto created by trigger 2100000746",
                "ID": "1798193780860391424",
                "InstanceType": "Postgres",
                "Name": "postgres default",
                "UpdateTime": "1717557780"
            },
             {
                "AssociatedInstanceNum": 1,
                "Category": "Default",
                "Comment": "auto created by trigger 2100067216",
                "ID": "1805169413175947264",
                "InstanceType": "VeDBMySQL",
                "Name": "vedb_mysql default",
                "UpdateTime": "1719220901"
            },            
            {
                "AssociatedInstanceNum": 0,
                "Category": "Custom",
                "Comment": "created by",
                "ID": "1826683897031692288",
                "InstanceType": "MySQL",
                "Name": "、、、",
                "UpdateTime": "1724350353"
            },
            {
                "AssociatedInstanceNum": 0,
                "Category": "Default",
                "Comment": "auto created by trigger 2100067216",
                "ID": "1833328583884464128",
                "InstanceType": "MSSQL",
                "Name": "SQLSever default",
                "UpdateTime": "1725934570"
            },
            {
                "AssociatedInstanceNum": 0,
                "Category": "Custom",
                "Comment": "created by",
                "ID": "1843610605055934464",
                "InstanceType": "Postgres",
                "Name": "6767",
                "UpdateTime": "1728385995"
            },
            {
                "AssociatedInstanceNum": 0,
                "Category": "Custom",
                "Comment": "created by",
                "ID": "1851903984349007872",
                "InstanceType": "MSSQL",
                "Name": "test",
                "UpdateTime": "1730363291"
            }
        ],
        "Total": 7
    }
}
```


<span id="eDOZpqGg"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DBW/error-codes).
