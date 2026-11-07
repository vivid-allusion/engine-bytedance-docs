---
title: "DescribeVpcEndpointZones - Querying the list of endpoint availability zones"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointZones"
---

Call the DescribeVpcEndpointZones API to query the availability zones added to the specified endpoint.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcEndpointZones&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|TZX7Xv">必选</span> `Example: DescribeVpcEndpointZones`

Action to execute. Set the value to **DescribeVpcEndpointZones**.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|oQlzZ0">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**EndpointId ** <span data-label="purple"> String  </span><span data-api-tag="require|dtVqWI">必选</span> `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.



**PageNumber** <span data-label="purple">Integer</span> `optional` `Example: 1`

Page number of the list. Default: 1.



**PageSize ** <span data-label="purple"> Integer  </span>`optional` `Example: 10`

The number of entries per page in a pagination query. Maximum: 100. Default: 10.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



**PageNumber** <span data-label="purple">Integer</span> `optional` `Example: 1`

The current page number.



**PageSize ** <span data-label="purple"> Integer  </span>`optional` `Example: 10`

Number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple"> Integer </span>`optional` `Example: 2`

The total number of endpoint services matching the specified conditions.



**EndpointZones ** <span data-label="purple"> Object[] </span>`optional` `Example: -`

Details of the endpoint availability zone.


**ZoneId ** <span data-label="purple"> String </span>`optional` `Example: cn-guangzhou-a`

ID of the endpoint availability zone.



**ZoneDomain ** <span data-label="purple"> String </span>`optional` `Example: ep-273yuq6q7bgn47fap8squ****.cn-guangzhou-a.epsvc-273yuqembrojk7fap8sbf****.cn-guangzhou.privatelink.volces.com`

Domain name of the endpoint availability zone. Format: <Endpoint ID\>.<Availability zones ID\>.<Endpoint Service ID\>.<region ID\>.privatelink.volces.com.



**ZoneStatus ** <span data-label="purple"> String </span>`optional` `Example: Connected`

Status of the endpoint availability zone.


* PendingAcceptance: Waiting for connection

* Connecting: Connecting.

* Connected: Connected.

* Disconnecting: Disconnecting.

* rejected: connection denied.

* Failed: Connection failed.



**ServiceStatus ** <span data-label="purple"> String </span>`optional` `Example: Active`

Service status of the endpoint IPv4 address.


* Active: Normal.

* Inactive: Abnormal.



**Ipv6ServiceStatus ** <span data-label="purple"> String  </span>`optional` `Example: Active`

Service status of the endpoint IPv6 address.


* Active: Normal.

* Inactive: Abnormal.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is not returned if the endpoint only supports IPv4.</div>




**SubnetId ** <span data-label="purple"> String </span>`optional` `Example: subnet-2744ts087kglc7fap8tu6****`

The ID of the subnet to which the endpoint network interface belongs.



**NetworkInterfaceId ** <span data-label="purple"> String </span>`optional` `Example: eni-273w2q67fwq9s7fap8t1a****`

ID of the endpoint network interface.

If undergoing seamless service resource replacement, this represents the ID of the endpoint network interface connected to the service resource being replaced.



**NetworkInterfaceIP ** <span data-label="purple"> String  </span>`optional` `Example: 192.XX.XX.3`

Private IPv4 address of the endpoint network interface.

If undergoing seamless service resource replacement, this represents the IPv4 address of the endpoint network interface connected to the service resource being replaced.



**NetworkInterfaceIpv6 ** <span data-label="purple"> String </span>`optional` `Example: 2408::153:3921:XX:XX:7b12:1c5f`

Private IPv6 address of the endpoint network interface.

If undergoing seamless service resource replacement, this represents the IPv6 address of the endpoint network interface connected to the service resource being replaced.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is not returned if the endpoint only supports IPv4.</div>




**ReplacedNetworkInterfaceId ** <span data-label="purple"> String  </span>`optional` `Example: eni-273w2q67fwq9s7fap8t1a****`

The ID of the endpoint network interface used to connect to the new service resource.

If the endpoint is not undergoing seamless service resource replacement, this parameter returns empty.



**ReplacedNetworkInterfaceIp ** <span data-label="purple"> String </span>`optional` `Example: 192.XX.XX.4`

The IPv4 address of the endpoint network interface used to connect to the new service resource.

If the endpoint is not undergoing seamless service resource replacement, this parameter returns empty.



**ReplacedNetworkInterfaceIpv6 ** <span data-label="purple"> String </span>`optional` `Example: 2408::153:3921:XX:XX:7b12:1acc`

The IPv6 address of the endpoint network interface used to connect to the new service resource.

If the endpoint is not undergoing seamless service resource replacement, this parameter returns empty.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This parameter is not returned if the endpoint only supports IPv4.</div>





<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeVpcEndpointZones&Version=2020-04-01&EndpointId=ep-273yuq6q7bgn47fap8squ**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "Action": "DescribeVpcEndpointZones",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "PageNumber": 1,
        "PageSize": 10,  
        "TotalCount": 2,
        "EndpointZones": [
            {
                "ZoneId": "cn-guangzhou-a",
                "ZoneDomain": "ep-273yuq6q7bgn47fap8squ****.cn-guangzhou.epsvc-273yuqembrojk7fap8sbf****.cn-guangzhou.privatelink.volces.com",
                "ZoneStatus": "Connected",
                "ServiceStatus": "Active",
                "SubnetId": "subnet-2744ts087kglc7fap8tu6****",
                "NetworkInterfaceId": "eni-273w2q67fwq9s7fap8t1a****",
                "NetworkInterfaceIP": "192.XX.XX.1"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Here, XXX represents the name of the missing parameter.</div><br> |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format of specified pagination parameter is invalid. |
|404 |InvalidEndpoint.NotFound |The specified endpoint does not exist. |The specified endpoint does not exist. |
