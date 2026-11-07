---
title: "NotifyGroupList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/NotifyGroupList"
---

Obtains the details of alert groups.

<span id="502e6514"></span>
## Request method

Use the POST method to send the request.

<span id="947e5d1b"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For the complete list of common parameters, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Field** |**Position** |**Type** |**Required** |**Description** |**Sample value** |
|---|---|---|---|---|---|
|Action |Query |String |Yes |The API name, which is a common parameter. |NotifyGroupList |
|Version |Query |String |Yes |The API version, which is a common parameter. |2022\-07\-11 |
|Keyword |RequestBody |String |Yes |The search keyword. |\- |
|PageNo |RequestBody |Int32 |Yes |The page number. |\- |
|PageSzie |RequestBody |Int32 |Yes |The page size. |\- |


<span id="cf3a54de"></span>
## Response parameters

The Result parameter contains the following fields:


|**Field** |**Type** |**Description** |
|---|---|---|
|Total |Int32 |The number of results. |
|Groups |Array[NotifyGroup] |The alert group information. |


**NotifyGroup**


|**Field** |**Type** |**Description** |
|---|---|---|
|Id |Int32 |The alert group ID. |
|GroupName |AlertRuleConfig |The alert group name. |
|Emails |Array[String] |The email addresses. |
|PhoneNumbers |Array[String] |The phone numbers. |


<span id="ef4e143f"></span>
## Sample request

```json
POST https://open.volcengineapi.com?Action=NotifyGroupList&Version=2022-07-11
&<Common Request Parameters>
```


<span id="0a979df3"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "",
        "Action": "NotifyGroupList",
        "Version": "2022-07-11",
        "Service": "apmplus_server",
        "Region": "cn-beijing"
    },
    "Result": {
        "Groups":[
            {
                "Id":1,
                "GroupName":"",
                "Emails":[],
                "PhoneNumbers":[]
            }
        ],
        "Total":1
    }
}
```
