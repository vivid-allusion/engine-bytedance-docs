---
title: "DeleteContactsByIds"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/DeleteContactsByIds"
---

Delete contacts.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Before deleting a contact, confirm that the contact is not associated with any alert contact group.


* Up to 100 contacts can be deleted in a single API call.


<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=DeleteContactsByIds&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteContactsByIds&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteContactsByIds |The name of the API. The API name is `DeleteContactsByIds`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|Ids |Array of String |Yes |["145262463627244\*\*\*\*"] |The contact ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=DeleteContactsByIds&Version=2018-01-01
Content-Type: application/json
{
    "Ids": [
        "145262463627244****"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |["145262463627244\*\*\*\*"] |The contact ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DeleteContactsByIds",
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
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
