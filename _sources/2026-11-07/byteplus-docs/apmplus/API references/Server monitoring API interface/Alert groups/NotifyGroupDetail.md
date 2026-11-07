---
title: "NotifyGroupDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/NotifyGroupDetail"
---

Obtains the details of alert groups.

<span id="0cce119f"></span>
## Request method

Use the POST method to send the request.

<span id="d2a8f4e7"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For the complete list of common parameters, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Field** |**Position** |**Type** |**Required** |**Description** |**Sample value** |
|---|---|---|---|---|---|
|Action |Query |String |Yes |The API name, which is a public parameter. |NotifyGroupDetail |
|Version |Query |String |Yes |The API version, which is a public parameter. |2022\-07\-11 |
|Keyword |RequestBody |String |Yes |The search keyword. |\- |
|PageNo |RequestBody |Int32 |Yes |The page number. |\- |
|PageSzie |RequestBody |Int32 |Yes |The page size. |\- |


<span id="0916f86d"></span>
## Response parameters

The Result parameter contains the following fields:


|**Field** |**Type** |**Description** |
|---|---|---|
|Detail |NotifyGroup |The alert group information. |


**NotifyGroup**


|**Field** |**Type** |**Description** |
|---|---|---|
|Id |Int32 |The alert group ID. |
|GroupName |AlertRuleConfig |The alert group name. |
|Emails |Array[String] |The email addresses. |
|PhoneNumbers |Array[String] |The phone numbers. |


<span id="19b0f26b"></span>
## Sample request

```json
POST https://open.volcengineapi.com?Action=NotifyGroupDetail&Version=2022-07-11
&<Common Request Parameters>
```


<span id="95859aa6"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "",
        "Action": "NotifyGroupDetail",
        "Version": "2022-07-11",
        "Service": "apmplus_server",
        "Region": "cn-beijing"
    },
    "Result": {
        "Detail": {
                "Id":1,
                "GroupName":"",
                "Emails":[],
                "PhoneNumbers":[]
            }

    }
}
```
