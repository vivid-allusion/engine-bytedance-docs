---
title: "UpdateContactGroup"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/UpdateContactGroup"
---

Update the basic information of the specified contact group.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=UpdateContactGroup&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateContactGroup&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateContactGroup |The name of the API. The API name is `UpdateContactGroup`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|Id |String |Yes |145258255725730\*\*\* |Contact group ID.<br><br>You can call the [ListContactGroups](https://docs.byteplus.com/en/docs/cloudmonitor/ListContactGroups) API to query contact group IDs. |
|Name |String |No |primary_contact_group |Contact group name.<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can contain only Chinese characters, letters, digits, underscores (`_`), and hyphens (`-`).<br><br>* The name must be 1 to 128 characters in length. |
|Description |String |No |This contact group is the primary contact group. Use this contact group if you do not need a particular contact group. |Contact group description.<br><br><br>* It must be 1 to 255 characters in length.<br><br>* It can contain Chinese characters, letters, and special characters such as underscores. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=UpdateContactGroup&Version=2018-01-01
Content-Type: application/json
{
    "Description": "This contact group is the primary contact group. Please bind this contact group by default.",
    "Id": "145258255725730***",
    "Name": "primary_contact_group"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |["1599\*\*\*\*\*9776"] |Contact group ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateContactGroup",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            "1599*****9776"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
