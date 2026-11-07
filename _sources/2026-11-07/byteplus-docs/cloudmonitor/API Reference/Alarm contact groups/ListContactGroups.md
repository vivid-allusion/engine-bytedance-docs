---
title: "ListContactGroups"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListContactGroups"
---

Query the list of contact groups. Supports fuzzy search by contact group name.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListContactGroups&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListContactGroups&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListContactGroups |The name of the API. The API name is `ListContactGroups`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Name |String |No |group |The contact group name keyword. Fuzzy search is supported. |
|PageSize |Integer |No |20 |Number of rows per page for a pagination query. The default value is 10. The value must be greater than 0. |
|PageNumber |Integer |No |1 |The page number of the list. The default value is 1. The list range to be queried is:<br><br><br>* Actual start position = PageNumber × PageSize<br><br>* Actual end position = PageNumber × (PageSize+1) |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListContactGroups&Version=2018-01-01
Content-Type: application/json
{
    "Name": "group",
    "PageNumber": 1,
    "PageSize": 20
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of [ContactGroupVO](https://docs.byteplus.com/en/docs/39/16278#contactgroupvo) |\- |Details of contact groups meeting the criteria. |
|PageSize |Integer |30 |The number of rows per page for a pagination query. The default value is 30. |
|PageNumber |Integer |1 |The page number for a pagination query. The default value is 1. |
|TotalCount |Integer |2 |The total number of contact groups meeting the criteria. |


<span id="contactgroupvo"></span>
### ContactGroupVO


|Parameters |Types |Sample value |Description |
|---|---|---|---|
|Id |String |145080093687100\*\*\*\* |Contact group ID. |
|Name |String |DefaultAlertContactGroup |Contact group name. |
|AccountId |String |100000\*\*\*\* |Account ID that created this contact group. |
|CreatedAt |String |2021\-10\-20T20:27:53+08:00 |Creation time of the contact group. |
|UpdatedAt |String |2021\-10\-20T20:27:53+08:00 |Time when the contact group was last updated. |
|Description |String |This is a group. |Contact group description. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListContactGroups",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "Id": "145080093687100****",
                "Name": "Default Alert Contact Group",
                "Contacts": [
                    {
                        "Id": "145262463627244****",
                        "Name": "user-demo",
                        "Email": "user-demo@example.com",
                        "Phone": "1861283****"
                    }
                ],
                "AccountId": "100000****",
                "CreatedAt": "2021-10-20T20:27:53+08:00",
                "UpdatedAt": "2021-10-20T20:27:53+08:00",
                "Description": "This is a group."
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
