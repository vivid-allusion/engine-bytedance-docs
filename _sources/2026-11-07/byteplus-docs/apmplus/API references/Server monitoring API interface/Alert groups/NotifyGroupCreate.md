---
title: "NotifyGroupCreate"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/NotifyGroupCreate"
---

Configures the details of an alert group.

<span id="6a6a96af"></span>
## Request method

Use the POST method to send the request.

<span id="ba851280"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For the complete list of common parameters, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Field** |**Position** |**Type** |**Required** |**Description** |**Sample value** |
|---|---|---|---|---|---|
|Action |Query |String |Yes |The API name, which is a common parameter. |NotifyGroupCreate |
|Version |Query |String |Yes |The API version, which is a common parameter. |2022\-07\-11 |
|GroupName |RequestBody |String |Yes |The alert group name. |\- |
|Emails |RequestBody |Array[String] |Yes |The email addresses. |\- |
|PhoneNumbers |RequestBody |Array[String] |Yes |The phone numbers. |\- |


<span id="ecccc02a"></span>
## Response parameters

The Result parameter contains the following fields:


|**Field** |**Type** |**Description** |
|---|---|---|
|Id |Int32 |The alert group ID. |


<span id="8c3bcf26"></span>
## Sample request

```json
POST https://open.volcengineapi.com?Action=NotifyGroupCreate&Version=2022-07-11
&<Common Request Parameters>
```


<span id="9a87b620"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "",
        "Action": "NotifyGroupCreate",
        "Version": "2022-07-11",
        "Service": "apmplus_server",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id":1
    }
}
```
