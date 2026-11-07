---
title: "ListContactsByIds"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListContactsByIds"
---

Query the details of the specified contacts.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Up to 100 contacts can be queried in a single API call.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListContactsByIds&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListContactsByIds&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListContactsByIds |The name of the API. The API name is `ListContactsByIds`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|Ids |Array of String |Yes |["145258255725730\*\*\*\*", "145258255725730\*\*\*\*"] |The contact IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListContactsByIds&Version=2018-01-01
Content-Type: application/json
{
    "Ids": [
        "145258255725730****",
        "145258255725730****"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of [ContactsVO](https://docs.byteplus.com/en/docs/39/16286#contactsvo) |\- |Details of contacts meeting the criteria. |


<span id="contactsvo"></span>
### ContactsVO


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Id |String |145262463627244\*\*\*\* |The contact ID. |
|Name |String |user\-demo |The name of the contact. |
|Email |String |user\-demo@example.com |Email address of the contact. |
|Phone |String |1861283\*\*\*\* |Mobile phone number of the contact. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListContactsByIds",
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
                "Phone": "1861283****"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
