---
title: "UpdateInspectionPolicy"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/UpdateInspectionPolicy"
---

Updates the configuration of an inspection policy.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UpdateInspectionPolicy&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateInspectionPolicy&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateInspectionPolicy |The API name. The API name is `UpdateInspectionPolicy`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Id |String |Yes |R202604\*\*\*\* |The inspection policy ID.<br><br>You can call the [ListInspectionPolicies](https://docs.byteplus.com/en/docs/vke/ListInspectionPolicies?lang=en) API to obtain the inspection policy ID. |
|Name |String |No |policy\-test |The inspection policy name. |
|ResourceIds |Array of String |No |["ccbm7\*\*\*\*", "ccdhm\*\*\*\*"] |The inspection object IDs.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
|Enabled |Boolean |No |true |Whether to enable the inspection policy. Valid values:<br><br><br>* **true**: Yes.<br><br>* **false**: Disable it. |
|Schedule |String |No |0 0 13 \* 5 |The inspection schedule. The standard crontab command is required. For example, 0 0 13 \* 5 means it will be executed at midnight on the 13th of every month and every Friday. |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=UpdateInspectionPolicy&Version=2022-05-12
Content-Type: application/json
{
    "Id": "R2026******",
    "Name": "policy-test",
    "ResourceIds": [
        "ccbm7****",
        "ccdhm****"
    ],
    "Enabled": true,
    "Schedule": "0 0 13 * 5",
    "ClientToken": "BC028527-33B9-4990-A633-84E9F9****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

There are no proprietary response parameters for this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateInspectionPolicy",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
