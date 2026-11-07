---
title: "NotifyGroupUpdate"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/NotifyGroupUpdate"
---

Modifies the details of an alert group.

<span id="e39936d3"></span>
## Request method

Use the POST method to send the request.

<span id="fe621862"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For the complete list of common parameters, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Field** |**Position** |**Type** |**Required** |**Description** |**Sample value** |
|---|---|---|---|---|---|
|Action |Query |String |Yes |The API name, which is a public parameter. |NotifyGroupUpdate |
|Version |Query |String |Yes |The API version, which is a public parameter. |2022\-07\-11 |
|GroupId |RequestBody |Int32 |Yes |The alert group ID. |\- |
|GroupName |RequestBody |String |Yes |The alert group name. |\- |
|Emails |RequestBody |Array[String] |Yes |The email addresses. |\- |
|PhoneNumbers |RequestBody |Array[String] |Yes |The phone numbers. |\- |


<span id="zEMFQGCV"></span>
## Response parameters

The Result parameter contains the following fields:


|**Field** |**Type** |**Description** |
|---|---|---|
|Id |Int32 |The alert group ID. |


<span id="17906c61"></span>
## Sample request

```json
POST https://open.volcengineapi.com?Action=NotifyGroupUpdate&Version=2022-07-11
&<Common Request Parameters>
```


<span id="1f1dbf06"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "",
        "Action": "NotifyGroupUpdate",
        "Version": "2022-07-11",
        "Service": "apmplus_server",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id":1
    }
}
```
