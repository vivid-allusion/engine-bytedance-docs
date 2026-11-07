---
title: "ModifyVpcEndpointAttributes - Modifying the endpoint attribute"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointAttributes"
---

Call the ModifyVpcEndpointAttributes API to modify the specified endpoint information. For operational instructions and precautions, see [Modifying an endpoint](https://docs.byteplus.com/en/docs/privatelink/Modifying-basic-information-on-endpoints).

> When calling this API to modify an endpoint, the state of the endpoint instance transitions as follows: Available \> Pending \> Available.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyVpcEndpointAttributes&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|RJKLqJ">必选</span> `Example: ModifyVpcEndpointAttributes`

Action to execute. Set the value to **ModifyVpcEndpointAttributes**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|2pX8Y3">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**EndpointId ** <span data-label="purple">String</span> <span data-api-tag="require|3z6qDo">必选</span>`Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.



**EndpointName ** <span data-label="purple"> String  </span>`optional` `Example: endpoint-02`

Name of the endpoint.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.



**IpAddressVersions.N ** <span data-label="purple">String</span> `optional` `Example: ipv4`

The IP protocol type of the interface endpoint.


* ipv4

* ipv6: This value is currently in beta stage. For trial requests, contact your account manager.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">When only <strong>ipv4</strong> is specified, it indicates that the interface VPC endpoint will be converted to the IPv4 type, and it will only handle IPv4 requests.</div>


* <div data-tips="true" data-tips-type="default">When both <strong>ipv4</strong> and <strong>ipv6</strong> are specified, it indicates that the interface VPC endpoint will be converted to a dual\-stack type, supporting both IPv4 and IPv6 requests. The system will automatically assign an IPv6 address to it.</div>


   <div data-tips="true" data-tips-type="default">If you need to specify <strong>IPv6</strong>, ensure the following conditions are met:   </div>
   

   * <div data-tips="true" data-tips-type="default">You have been granted allowlist permissions for the dual\-stack feature of PrivateLink.</div>


   * <div data-tips="true" data-tips-type="default">The subnet to which the interface endpoint belongs has the IPv6 CIDR block enabled.</div>


   * <div data-tips="true" data-tips-type="default">The endpoint service associated with the interface endpoint is of the dual\-stack type.</div>


* <div data-tips="true" data-tips-type="default">Currently, specifying only <strong>IPv6</strong> is not supported.</div>




**PrivateDNSEnabled ** <span data-label="purple"> Boolean </span>`optional` `Example: false`

Enable private DNS name.


* false: Disable.

* true: Enable.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The private DNS name of the VPC endpoint service must have a verification status of <strong>verified</strong> before it can be enabled. You can call the <a href="https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceAttributes">DescribeVpcEndpointServiceAttributes</a> API to view the private DNS name verification status of the endpoint service.</div>


* <div data-tips="true" data-tips-type="default">When enabled, the private DNS name of the endpoint defaults to the private DNS name of its associated endpoint service.</div>




**Description ** <span data-label="purple"> String </span>`optional` `Example: This endpoint is for test.`

The description of the endpoint.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyVpcEndpointAttributes&Version=2020-04-01&EndpointId=ep-273yuq6q7bgn47fap8squ****&EndpointName=endpoint-02 HTTP/1.1
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
        "Action": "ModifyVpcEndpointAttributes",
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
|400 |InvalidEndpoint.InvalidStatus |The specified endpoint is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidEndpointService.InvalidLock |The operation is refused by the endpoint service. |This operation is not supported for the endpoint service. |
|400 |InvalidPrivateDNS.UnsupportedOperation |The request on the specified PrivateDNS is denied due to the PrivateDNS is disabled. |The request was rejected because the Private DNS feature is not enabled. |
|400 |ErrPrivateZoneExisted |The vpc and the private dns have created the private zone. |Private DNS resolution has already been configured for this VPC and DNS domain. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |The available IPs under the specified subnet are insufficient. |
|400 |InvalidEndpointZoneIPVersion.AddressMismatch |The specified EndpointZone AddressIPVersion and address are not matched. |The specified availability zone address for the VPC endpoint does not match its IP address type. |
|400 |InvalidIpAddressVersions.Conflict |The specified IpAddressVersions parameter is duplicated. |The specified IpAddressVersions are duplicated. |
|400 |InvalidIpAddressVersions.Malformed |The specified IpAddressVersions is malformed. |The specified IpAddressVersions parameter format is invalid. |
|400 |InvalidEndpointIpAddressVersions.EndpointServiceMisMatch |The IpAddressVersions of associated EndpointService and Endpoint mismatch. |The IP address type of the endpoint does not match the associated endpoint service. |
|400 |InvalidSubnet.VpcMisMatch |The specified subnet and vpc don't match. |The specified VPC and subnet do not match. |
|400 |InvalidSubnet.ZoneMisMatch |The specified subnet and available zone don't match. |The specified Availability Zone and subnet do not match. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |InvalidEndpoint.ServiceDeleted |The specified endpoint's service has been deleted for the request. |The specified endpoint's associated endpoint service has been deleted, and the request cannot be processed. |
|400 |PrivateDNSNameConflictwithPrivateZone |The specified private DNS name already exists private zone in the VPC. |The specified private DNS name already exists for PrivateZone within this VPC. |
|400 |InvalidEndpointZoneIPVersion.SubnetMismatch |The specified EndpointZone Subnet and Endpoint IPAddressVersion are not matched. |The specified availability zone subnet for the VPC endpoint does not match its IP address type. |
|403 |Forbidden.IPv6EndpointToOthers |The IPv6 Endpoint can not be modified to other IP version. |Endpoints of the IPv6 type are not allowed to have their IP address type changed. |
|403 |Forbidden.ToIPv6Endpoint |The Endpoint can not be modified to IPv6 from other IP version. |Endpoints of other IP address types cannot be converted to the IPv6 type. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
|404 |InvalidEndpoint.NotFound |The specified endpoint does not exist. |The specified endpoint does not exist. |
|409 |InvalidVpcPrivateDNSName.Conflict |The specified PrivateDNSName in single vpc and single endpoint service already exists. |The specified private DNS name already exists under the same VPC and the same endpoint service. |
|500 |PrivateZoneCreateFailed |The private zone create failed. |PrivateZone creation failed. |
|500 |PrivateZoneQueryFailed |Failed to query private zone. |Failed to query PrivateZone. |
|500 |AssignIPv6AddressFailed |Failed to assign ipv6 address. |Failed to assign an IPv6 address. |
