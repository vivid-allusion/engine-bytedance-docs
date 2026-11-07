---
title: "EnableEventRule"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/EnableEventRule"
---

Enable an event rule.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

This API involves multiple downstream dependencies. Frequent calls will trigger rate limiting. We recommend keeping QPS not higher than 20 for this API.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=EnableEventRule&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=EnableEventRule&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request descriptions


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |EnableEventRule |The name of the API. The API name is `EnableEventRule`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|RuleId |Array of String |Yes |["158474\*\*\*\*\*\*8334720"] |ID of the event rule to be enabled. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=EnableEventRule&Version=2018-01-01
Content-Type: application/json
{
    "RuleId": [
        "158474******8334720"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Data |Object of [RuleIDsVo](https://docs.byteplus.com/en/docs/39/16306#ruleidsvo) |\- |Response data. |


<span id="ruleidsvo"></span>
### RuleIDsVo


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|RuleId |Array of String |["158474\*\*\*\*\*\*8334720"] |Event rule ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "EnableEventRule",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": {
            "RuleId": [
                "158474******8334720"
            ]
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no error codes unique to itself. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
