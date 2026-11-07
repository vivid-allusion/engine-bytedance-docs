---
title: "DeleteVirtualNode"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/DeleteVirtualNode"
---

Delete a specified virtual node.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta · Apply for Trial</strong></a>]: APIs related to virtual nodes are in the <strong>beta</strong> phase. To use these APIs, submit an application.</div>


<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* This is an asynchronous API. When this API returns a success message, the virtual node will be in the `{Deleting, [Progressing]}` state. However, the return of a success message does not indicate that the node will be deleted ultimately. You can call the [ListVirtualNodes](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes) API to check whether the virtual node exists. If you cannot query the node, the virtual node has been deleted.

* The virtual node can be deleted only if all VCI pods on the virtual node have been deleted.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=DeleteVirtualNode&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to use public parameters. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteVirtualNode |The API name. The name of the current API is `DeleteVirtualNode`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Id |String |Yes |v73mhao7vj0g\*\*\*\*\*\*\*\* |The ID of the virtual node.<br><br>You can call the [ListVirtualNodes](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes) API to obtain the virtual node ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The virtual node must be in one of the following states:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Running,[*]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Failed, [*]}</code></div><br><br><br>   <div data-tips="true" data-tips-type="warning">You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListVirtualNodes">ListVirtualNodes</a> API to view the current status of the virtual node.   </div><br>    |


&nbsp;


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteVirtualNode |The API name. The name of the current API is `DeleteVirtualNode`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Id |String |Yes |v73mhao7vj0g\*\*\*\*\*\*\*\* |The ID of the virtual node.<br><br>You can call the [ListVirtualNodes](https://docs.byteplus.com/en/docs/vke/ListVirtualNodes) API to obtain the virtual node ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The virtual node must be in one of the following states:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Running,[*]}</code></div><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>{Failed, [*]}</code></div><br><br><br>   <div data-tips="true" data-tips-type="warning">You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListVirtualNodes">ListVirtualNodes</a> API to view the current status of the virtual node.   </div><br>    |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=DeleteVirtualNode&Version=2022-05-12 HTTP/1.1
Content-Type:application/json

{
    "Id": "vck4gdidle********"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

There are no response parameters proprietary to this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "0216353********",
        "Action": "DeleteVirtualNode",
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
|400 |OperationDenied.VirtualNodeStatus |The operation has been denied due to wrong virtual node status {{statusPhase}} and [{{statusConditions}}]. |The virtual node in the current state does not support this operation. Check the virtual node state required by this API and try again later. |
|400 |OperationDenied.ExistingPodInstances |The operation has been denied because the virtual node still has pod instances. |Pods still exist on the specified virtual node. Therefore, this operation is not supported. Delete the related pods and try again later. |


&nbsp;
