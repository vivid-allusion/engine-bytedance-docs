---
title: "DeleteAlertRule"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/DeleteAlertRule"
---

Deletes the details of alert rules.

<span id="6efd43fb"></span>
## Request method

Initiate the request using the POST method.

<span id="18288b38"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For the complete list of common parameters, see [Common parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Field** |**Position** |**Type** |**Required** |**Description** |**Sample value** |
|---|---|---|---|---|---|
|Action |Query |String |Yes |The API name, which is a public parameter. |DeleteAlertRule |
|Version |Query |String |Yes |The API version, which is a public parameter. |2022\-07\-11 |
|Ids |RequestBody |Array[Int64] |Yes |The alert configuration IDs. |\- |


<span id="6fbcd479"></span>
## Response parameters

The Result parameter contains the following fields:


|**Field** |**Type** |**Description** |
|---|---|---|
|Id |Int32 |The alert group ID. |


<span id="cb138f09"></span>
## Sample request

```json
POST https://open.volcengineapi.com?Action=DeleteAlertRule&Version=2022-07-11
&<Common Request Parameters>
```


<span id="473157a9"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "",
        "Action": "DeleteAlertRule",
        "Version": "2022-07-11",
        "Service": "apmplus_server",
        "Region": "cn-beijing"
    },
    "Result": {
    }
}
```
