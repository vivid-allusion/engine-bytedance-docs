---
title: "ListSupportedAddons"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListSupportedAddons"
---

View the details of add\-ons that are supported by VKE.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListSupportedAddons&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListSupportedAddons&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the request parameters for the API. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListSupportedAddons |The API name. The name of the current API is `ListSupportedAddons`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [ListSupportedAddonsFilter](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons#listsupportedaddonsfilter) |no |\- |Filters for querying add\-ons. |


<span id="listsupportedaddonsfilter"></span>
### ListSupportedAddonsFilter


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Name |String |no |ingress\-nginx |The name of the add\-on to be queried. |
|PodNetworkModes |Array of String |no |["Flannel"] |Pod network models (CNI) supported by the add\-on. Values:<br><br><br>* **Flannel**: an independent underlay network solution, based on which a high\-performance network for clusters can be built along with the global routing capabilities of VPCs.<br><br>* **VPC\-CNI**: an underlay network solution implemented based on the ENIs of VPCs, providing high network performance. |
|DeployModes |Array of String |no |["Managed"] |Supported deployment modes. Values:<br><br><br>* **Unmanaged**: Obtain add\-ons deployed in unmanaged mode.<br><br>* **Managed**: Obtain add\-ons deployed in managed mode.<br><br>* An empty value indicates that add\-ons with all supported deployment modes are returned. |
|DeployNodeTypes |Array of String |no |["Node"] |Deployment node type. This parameter is required only when `DeployMode` is set to Unmanaged. Valid values:<br><br><br>* **Node**: Obtain add\-ons with node (ECS) as their deployment node type.<br><br>* **VirtualNode**: Obtain add\-ons with virtual node (VCI) as their deployment node type.<br><br>* An empty value indicates that add\-ons with all supported deployment node types are returned. |
|Necessaries |Array of String |no |["Required"] |The installation necessity level of the add\-on. Values:<br><br><br>* **Required**: Required<br><br>* **Recommended**: Recommended<br><br>* **OnDemand**: Optional |
|Categories |Array of String |no |["Storage"] |Add\-on categories. Values:<br><br><br>* **Storage**: Storage<br><br>* **Network**: Network<br><br>* **Monitor**: Monitoring<br><br>* **Scheduler**: Scheduling<br><br>* **Dns**: DNS<br><br>* **Security**: Security<br><br>* **Gpu**: GPU<br><br>* **Image**: Image |
|Versions.Compatibilities.KubernetesVersions |Array of String |no |["v1.20.4"] |Kubernetes versions supported by the add\-on. For a list of Kubernetes versions in VKE, see [Kubernetes version release history](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=ListSupportedAddons&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "Filter": {
        "Name": "ingress-nginx",
        "PodNetworkModes": ["Flannel"],
        "DeployModes": ["Unmanaged"],
        "DeployNodeTypes": ["Node"],
        "Necessaries": ["OnDemand"],
        "Categories": ["Network"]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [SupportedAddon](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons#supportedaddon) |[] |Details of add\-ons supported by VKE. |
|TotalCount |Integer |10 |Total number of add\-ons that VKE supports. |


<span id="supportedaddon"></span>
### SupportedAddon


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Name |String |ingress\-nginx |The name of the add\-on. |
|Versions |Array of [AddonVersion](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons#addonversion) |[{"Versoin":"v1.0.0","CompatibleVersions":["v0.9.0"]}] |Supported versions of the add\-on. |
|PodNetworkModes |Array of String |["Flannel"] |The network model (CNI) of the pods. Values:<br><br><br>* **Flannel**: Flannel, an independent Underlay container network model.<br><br>* **VpcCniShared**: VPC\-CNI, an Underlay container network model implemented based on the ENI of private networks. |
|DeployMode |String |Unmanaged |The add\-on deployment mode. Values:<br><br><br>* **Unmanaged**: Unmanaged mode.<br><br>* **Managed**: Managed mode. |
|DeployNodeTypes |Array of String |["Node"] |Deployment node type. Values:<br><br><br>* **Node**: The deployment node type is nodes (ECS).<br><br>* **VirtualNode**: The deployment node type is virtual nodes (VCI).<br><br>   This parameter is returned only when `DeployModes` is set to `Unmanaged`. |
|Necessary |String |Required |The installation necessity level of the add\-on. Parameter values:<br><br><br>* **Required**: Required<br><br>* **Recommended**: Recommended<br><br>* **OnDemand**: Optional |
|Categories |Array of String |["Storage"] |Add\-on categories. Values:<br><br><br>* **Network**: Network<br><br>* **Monitor**: Monitoring<br><br>* **Scheduler**: Scheduling<br><br>* **Dns**: DNS<br><br>* **Security**: Security<br><br>* **Gpu**: GPU<br><br>* **Image**: Image<br><br>* If an empty array is returned, the add\-on does not have a defined category. |


<span id="addonversion"></span>
### AddonVersion


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Version |String |v0.44.0 |The version of the add\-on. |
|CompatibleVersions |Array of String |["v0.42.0", "v0.43.0"] |A list of lower versions that can be upgraded to the current version. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "20230509****",
        "Action": "ListSupportedAddons",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Name": "ingress-nginx",
                "Versions": [
                    {
                        "Version": "v1.2.1-vke.2",
                        "CompatibleVersions": [
                            "v0.44.1",
                            "v0.44.0",
                            "v0.49.3",
                            "v0.49.3-vke.1",
                            "v0.49.3-vke.2"
                        ],
                        "Compatibilities": [
                            {
                                "KubernetesVersion": "<v1.24-0"
                            }
                        ]
                    }
                ],
                "PodNetworkModes": [
                    "CalicoVxlan",
                    "Flannel",
                    "VpcCniHybrid",
                    "VpcCniShared"
                ],
                "DeployMode": "Unmanaged",
                "DeployNodeTypes": [
                    "Node",
                    "VirtualNode"
                ],
                "Necessary": "OnDemand",
                "Categories": [
                    "Network"
                ]
            }
        ],
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes proprietary to this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.

&nbsp;
