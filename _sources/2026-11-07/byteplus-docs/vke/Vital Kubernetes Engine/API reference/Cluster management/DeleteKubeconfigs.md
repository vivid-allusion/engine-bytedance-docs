---
title: "DeleteKubeconfigs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/DeleteKubeconfigs"
---

Revoke the Kubeconfig credentials of a cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* This API is asynchronous. A success message returned by this API does not necessarily indicate that the kubeconfig has been successfully deleted. You need to wait for five seconds and then call the [ListKubeconfigs](https://docs.byteplus.com/en/docs/vke/ListKubeconfigs) API to check whether the kubeconfig exists. If it is not found, it has been deleted successfully.

* The effect of deleting the cluster kubeconfig credentials varies depending on the permissions of the API caller:

   * If the caller has BytePlus root user permissions, they can delete credentials of their own account and their IAM users.

   * If the caller has IAM user permissions, they can only delete their own kubeconfig credentials.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=DeleteKubeconfigs&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteKubeconfigs&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteKubeconfigs |The API name. The name of the current API is `DeleteKubeconfigs`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |cc5silum\*\*\*\* |Cluster ID.<br><br>Cluster IDs can be queried by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in the <code>{Running,[Ok]}</code> or <code>{Updating,[Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to obtain the current status of the cluster.</div><br> |
|Ids |Array of String |Yes |["kc5silumrsfeqxxxx"] |Kubeconfig ID.<br><br>To query the ID of the kubeconfig, click the name of the target cluster on the **Cluster** page of the [VKE console](https://console.byteplus.com/vke), and on the cluster **Overview** page that appears, go to the **Connection** tab. You can also view the KubeConfig ID saved after you call the [CreateKubeconfig](https://docs.byteplus.com/en/docs/vke/CreateKubeconfig) API. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=DeleteKubeconfigs&Version=2022-05-12 HTTP/1.1
Content-Type:application/json

{
    "ClusterId": "cc5sil****",
    "Ids": ["kc5silumrsfeq****"]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

There are no proprietary response parameters for this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "m5Aeoaf****",
        "Action": "DeleteKubeconfigs",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. Refer to the [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) topic.


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied.ClusterStatus |The action has been denied due to wrong cluster status {{statusPhase}} and [{{statusConditions}}]. |The current status of the specified cluster does not support this operation. Please confirm the required cluster status for this API and try again. |
|400 |OperationDenied.KubeconfigStatus |The action has been denied due to wrong kubeconfig status {{statusPhase}}. |The current KubeConfig status does not support this operation. Please wait for five seconds and try again later. |


&nbsp;
