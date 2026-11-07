---
title: "UpdateKubernetesObservabilityComponentConfigs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/UpdateKubernetesObservabilityComponentConfigs"
---

Enable basic observability capabilities of cloud\-native observability for the specified service.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before using this API to enable basic cloud\-native observability capabilities for the specified services (such as AI resources, DNS, and CSI storage), confirm that cloud\-native observability is enabled in the cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability?lang=en">Enabling observability</a>.</div>


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UpdateKubernetesObservabilityComponentConfigs&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateKubernetesObservabilityComponentConfigs&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateKubernetesObservabilityComponentConfigs |The API name. The API name is `UpdateKubernetesObservabilityComponentConfigs`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |cc9l74mvqtofjnoj5xxxx |Cluster ID.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs. |
|ObservabilityComponentConfigs |Array of [UpdatableObservabilityComponentConfig](https://docs.byteplus.com/en/docs/90/119580#updatableobservabilitycomponentconfig) |Yes |\- |A list of basic observability configurations for services.<br><br><br>* Each element of the array represents the basic observability toggle configuration for a service.<br><br>* To configure multiple services at the same time, pass multiple objects in the array. |


<span id="updatableobservabilitycomponentconfig"></span>
### UpdatableObservabilityComponentConfig


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Enabled |Boolean |Yes |true |Whether to enable the basic observability feature for the service. Valid values:<br><br><br>* **true**: Enables the feature. The system collects basic observability data from this service.<br><br>* **false**: Does not enable this feature. The system no longer collects basic observability data from this service. |
|Component |String |Yes |vko.monitoring.dns |The service for which you want to enable basic observability. Valid values:<br><br><br>* **vko.monitoring.container**: Container service<br><br>* **vko.monitoring.ctrlPanel**: control plane service<br><br>* **vko.monitoring.dns**: DNS service<br><br>* **vko.monitoring.cni**: CNI Network<br><br>* **vko.monitoring.csi**: CSI Storage<br><br>* **vko.monitoring.ingress**: Ingress service<br><br>* **vko.monitoring.imageSpeedup**: Image speedup<br><br>* **vko.monitoring.imageRegistry**: Image repository<br><br>* **vko.monitoring.ai**: AI resources<br><br>* **vko.aiopsRemediation**: AIOps remediation |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=UpdateKubernetesObservabilityComponentConfigs&Version=2022-05-12
Content-Type: application/json
{
    "ClusterId": "cc9l74mvqt********",
    "ObservabilityComponentConfigs": [
        {
            "Enabled": true,
            "Component": "vko.monitoring.dns"
        }
    ]
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
        "RequestId": "20230604110420**********",
        "Action": "UpdateKubernetesObservabilityComponentConfigs",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
