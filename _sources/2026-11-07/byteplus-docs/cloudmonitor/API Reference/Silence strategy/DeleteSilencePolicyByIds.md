---
title: "DeleteSilencePolicyByIds"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/DeleteSilencePolicyByIds"
---

Delete suppression policies.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=DeleteSilencePolicyByIds&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteSilencePolicyByIds&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteSilencePolicyByIds |The name of the API. The API name is `DeleteSilencePolicyByIds`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|Ids |Array of String |Yes |["19222306\*\*\*"] |A list of suppression policy IDs.<br><br>You can call the [ListSilencePolicy](https://docs.byteplus.com/en/docs/cloudmonitor/ListSilencePolicy) API to query suppression policy IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=DeleteSilencePolicyByIds&Version=2018-01-01
Content-Type: application/json
{
    "Ids": [
        "19222306***"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |[] |Response data. It is an empty placeholder. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DeleteSilencePolicyByIds",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": []
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
