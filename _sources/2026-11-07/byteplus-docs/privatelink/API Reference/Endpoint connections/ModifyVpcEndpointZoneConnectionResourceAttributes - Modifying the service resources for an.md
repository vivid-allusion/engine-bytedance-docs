---
title: "ModifyVpcEndpointZoneConnectionResourceAttributes - Modifying the service resources for an endpoint connection"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointZoneConnectionResourceAttributes"
---

Call the ModifyVpcEndpointZoneConnectionResourceAttributes API to replace the service resource of an endpoint connection.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The PrivateLink service support for replacing service resources is in beta stage. For trial requests, contact your account manager.</div>


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyVpcEndpointZoneConnectionResourceAttributes&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|iTuCHK">必选</span> `Example: ModifyVpcEndpointZoneConnectionResourceAttributes`

Action to execute. Set the value to **ModifyVpcEndpointZoneConnectionResourceAttributes**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|bvNxPv">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**EndpointId ** <span data-label="purple">String </span><span data-api-tag="require|28jo9a">必选</span> `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.



**ServiceId ** <span data-label="purple">String </span><span data-api-tag="require|MxsVTy">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



**ResourceReplaceMode ** <span data-label="purple">String </span><span data-api-tag="require|OnFtmX">必选</span> `Example: grace`

Mode for replacing the service resource.


* grace: Seamless replacement​​. The current endpoint network interface maintains its connection to the old service resource. The endpoint creates a new ENI to establish a connection to the new service resource. New traffic is directed to the new connection by default. After the old connection has no traffic, you need to call the [DisableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/DisableVpcEndpointConnection) API to manually disconnect the old connection.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Seamless replacement adds a new network interface on the endpoint to establish the connection. Evaluate the business impact carefully before proceeding.</div>



* force: Replace now. The endpoint network interface immediately disconnects from the original service resource and establishes a connection to the new one.



**ZoneId ** <span data-label="purple">String </span><span data-api-tag="require|KXto6O">必选</span> `Example: cn-guangzhou-a`

The availability zone ID of the replaced service resource.



**ResourceId ** <span data-label="purple">String </span><span data-api-tag="require|GjUVpK">必选</span> `Example: clb-y1u2q56redg5tgfadfsur****`

Replaced service resource ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyVpcEndpointZoneConnectionResourceAttributes&Version=2020-04-01&EndpointId=ep-273yuq6q7bgn47fap8squ****&ServiceId=epsvc-2fe630gurkl37k5gfuy33****&ResourceReplaceMode=grace&ZoneId=cn-guangzhou-a&ResourceId=clb-y1u2q56redg5tgfadfsur**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "Action": "ModifyVpcEndpointZoneConnectionResourceAttributes",
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


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |The available IPs under the specified subnet are insufficient. |
|400 |InvalidEndpoint.InvalidStatus |The specified endpoint is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |InvalidEndpoint.ServiceMisMatch |The specified endpoint and service don't match. |The specified endpoint and endpoint service do not match. |
|400 |InvalidEndpointService.InvalidLock |The operation is refused by the endpoint service. |This operation is not supported for the endpoint service. |
|400 |InvalidEndpointZone.InvalidStatus |The specified EndpointZone is not in the correct status for the request. |The specified endpoint availability zone is in a status that cannot respond to this request. |
|400 |InvalidEndpointZoneIPVersion.AddressMismatch |The specified EndpointZone AddressIPVersion and address are not matched. |The specified availability zone address for the VPC endpoint does not match its IP address type. |
|400 |InvalidFusionClusterEndpoint.ResourceNotMatch |The endpoint zone of the fusion cluster is not allowed to replace the load balancer of non\-fusion cluster. |The specified CLB instance is not an integrated cluster instance and does not support being replaced with an endpoint availability zone of the integrated cluster. |
|400 |InvalidReplaceResource.TypeInconsistent |The types of specified resource and the replaced resource are inconsistent. |The specified service resource type does not match the type of the service resource being replaced. |
|400 |InvalidReplaceResource.ZoneMismatch |The available zones of specified resource and the replaced resource are not matched. |The availability zone of the specified service resource does not match that of the service resource being replaced. |
|400 |InvalidResource.Conflict |The specified resource is duplicated. |The specified resource is duplicated. |
|400 |InvalidResourceReplaceMode.Malformed |The specified ResourceReplaceMode is malformed. |The specified service resource switch pattern is invalid. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType parameter format is invalid. |
|400 |InvalidServiceResourceType.Malformed |The specified ServiceResourceType is malformed. |The specified ServiceResourceType parameter format is invalid. |
|400 |InvalidServiceType.Malformed |The specified ServiceType is malformed. |The format of specified ServiceType is invalid. |
|400 |InvalidSubnet.VpcMisMatch |The specified subnet and vpc don't match. |The specified VPC and subnet do not match. |
|400 |InvalidSubnet.ZoneMisMatch |The specified subnet and available zone don't match. |The specified Availability Zone and subnet do not match. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |UnsupportedOperation.ReplaceResourceConflict |The specified endpoint connection has not completed the service resource replacement. Please disconnect the service resource first. |The specified endpoint connection has not yet completed the service resource replacement. Please disconnect the service resource first. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidEndpoint.NotFound |The specified endpoint does not exist. |The specified endpoint does not exist. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
|404 |InvalidEndpointZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|404 |InvalidServiceResource.NotFound |The specified ServiceResource does not exist. |The specified service resource does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|500 |NetworkInterfaceCreateFailed |The network interface create failed. |Failed to create the network interface in the availability zone. |
