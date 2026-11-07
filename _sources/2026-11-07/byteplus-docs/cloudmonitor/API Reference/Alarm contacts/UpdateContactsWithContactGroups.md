---
title: "UpdateContactsWithContactGroups"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/UpdateContactsWithContactGroups"
---

Add a contact to one or more specified contact groups.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

A contact can be added to up to 10 alert contact groups.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=UpdateContactsWithContactGroups&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateContactsWithContactGroups&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateContactsWithContactGroups |The API name. The API name is `UpdateContactsWithContactGroups`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Id |String |Yes |145262463627244\*\*\*\* |The contact ID.<br><br>You can call the [ListContacts](https://docs.byteplus.com/en/docs/cloudmonitor/ListContacts) API to obtain contact IDs. |
|ContactGroupIds |Array of String |Yes |["145080093687100\*\*\*\*","145080093687100\*\*\*\*"] |Contact group ID.<br><br><br>* The value will replace the associated contact groups of the contact.<br><br>* The number of contact group IDs cannot exceed 10. This is because each contact can be added to up to 10 contact groups.<br><br>* You can call the [ListContactGroups](https://docs.byteplus.com/en/docs/cloudmonitor/ListContactGroups) API to query contact group IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=UpdateContactsWithContactGroups&Version=2018-01-01
Content-Type: application/json
{
    "Id": "145262463627244****",
    "ContactGroupIds": [
        "145080093687100****",
        "145080093687100****"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |["145262463627244\*\*\*\*"] |The contact ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateContactsWithContactGroups",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            "145262463627244****"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
