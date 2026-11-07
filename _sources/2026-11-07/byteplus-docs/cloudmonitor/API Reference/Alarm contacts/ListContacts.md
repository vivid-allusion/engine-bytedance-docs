---
title: "ListContacts"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListContacts"
---

Query the list of contacts. Fuzzy search by contact name keyword is supported.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListContacts&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListContacts&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListContacts |The name of the API. The API name is `ListContacts`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|Name |String |No |user\-demo |Contact name keyword. Fuzzy search is supported.<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can contain only Chinese characters, letters, digits, underscores (`_`), and hyphens (`-`).<br><br>* The name must be 1 to 128 characters in length. |
|Phone |String |No |133\*\*\*\*4354 |Phone number keyword. Fuzzy search is supported. |
|Email |String |No |user\-demo@example.com |Email address keyword. Fuzzy search is supported. |
|PageNumber |Integer |No |1 |Page number of the list. The value must be greater than 0. The default value is 1. The list range to be queried is:<br><br><br>* Actual start position = (PageNumber\-1) \* PageSize<br><br>* Actual end position = PageNumber \* PageSize |
|PageSize |Integer |No |10 |Number of rows per page for a pagination query. The default value is 10. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListContacts&Version=2018-01-01
Content-Type: application/json
{
    "Name": "user-demo",
    "Email": "user-demo@example.com",
    "Phone": "133****4354",
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of [ContactsVO](https://docs.byteplus.com/en/docs/39/16285#contactsvo) |\- |Details of contacts meeting the criteria. |
|PageSize |Integer |30 |The number of rows per page for a pagination query. The default value is 30. |
|PageNumber |Integer |1 |The page number for a pagination query. The default value is 1. |
|TotalCount |Integer |2 |Total number of contacts meeting the criteria. |


<span id="contactsvo"></span>
### ContactsVO


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |145262463627244\*\*\*\* |The contact ID. |
|Name |String |user\-demo |The name of the contact. |
|Email |String |user\-demo@example.com |Email address of the contact. |
|Phone |String |1861283\*\*\*\* |Mobile phone number of the contact. |
|ContactGroups |Array of [ContactGroupVO](https://docs.byteplus.com/en/docs/39/16285#contactgroupvo) |\- |Contact groups associated with the contact. |


<span id="contactgroupvo"></span>
### ContactGroupVO


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |145080093687100\*\*\*\* |Contact group ID. |
|Name |String |DefaultAlertContactGroup |Contact group name. |
|AccountId |String |100000\*\*\*\* |ID of the account within which the contact group was created. |
|CreatedAt |String |2021\-10\-20T20:27:53+08:00 |Creation time of the contact group. |
|UpdatedAt |String |2021\-10\-20T20:27:53+08:00 |Time when the contact group was last updated. |
|Description |String |This is a group. |Contact group description. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListContacts",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            {
                "Id": "145262463627244****",
                "Name": "user-demo",
                "Email": "user-demo@example.com",
                "Phone": "1861283****",
                "ContactGroups": [
                    {
                        "Id": "145080093687100****",
                        "Name": "Default Alert Contact Group",
                        "AccountId": "100000****",
                        "CreatedAt": "2021-10-20T20:27:53+08:00",
                        "UpdatedAt": "2021-10-20T20:27:53+08:00",
                        "Description": "This is a group."
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
