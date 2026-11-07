---
title: "ModifyVpcEndpointServiceAttributes - Updating the endpoint service attributes"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceAttributes"
---

Call the ModifyVpcEndpointServiceAttributes API to modify the configuration of a specified endpoint service.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

When a VPC endpoint service has private DNS enabled and is already associated with VPC endpoints that also have private DNS enabled, modifications to the parameters `PrivateDNSEnabled`, `PrivateDNSType`, and `PrivateDNSName` are not supported.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyVpcEndpointServiceAttributes&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|3R6w0R">必选</span> `Example: ModifyVpcEndpointServiceAttributes`

Action to execute. Set the value to **ModifyVpcEndpointServiceAttributes**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|AubXAL">必选</span> `Example: 2020-04-01`

Current API version is **2020\-04\-01**.



**ServiceId ** <span data-label="purple">String </span><span data-api-tag="require|hITf2v">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



**IpAddressVersions.N ** <span data-label="purple">String </span>`optional` `Example: ipv4`

The IP protocol type of the endpoint service.


* ipv4

* ipv6: This value is currently in beta stage. For trial requests, contact your account manager.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When only <strong>ipv4</strong> is specified, it indicates that the endpoint service will be converted to the IPv4 type and will only provide IPv4 services.</div>


* <div data-tips="true" data-tips-type="tip">When both <strong>ipv4</strong> and <strong>ipv6</strong> are specified, it indicates that the endpoint service will be converted to a dual\-stack type, supporting both IPv4 and IPv6 services. The system will automatically assign an IPv6 address to it.</div>


   <div data-tips="true" data-tips-type="tip">If you need to specify <strong>ipv6</strong>, ensure the following conditions are met:   </div>
   

   * <div data-tips="true" data-tips-type="tip">The IPv6 functionality for the PrivateLink service has been activated.</div>


   * <div data-tips="true" data-tips-type="tip">The specified service resource supports dual\-stack.</div>


* <div data-tips="true" data-tips-type="tip">Currently, specifying only <strong>IPv6</strong> is not supported.</div>


* <div data-tips="true" data-tips-type="tip">If you do not modify this parameter value, its original configuration remains.</div>




**AutoAcceptEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Auto\-accept endpoint connection.


* true: The endpoint service automatically accepts endpoint connection requests.

* False: The endpoint service does not automatically accept endpoint connections; you need to manually accept them by calling the [EnableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/EnableVpcEndpointConnection) API.



**PrivateDNSEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Whether to enable private DNS name for the VPC endpoint service.


* false: Not enable.

* true: Enabled.



**PrivateDNSType ** <span data-label="purple">String </span>`optional` `Example: public`

Domain type of the private DNS name.


* Public: Internet.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect when the <code>PrivateDNSEnabled</code> parameter is set to <strong>true</strong>.</div>




**PrivateDNSName ** <span data-label="purple">String </span>`optional` `Example: www.example.com`

Private DNS name refers to the custom domain name you wish to use when accessing the service via PrivateLink, and it only supports internet domain names.

Internet domain names cannot be set to those already configured for internal (global) resolution, nor to domain names used for PrivateLink (including endpoint service domain names and endpoint domain names).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This parameter must be specified when the <code>PrivateDNSEnabled</code> parameter is set to <strong>true</strong>.</div>


* <div data-tips="true" data-tips-type="tip">If a wildcard domain name such as <code>*.www.example.com</code> is provided, both the wildcard domain and its root domain <code>www.example.com</code> will be supported for resolution.</div>




**Description ** <span data-label="purple">String </span>`optional` `Example: endpoint service`

Description of the endpoint service.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.

* If you do not modify this parameter value, its original configuration remains.



**AddSupportedRegions.N ** <span data-label="purple">String </span>`optional` `Example: cn-beijing`

Add regions where the endpoint service is published.



**RemoveSupportedRegions.N ** <span data-label="purple">String </span>`optional` `Example: cn-shanghai`

Remove regions where the endpoint service is published.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyVpcEndpointServiceAttributes&Version=2020-04-01&ServiceId=epsvc-2fe630gurkl37k5gfuy33**** HTTP/1.1
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
        "Action": "ModifyVpcEndpointServiceAttributes",
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
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request is missing a required parameter. Ensure that your request includes all required parameters, such as XXX.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Here, XXX represents the name of the missing parameter.</div><br> |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidEndpointService.InvalidStatus |The specified EndpointService is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |ErrInterfaceNotSupportedResourceType |The Interface does not support the resource type. |The endpoint service API does not support this service resource type. |
|400 |InvalidPrivateDNSEnable.InUse |The specified PrivateDNS is being occupied by Endpoint of the EndpointService. |The specified private DNS is currently in use by endpoints under the endpoint service. |
|400 |InvalidPrivateDNSEnabled.PrivateDNSNameMismatch |The specified PrivateDNSEnabled and PrivateDNSName are mismatched. |The specified parameter for whether private DNS is enabled does not match the provided private DNS name. |
|400 |InvalidPrivateDNSName.Malformed |The specified PrivateDNSName is malformed. |The specified PrivateDNSName parameter format is invalid. |
|400 |InvalidEndpointService.InvalidLock |The operation is refused by the endpoint service. |This operation is not supported for the endpoint service. |
|400 |InvalidPrivateDNSEnabled.PrivateDNSTypeMismatch |The specified PrivateDNSEnabled and PrivateDNSType are mismatched. |The specified parameter PrivateDNSEnabled does not match the PrivateDNSType. |
|400 |InvalidPrivateDNSType.Malformed |The specified PrivateDNSType is malformed. |The specified PrivateDNSType parameter format is invalid. |
|400 |ErrPrivateLinkServiceNotSupportedZone |The PrivateLink service does not support the zone. |The VPC endpoint service does not support adding service resources from this Availability Zone. |
|400 |InvalidIpAddressVersions.Conflict |The specified IpAddressVersions parameter is duplicated. |The specified IpAddressVersions is duplicated. |
|400 |InvalidIpAddressVersions.Malformed |The specified IpAddressVersions is malformed. |The specified IpAddressVersions parameter format is invalid. |
|400 |InvalidModifyConnectedDualStackEpsvcIPVersion.Conflict |There are still existing dualstack endpoints on the specified EndpointService instance. |The modification is temporarily unavailable as there are still existing connections on the current endpoint service. |
|400 |InvalidServiceResource.Malformed |The specified ServiceResource is malformed. |The specified ServiceResource parameter format is invalid. |
|400 |InvalidServiceResourceStatus.IPVersionMismatch |The specified service resource can not support the EndpointService ipAddressVersion that you want. |The current service resource does not support the specified endpoint service IP address type. |
|400 |InvalidModifyConnectedEpsvcIPVersion.Conflict |There are still existing connected endpoints on the specified EndpointService instance. |The modification is temporarily unavailable as there are still existing connections on the current endpoint service. |
|400 |InvalidPrivateDNSType.ServiceOwnerMismatch |The specified service owner can not support the EndpointService PrivateDNS type that you want. |The specified private DNS type is not supported by the current service owner. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
|404 |InvalidServiceResource.NotFound |The specified ServiceResource does not exist. |The specified service resource does not exist. |
