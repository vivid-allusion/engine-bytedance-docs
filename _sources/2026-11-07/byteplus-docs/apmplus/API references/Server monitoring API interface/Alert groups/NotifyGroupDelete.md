---
title: "NotifyGroupDelete"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/NotifyGroupDelete"
---

Deletes the details of an alert group.

<span id="4de03c08"></span>
## Request method

Use the POST method to send the request.

<span id="f93601e6"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For the complete list of common parameters, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Field** |**Position** |**Type** |**Required** |**Description** |**Sample value** |
|---|---|---|---|---|---|
|Action |Query |String |Yes |The API name, which is a common parameter. |NotifyGroupDelete |
|Version |Query |String |Yes |The API version, which is a common parameter. |2022\-07\-11 |
|GroupId |RequestBody |Int32 |Yes |The alert group ID. |\- |


<span id="5f0e1980"></span>
## Response parameters

The Result parameter contains the following fields:


|**Field** |**Type** |**Description** |
|---|---|---|
|Id |Int32 |The alert group ID. |


<span id="1402bd30"></span>
## Sample request

```json
POST https://open.volcengineapi.com?Action=NotifyGroupDelete&Version=2022-07-11
&<Common Request Parameters>
```


<span id="66bbbd8e"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "",
        "Action": "NotifyGroupDelete",
        "Version": "2022-07-11",
        "Service": "apmplus_server",
        "Region": "cn-beijing"
    },
    "Result": {
    }
}
```
