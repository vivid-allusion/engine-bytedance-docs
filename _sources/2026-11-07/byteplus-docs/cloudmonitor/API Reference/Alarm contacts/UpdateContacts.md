---
title: "UpdateContacts"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/UpdateContacts"
---

Update all the attributes of the specified contact, including the name, mobile phone, and email address.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=UpdateContacts&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateContacts&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateContacts |The name of the API. The API name is `UpdateContacts`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|Id |String |Yes |1452\*\*\*\*\*7244 |The contact ID.<br><br>You can call the [ListContacts](https://docs.byteplus.com/en/docs/cloudmonitor/ListContacts) API to obtain the contact ID. |
|Name |String |Yes |user\-name |The new name of the contact.<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can contain only Chinese characters, letters, digits, underscores (`_`), and hyphens (`-`).<br><br>* The name must be 1 to 128 characters in length. |
|Phone |String |No |1234567\*\*\*\* |The new phone number of the contact. If not provided, the original value of this parameter will be cleared by default. |
|Email |String |Yes |user@example.com |The new email address of the contact. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=UpdateContacts&Version=2018-01-01
Content-Type: application/json
{
    "Id": "1452*****7244",
    "Name": "user-name",
    "Email": "user@example.com",
    "Phone": "1234567****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |["1452\*\*\*\*\*7244"] |The contact ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateContacts",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            "1452*****7244"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
