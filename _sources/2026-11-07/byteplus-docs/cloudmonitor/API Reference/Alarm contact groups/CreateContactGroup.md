---
title: "CreateContactGroup"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/CreateContactGroup"
---

Create an alert contact group.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

A single account can create at most 100 contact groups.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=CreateContactGroup&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateContactGroup&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Paramete |Types |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateContactGroup |The name of the API. The API name is `CreateContactGroup`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|Name |String |Yes |primary_contact_group |Contact group name.<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can contain only Chinese characters, letters, digits, underscores (`_`), and hyphens (`-`).<br><br>* The name must be 1 to 128 characters in length. |
|Description |String |No |This contact group is the primary contact group. Use this contact group if you do not need a particular contact group. |Contact group description.<br><br><br>* If no value is provided, it defaults to an empty string.<br><br>* It must be 1 to 255 characters in length.<br><br>* It can contain Chinese characters, letters, and special characters such as underscores. |
|ContactsIdList |Array of String |No |["145247681036000\*\*\*\*",<br><br>"145247681036001\*\*\*\*"] |Contacts to be added to the contact group. The value is a list of contact IDs.<br><br><br>* You can call the [ListContacts](https://docs.byteplus.com/en/docs/cloudmonitor/ListContacts) API to query contact IDs.<br><br>* The number of contact IDs cannot exceed 10, since a single contact group can contain up to 10 contacts. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=CreateContactGroup&Version=2018-01-01
Content-Type: application/json
{
    "Description": "This contact group is the primary contact group. Please bind this contact group by default.",
    "Name": "primary_contact_group",
    "ContactsIdList": [
        "145247681036000****",
        "145247681036001****"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |["1599\*\*\*\*\*9648"] |Contact group ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateContactGroup",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            "1599*****9648"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
