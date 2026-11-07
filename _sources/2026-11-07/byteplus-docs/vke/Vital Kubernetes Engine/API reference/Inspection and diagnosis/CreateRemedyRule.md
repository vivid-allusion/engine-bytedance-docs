---
title: "CreateRemedyRule"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateRemedyRule"
---

Creates a check and self\-healing rule.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateRemedyRule&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateRemedyRule&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateRemedyRule |The API name. The API name is `CreateRemedyRule`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Name |String |Yes |Remedy\-Node |The name of the check and self\-healing rule. |
|ClusterId |String |Yes |cda5\*\*\*\* |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
|Rules |Array of [RemedyRule](https://docs.byteplus.com/en/docs/90/120600#remedyrule) |Yes |\- |The check and self\-healing rule. |
|ClientToken |String |No |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id="remedyrule"></span>
### RemedyRule


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|FaultType |String |Yes |NodeFault |The failure type. Valid values:<br><br><br>* **GPUFault:**  GPU failure<br><br>* **NodeFault:**  Node failure<br><br>* **SystemFault:**  System and add\-on failure<br><br>* **RegisteredFault:**  Custom failure<br><br>* **XidFault:**  XID exception |
|IncidentTypes |Array of String |Yes |["NodeNotReady","NodeFailure"] |The self\-healing check item. Different types of failures support different check items. You need to fill in the Kubernetes event here. For details, see [Check and self-healing overview](https://docs.byteplus.com/en/docs/vke/Check_and_self-healing_overview). |
|RemedyStrategy |Object of [RemedyStrategy](https://docs.byteplus.com/en/docs/90/120600#remedystrategy) |Yes |\- |The check and self\-healing policy. |


<span id="remedystrategy"></span>
### RemedyStrategy


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Remedy |The policy type. Valid values:<br><br><br>* **Notify**: Prompt for exception<br><br>* **CordonNode**: Cordon nodes<br><br>* **DrainNode**: Drain nodes<br><br>* **Remedy**: Self\-healing<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter can be set to <code>Remedy</code> only if <code>RemedyRule.FaultType</code> is set to <code>RegisteredFault</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter can be set to <code>DrainNode</code> or <code>Remedy</code> only if <code>RemedyRule.FaultType</code> is set to <code>XidFault</code>.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=CreateRemedyRule&Version=2022-05-12
Content-Type: application/json
{
    "Name": "Remedy-Node",
    "ClusterId": "cda5****",
    "Rules": [
        {
            "FaultType": "NodeFault",
            "IncidentTypes": [
                "NodeNotReady",
                "NodeFailure"
            ],
            "RemedyStrategy": {
                "Type": "Remedy"
            }
        }
    ],
    "ClientToken": "BC028527-33B9-4990-A633-84E9F9****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |R202609\*\*\*\* |The ID of the check and self\-healing rule. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "CreateRemedyRule",
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

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
