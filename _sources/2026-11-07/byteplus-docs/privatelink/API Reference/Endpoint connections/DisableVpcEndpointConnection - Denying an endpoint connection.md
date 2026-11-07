---
title: "DisableVpcEndpointConnection - Denying an endpoint connection"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DisableVpcEndpointConnection"
---

Call the DisableVpcEndpointConnection API to reject the specified endpoint connection.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

During the seamless replacement of service resources, the endpoint service retains existing endpoint connections and temporarily does not respond to disconnection requests.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DisableVpcEndpointConnection&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|X12Ib1">必选</span> `Example: DisableVpcEndpointConnection`

Action to execute. Set the value to **DisableVpcEndpointConnection**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|amRFeA">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**EndpointId ** <span data-label="purple"> String  </span><span data-api-tag="require|jhRzu8">必选</span> `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.



**ServiceId ** <span data-label="purple"> String  </span><span data-api-tag="require|X7ntng">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



**ReplacingResource ** <span data-label="purple"> Boolean  </span>`optional` `Example: false`

Whether to operate on the endpoint connection that is undergoing seamless service resource replacement.


* true: Yes, perform a seamless replacement​​ of the old service resource for the endpoint connection.

* false: No, then reject the specified endpoint connection.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If this parameter is empty, the specified endpoint connection is rejected.</div>




**ZoneId ** <span data-label="purple"> String </span>`optional` `Example: cn-guangzhou-a`

ID of the endpoint Availability Zone.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter must be configured when the ReplacingResource parameter is set to <strong>true</strong>.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DisableVpcEndpointConnection&Version=2020-04-01&EndpointId=ep-273yuq6q7bgn47fap8squ****&ServiceId=epsvc-2fe630gurkl37k5gfuy33**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DisableVpcEndpointConnection",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Here, XXX represents the name of the missing parameter.</div><br> |
|400 |InvalidEndpointService.InvalidLock |The operation is refused by the endpoint service. |This operation is not supported for the endpoint service. |
|400 |UnsupportedOperation.ConnectionStatus |The connection status does not support operation. |The current connection state does not support this operation. |
|400 |InvalidReplaceResource.Deleted |The new replacement resource has been deleted, therefore you are unable to disconnect the service. |The service resource being replaced for the specified endpoint connection has been deleted, therefore the service resource cannot be disconnected. |
|400 |InvalidEndpoint.ServiceMisMatch |The specified endpoint and service don't match. |The specified endpoint and endpoint service do not match. |
|400 |InvalidEndpoint.InvalidStatus |The specified endpoint is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |InvalidEndpointZone.InvalidStatus |The specified EndpointZone is not in the correct status for the request. |The specified endpoint availability zone is in a status that cannot respond to this request. |
|400 |UnsupportedOperation.ReplaceResourceConflict |The specified endpoint connection has not completed the service resource replacement. Please disconnect the service resource first. |The specified endpoint connection has not yet completed the service resource replacement. Please disconnect the service resource first. |
|404 |InvalidReplaceResource.NotFound |The specified endpoint connection has not replaced the service resource, so you cannot disconnect the service resource. |The specified endpoint connection has not replaced its service resource, therefore the service resource cannot be disconnected. |
|404 |InvalidEndpointZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|404 |InvalidEndpoint.NotFound |The specified endpoint does not exist. |The specified endpoint does not exist. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
