---
title: "CreateKubeconfig"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateKubeconfig"
---

Generate the Kubeconfig credentials for a cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

This is an asynchronous API. When this API returns a success message, it does not mean that the KubeConfig can be immediately used. You need to call the [ListKubeconfigs](https://docs.byteplus.com/en/docs/vke/ListKubeconfigs) API to obtain the text information of the KubeConfig, and attempt to use it after five seconds.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateKubeconfig&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateKubeconfig&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateKubeconfig |The API name. The name of the current API is `CreateKubeconfig`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |cc8oo0ivqt\*\*\*\*\*\*\*\* |Cluster ID.<br><br>Cluster IDs can be queried by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in the <code>{Running,[Ok]}</code> or <code>{Updating,[Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to obtain the current status of the cluster.</div><br> |
|Type |String |Yes |Private |The type of the cluster KubeConfig file. Valid values:<br><br><br>* **Private**: A Kubeconfig file for private access<br><br>* **Public**: A Kubeconfig file for public access |
|ValidDuration |Integer |no |43800 |The valid period of the KubeConfig file.<br><br><br>* Valid values: 1 to 867240.<br><br>* Unit: hours.<br><br>* Default value: 26280 (3 years). |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=CreateKubeconfig&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "ClusterId": "cc8oo0ivqt********",
    "Type": "Private",
    "ValidDuration": 867240
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Id |String |kc5silum\*\*\*\*\*\*\*\* |Kubeconfig ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">We recommend that you store the KubeConfig ID securely for future use.</div><br> |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "0216353********",
        "Action": "CreateKubeconfig",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "kc5silum********"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. Refer to the [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) topic for details.


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied.ClusterStatus |The action has been denied due to wrong cluster status {{statusPhase}} and [{{statusConditions}}]. |The current status of the specified cluster does not support this operation. Please confirm the required cluster status for this API and try again. |
|400 |LimitExceeded.KubeconfigNumber |You have reached the limit of the number of kubeconfig that you can create. |The number of KubeConfig files that can be generated has reached the upper limit. For product limit descriptions, please refer to the [Limit](https://docs.byteplus.com/en/docs/vke/Limits) documentation. |


&nbsp;
