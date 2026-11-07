---
title: "CreateInspectionPolicy"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateInspectionPolicy"
---

Creates an inspection policy.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateInspectionPolicy&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateInspectionPolicy&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateInspectionPolicy |The API name. The API name is `CreateInspectionPolicy`. |
|Version |String |Yes |May 12, 2022 |The API version. The API version is `2022-05-12`. |
|Name |String |No |policy\-test |The inspection policy name.<br><br><br>* It can contain uppercase and lowercase letters, Chinese characters, digits, and hyphens (\-).<br><br>* It can be 2 to 64 characters in length. |
|ClusterId |String |No |ccbm\*\*\*\*\* |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
|ResourceType |String |Yes |VkeCluster |The inspection object type. You can only set the value to **VkeCluster**, which indicates a cluster inspection. |
|ResourceIds |Array of String |No |["ccbm7\*\*\*\*", "ccdhm\*\*\*\*"] |The inspection object IDs. |
|Type |String |Yes |ClusterInspection |The inspection type. You can only set the value to **ClusterInspection**, which indicates that a regular inspection is initiated for the inspection object. |
|Enabled |Boolean |No |true |Whether the inspection policy is enabled. Valid values:<br><br><br>* **true**: The policy is enabled.<br><br>* **false**: The policy is disabled. |
|Schedule |String |No |0 0 13 \* 5 |The inspection schedule in standard crontab format. For example, `0 0 13 * 5` means it will be executed at midnight on the 13th of every month and every Friday. |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=CreateInspectionPolicy&Version=2022-05-12
Content-Type: application/json
{
    "Name": "policy-test",
    "ClusterId": "ccbm*****",
    "ResourceType": "VkeCluster",
    "ResourceIds": [
        "ccbm7****",
        "ccdhm****"
    ],
    "Type": "ClusterInspection",
    "Enabled": true,
    "Schedule": "0 0 13 * 5",
    "ClientToken": "BC028527-33B9-4990-A633-84E9F9****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |R2026\*\*\*\*\*\* |The inspection policy ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104********",
        "Action": "CreateInspectionPolicy",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "R2026******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API has no API\-specific error codes. For details about common error codes, see [Common error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes).
