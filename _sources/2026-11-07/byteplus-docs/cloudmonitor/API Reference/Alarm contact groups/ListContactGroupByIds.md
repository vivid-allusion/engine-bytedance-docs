---
title: "ListContactGroupByIds"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListContactGroupByIds"
---

Query the details of the specified contact groups.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

A single call to this API can query up to 100 contact groups.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListContactGroupByIds&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListContactGroupByIds&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListContactGroupByIds |The name of the API. The API name is `ListContactGroupByIds`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Ids |Array of String |Yes |["145258255725730\*\*\*\*","145258255725730\*\*\*\*"] |Contact group IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListContactGroupByIds&Version=2018-01-01
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


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of [ContactGroupVO](https://docs.byteplus.com/en/docs/39/16279#contactgroupvo) |\- |Details of contact groups meeting the criteria. |


<span id="contactgroupvo"></span>
### ContactGroupVO


|Parameters |Type |Sample value |Description |
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
        "Action": "ListContactGroupByIds",
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
