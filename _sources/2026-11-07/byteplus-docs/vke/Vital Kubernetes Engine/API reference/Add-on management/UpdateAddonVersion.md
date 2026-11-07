---
title: "UpdateAddonVersion"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/UpdateAddonVersion"
---

Update the version of a specified add\-on in a specified cluster.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* Before calling this API, first call the [ListSupportedAddons](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons) API to obtain the values of parameters (such as Version) for the specified add\-on. This helps reduce update failures.

* This API is asynchronous. When the API call returns success, the add\-on is in the `{Updating, [Progressing]}` state until the update is executed successfully and the add\-on enters the `{Running, [Ok]}` state. Call the [ListAddons](https://docs.byteplus.com/en/docs/vke/ListAddons) API to obtain the current status of the add\-on and view whether the add\-on version has been updated successfully.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UpdateAddonVersion&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateAddonVersion&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the request parameters for the API. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateAddonVersion |The API name. The name of the current API is `UpdateAddonVersion`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ClusterId |String |Yes |cc5silum\*\*\*\* |The ID of the cluster to which the add\-on to be updated belongs.<br><br>Cluster IDs can be fetched by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The cluster must be in the <code>{Running,[Ok]}</code> or <code>{Updating, [Progressing]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListClusters">ListClusters</a> API to obtain the current status of the cluster.</div><br> |
|Name |String |Yes |ingress\-nginx |The name of the add\-on to be updated.<br><br>You can call the [ListAddons](https://docs.byteplus.com/en/docs/vke/ListAddons) API to obtain the add\-on name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The add\-on must be in the <code>{Running, [*]}</code> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListAddons">ListAddons</a> API to obtain the current status of the add\-on.</div><br> |
|Version |String |Yes |v0.44.0 |The target version (the version to which the add\-on will be updated).<br><br>You can call the [ListSupportedAddons](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons) API to obtain the available target versions. |
|ClientToken |String |no |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=UpdateAddonVersion&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
        "ClusterId": "cc5si****",
        "Name": "ingress-nginx",
        "Version": "v0.44.0",
        "ClientToken": "BC028527-33B9-4990-A633-84E9F9******"
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
                "RequestId": "0216353****",
                "Action": "UpdateAddonVersion",
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


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied.ClusterStatus |The action has been denied due to wrong cluster status {{statusPhase}} and [{{statusConditions}}]. |The current status of the specified cluster does not support this action. Please confirm the required cluster status for this API and try again later. |
|400 |OperationDenied.AddonStatus |The action has been forbidden due to wrong addon status {{statusPhase}} and [{{statusConditions}}]. |The current add\-on status does not support an add\-on update. Please confirm the required add\-on status for this API and try again later. |
|400 |OperationDenied.GracefulUpgrade |The addon does not support graceful upgrade from the current version to the target version. |The add\-on does not support graceful upgrade from the current version to the target version.<br><br>Please call the [ListSupportedAddons](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons) API to obtain the available target versions of the add\-on and upgrade sequentially. |
|400 |NotSupported.{{parameter}} |The specified {{resourceType}} {{resourceContent}} is not supported. |The specified add\-on does not support upgrading. Please call the [ListSupportedAddons](https://docs.byteplus.com/en/docs/vke/ListSupportedAddons) API to confirm the list of supported add\-ons and try again later. |


&nbsp;
