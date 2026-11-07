---
title: "ModifyUniqueResourceTypeVpcEndpointServiceAttributes - Updating the attributes of an RDS-type endpoint service"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/ModifyUniqueResourceTypeVpcEndpointServiceAttributes"
---

Call the ModifyUniqueResourceTypeVpcEndpointServiceAttributes API to modify the configuration of the specified endpoint service.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The PrivateLink feature for RDS type service resource is in beta stage. To call this API, contact your account manager.

* This interface only supports modifying endpoint services associated with RDS type service resources. To modify endpoint services with other types of service resources, please call the [ModifyVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceAttributes) API.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyUniqueResourceTypeVpcEndpointServiceAttributes&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|1EPwiz">必选</span> `Example: ModifyUniqueResourceTypeVpcEndpointServiceAttributes`

Action to execute. Set the value to **ModifyUniqueResourceTypeVpcEndpointServiceAttributes**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|aIt_7F">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ServiceId ** <span data-label="purple"> String </span><span data-api-tag="require|FKbpdm">必选</span> `Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.



**IpAddressVersions.N ** <span data-label="purple"> String </span>`optional` `example: ipv4`

The IP protocol type of the endpoint service.


* ipv4

* IPv6: This value is currently in beta stage. For trial requests, contact your account manager.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">When only <strong>ipv4</strong> is specified, it indicates that the endpoint service will be converted to the IPv4 type and will only provide IPv4 services.</div>


* <div data-tips="true" data-tips-type="default">When both <strong>ipv4</strong> and <strong>ipv6</strong> are specified, it indicates that the endpoint service will be converted to a dual\-stack type, supporting both IPv4 and IPv6 services. The system will automatically assign an IPv6 address to it.</div>


   <div data-tips="true" data-tips-type="default">If you need to specify <strong>IPv6</strong>, ensure the following conditions are met:   </div>
   

   * <div data-tips="true" data-tips-type="default">The IPv6 functionality for the PrivateLink service has been activated.</div>


   * <div data-tips="true" data-tips-type="default">The specified service resource supports dual\-stack.</div>


* <div data-tips="true" data-tips-type="default">Currently, specifying only <strong>IPv6</strong> is not supported.</div>


* <div data-tips="true" data-tips-type="default">If you do not modify this parameter value, its original configuration remains.</div>




**Resource.InstanceId ** <span data-label="purple"> String </span>`optional` `Example: mysql-bp1o94dp5i6ea****`

The ID of the RDS instance to which the RDS type service resource to be added to the endpoint service belongs.

You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances) API to view the ID of the RDS instance.



**Resource.ResourceId ** <span data-label="purple"> String </span><span data-api-tag="require|SaGwpu">必选</span> `Example: mysql-bp1o94dp5i6ea****-cluster-qhwjs67hbmsj****`

The ID of the RDS type service resource to be added to the endpoint service.

You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancedetail) API to obtain the ID of the RDS instance connection endpoint.



**AutoAcceptEnabled ** <span data-label="purple"> Boolean  </span>`optional` `Example: false`

Auto\-accept endpoint connection. Valid values:


* true: The endpoint service automatically accepts endpoint connection requests.

* false: The endpoint service does not automatically accept endpoint connections; you need to manually accept them by calling the [EnableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/EnableVpcEndpointConnection) API.



**ZoneIds.N ** <span data-label="purple"> String  </span>`optional` `Example: cn-guangzhou-a`

The availability zone IDs supported by the endpoint service.

You can call the [DescribePrivateLinkAvailableZones](https://docs.byteplus.com/en/docs/privatelink/DescribePrivateLinkAvailableZones) API to get the Availability Zone IDs.


* Parameter \- N: Indicates the serial number of the Availability Zone, ranging from 1 to 20.

* Separate multiple Availability Zones with ampersands ( & ).



**Description ** <span data-label="purple"> String  </span>`optional` `Example: endpoint service`

Description of the endpoint service.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.

* If you do not modify this parameter value, its original configuration remains.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyUniqueResourceTypeVpcEndpointServiceAttributes&Version=2020-04-01&ServiceId=epsvc-2fe630gurkl37k5gfuy33****&Resource.ResourceId=mysql-bp1o94dp5i6ea****-cluster-qhwjs67hbmsj**** HTTP/1.1
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
        "Action": "ModifyUniqueResourceTypeVpcEndpointServiceAttributes",
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
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidEndpointService.InvalidStatus |The specified EndpointService is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |ErrInterfaceNotSupportedResourceType |The Interface does not support the resource type. |The endpoint service API does not support this service resource type. |
|400 |ErrPrivateLinkServiceNotSupportedZone |The PrivateLink service does not support the zone. |The VPC endpoint service does not support adding service resources from this Availability Zone. |
|400 |InvalidServiceResource.InUse |The specified service resource is in use. |Service resource is in use. |
|400 |InvalidEndpointService.InvalidLock |The operation is refused by the endpoint service. |This operation is not supported for the endpoint service. |
|400 |InvalidServiceResource.Malformed |The specified ServiceResource is malformed. |The specified ServiceResource parameter format is invalid. |
|400 |InvalidServiceZone.InUse |The specified ServiceZone is in use. |The endpoint service availability zone is currently in use. |
|400 |InvalidZone.Conflict |The specified zone is duplicated. |Duplicate Availability Zones specified. |
|400 |InvalidZone.Malformed |The specified Zone is malformed. |The specified zone parameter format is invalid. |
|400 |InvalidIpAddressVersions.Conflict |The specified IpAddressVersions parameter is duplicated. |The specified IpAddressVersions are duplicated. |
|400 |InvalidIpAddressVersions.Malformed |The specified IpAddressVersions is malformed. |The specified IpAddressVersions parameter format is invalid. |
|400 |InvalidModifyConnectedDualStackEpsvcIPVersion.Conflict |There are still existing dualstack endpoints on the specified EndpointService instance. |The modification is temporarily unavailable as there are still existing connections on the current endpoint service. |
|400 |InvalidServiceResourceStatus.IPVersionMismatch |The specified service resource can not support the EndpointService ipAddressVersion that you want. |The current service resource does not support the specified endpoint service IP address type. |
|400 |InvalidLocation.Intercepted |The specified action has been intercepted by location. |The current account does not have operation permissions in the specified region. Please request to be added to the allowlist. |
|400 |InvalidModifyConnectedEpsvcIPVersion.Conflict |There are still existing connected endpoints on the specified EndpointService instance. |The modification is temporarily unavailable as there are still existing connections on the current endpoint service. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
|404 |InvalidServiceResource.NotFound |The specified ServiceResource does not exist. |The specified service resource does not exist. |
