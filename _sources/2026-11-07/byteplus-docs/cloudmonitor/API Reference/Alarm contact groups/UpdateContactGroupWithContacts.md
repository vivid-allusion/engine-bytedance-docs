---
title: "UpdateContactGroupWithContacts"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/UpdateContactGroupWithContacts"
---

Update the members of the specified contact group, including adding and deleting specified contacts.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

A contact group can have up to 100 contacts.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=UpdateContactGroupWithContacts&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateContactGroupWithContacts&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateContactGroupWithContacts |The API name. The API name is `UpdateContactGroupWithContacts`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Id |String |Yes |145258255725730\*\*\* |Contact group ID.<br><br>You can call the [ListContactGroups](https://docs.byteplus.com/en/docs/cloudmonitor/ListContactGroups) API to query contact group IDs. |
|ContactsIdList |Array of String |Yes |["145247681036000\*\*\*\*","145080104031932\*\*\*\*"] |The updated list of contacts. The contact list will replace the original IDs in the contact group.<br><br><br>* You can call the [ListContacts](https://docs.byteplus.com/en/docs/cloudmonitor/ListContacts) API to query contact IDs.<br><br>* The number of contact IDs cannot exceed 100. This is because each contact group can have up to 100 contacts. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=UpdateContactGroupWithContacts&Version=2018-01-01
Content-Type: application/json
{
    "Id": "145258255725730***",
    "ContactsIdList": [
        "145247681036000****",
        "145080104031932****"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |["145258255725730\*\*\*\*"] |Contact group ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateContactGroupWithContacts",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            "145258255725730****"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
