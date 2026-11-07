---
title: "SetStateOfRulesByIds"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/SetStateOfRulesByIds"
---

Enable or disable an alert policy.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=SetStateOfRulesByIds&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=SetStateOfRulesByIds&serviceCode=Volc_Observe&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |SetStateOfRulesByIds |The name of the API. The API name is `SetStateOfRulesByIds`. |
|Version |String |Yes |2018\-01\-01 |The API version. The API version is `2018-01-01`. |
|Ids |Array of String |Yes |["155435238945\*\*\*\*\*\*"] |Alert policy ID. The data type is array. Separate multiple elements with comma (`,`). |
|State |String |Yes |enable |Alert policy status. Values:<br><br><br>* **disable**: Disabled<br><br>* **enable**: Enabled |
|ProjectName |String |No |project_1 |Name of the project to which the alert policy belongs. If no project is specified, it defaults to the "default" project. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=SetStateOfRulesByIds&Version=2018-01-01
Content-Type: application/json
{
    "Ids": [
        "155435238945******"
    ],
    "ProjectName": "project_1",
    "State": "enable"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Data |Array of String |[] |Response data content. It is an empty placeholder. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "SetStateOfRulesByIds",
        "Region": "cn-beijing",
        "Service": "cloudmonitor",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Data": [
            ""
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).

&nbsp;
