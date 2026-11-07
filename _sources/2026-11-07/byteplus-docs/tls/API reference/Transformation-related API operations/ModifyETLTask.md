---
title: "ModifyETLTask"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ModifyETLTask"
---

Call the ModifyETLTask interface to modify the specified processing task.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **PUT**

* Request URL: **https://tls\-{Region}.bytepluses.com/ModifyETLTask**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Description |String |False |`This is a test project` |A brief description of the data transformation task.<br><br><br>* The characters `<>`, `'`, `\`, `\\` are not supported.<br><br>* The length is from 0 to 64 characters. |
|Name |String |False |`etl-task-name` |The name of the transformation task, please refer to the [Resource Naming Convention](https://docs.byteplus.com/en/docs/tls/Limits#resource-naming-limit). |
|Script |String |False |`f_set("key","value")` |The transformation rules. |
|TargetResources |Array of [TargetResources](https://docs.byteplus.com/en/docs/38/36171#targetresources) |False |`/` |The Related information of the output target. |
|TaskId |String |True |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The transformation ID. |


<span id="targetresources"></span>
### TargetResources


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Alias |String |True |`test` |Customize the name of the output target, which will be used to refer to the output target in the data processing rules. |
|TopicId |String |True |`4a9bd4bd-53f1-43ff-b88a-64ee1be5****` |The log topic for storing processed logs. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
PUT https://tls-{Region}.bytepluses.com/ModifyETLTask HTTP/1.1
Content-Type: application/json
PUT https://tls-{Region}.ibytepluses.com/ModifyETLTask HTTP/1.1
Content-Type: application/json
{
    "TaskId": "063e66a3-7764-4bdc-****-709a2f4219b4",
    "Script": "f_set(\"aaaa\", 'aaaa', \"key2\", 'sssss', mode=\"overwrite\")",
    "Name": "asdfaf",
    "Description": "adsf653",
    "TargetResources": [
        {
            "Alias": "asdfadf",
            "TopicId": "a4d5dd28-07a*****8d2f-19080e36e579"
        }
    ]
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```


<span id="error-code"></span>
## Error code

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).

&nbsp;
