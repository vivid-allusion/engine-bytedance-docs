---
title: "GetSilenceUserListAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsilenceuserlistapi"
---

Call this API to get the list of users who are prohibited from posting chat messages in a specific live\-streaming activity.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `GetSilenceUserListAPI`

* Request method: GET

* Request URI: `http://livesaas.byteplusapi.com/?Action=GetSilenceUserListAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="Query string parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Action |Yes |String |API operation. |
|Version |Yes |String |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Yes |Integer |ID of the live\-streaming activity. |


<span id="Sample request"></span>
### Sample request

```JSON
Get http://livesaas.byteplusapi.com/?Action=GetSilenceUserListAPI&Version=2020-06-01&ActivityId=1231231231
```


<span id="Response"></span>
## Response

<span id="Response schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|UserList |Array |A list of silenced users. |


<span id="UserInfo"></span>
#### UserInfo


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|UserId |Integer |User ID. |
|Nickname |String |Nickname of the user. |


<span id="Sample response"></span>
### Sample response

The following is a sample response for a successful request:

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202201201826170101501312091D1C09D2",
        "Action":"GetSilenceUserListAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1"
    },
    "Result":{
         "UserList": [
             {
                 "Nickname": "user1",
                 "UserId": 1670265947464959
             }
         ]
     }
}
```
