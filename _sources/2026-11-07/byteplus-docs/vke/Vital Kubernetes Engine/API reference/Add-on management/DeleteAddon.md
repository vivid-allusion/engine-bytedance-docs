---
title: "DeleteAddon"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/DeleteAddon"
---

Remove a specified add\-on from a specified cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* Before calling this API, first call the [ListSupportedAddons](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons) API to query details of the specified add\-on.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Required add\-ons cannot be uninstalled.   </div>
   

* This API is asynchronous. When this API returns success, the add\-on is in the `{Deleting, [Progressing]}` state. A successful API response does not indicate that the add\-on has been uninstalled. You need to call the [ListAddons](https://docs.byteplus.com/en/docs/vke/ListAddons) API to check whether the add\-on exists in the specified cluster. If it is not found, the add\-on has been successfully uninstalled.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=DeleteAddon&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteAddon&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the request parameters for the API. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteAddon |The API name. The name of the current API is `DeleteAddon`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |cc5silumrsfeqxxxx |The ID of the cluster to which the add\-on to be uninstalled belongs.<br><br>Cluster IDs can be queried by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in the <code>{Running,[Ok]}</code> or <code>{Updating, [Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to view the current status of the cluster.</div><br> |
|Name |String |Yes |ingress\-nginx |The name of the add\-on to be uninstalled.<br><br>You can call the [ListAddons](https://docs.byteplus.com/en/docs/vke/ListAddons) API to obtain the add\-on name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The add\-on must <strong>not be in the </strong><code>{Creating, [Progressing]}</code>, <code>{Deleting, [Progressing]}</code>, or <code>{Failed, [ClusterNotRunning]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListAddons">ListAddons</a> API to obtain the current status of the add\-on.</div><br> |
|RetainResources |Array of String |no |["Crd"] |Resources to be retained when deleting the add\-on. Values:<br><br><br>* An empty value (default) deletes all associated resources.<br><br>    &nbsp;<br><br>* **Crd**: Retains the CRD (Custom Resource Definition) resources when deleting the add\-on. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST /?Action=DeleteAddon&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
        "ClusterId": "cc5silumrsf******",
        "Name": "ingress-nginx",
        "RetainResources": ["Crd"]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

There are no proprietary response parameters for this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type:application/json
{
        "ResponseMetadata": {
                "RequestId": "021635330810134****",
                "Action": "DeleteAddon",
                "Version": "2022-05-12",
                "Service": "vke",
                "Region": "cn-beijing"
        },
        "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. Refer to the [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) topic for details.


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |OperationDenied.ClusterStatus |The action has been denied due to wrong cluster status {{statusPhase}} and [{{statusConditions}}]. |The current status of the specified cluster does not support this action. Please confirm the required cluster status for this API and try again later. |
|400 |OperationDenied.AddonStatus |The action has been forbidden due to wrong addon status {{statusPhase}} and [{{statusConditions}}]. |The current add\-on status does not support updating the add\-on configuration. Please confirm the required add\-on status for this API and try again later. |
|400 |OperationDenied.RequiredAddon |It is forbidden to delete required addon. |This add\-on is required by the system and cannot be uninstalled. |
