---
title: "CreateSslVpnServer - Creating an SSL-VPN server"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/CreateSslVpnServer"
---

Call CreateSslVpnServer to create an SSL\-VPN server.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateSslVpnServer&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|9opOBq">必选</span> `Example: CreateSslVpnServer`

The action that you want to perform. Value: CreateSslVpnServer.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|Q4ujpV">必选</span> `Example: 2020-04-01`

The API version.



**VpnGatewayId ** <span data-label="purple"> String  </span><span data-api-tag="require|Lr67Ik">必选</span> `Example: vgw-12bfa2du17q7y1rk****`

The ID of the VPN gateway used to create the SSL\-VPN server. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) to query the VPN gateway ID.



**LocalSubnets.N ** <span data-label="purple"> String </span><span data-api-tag="require|_6xs6F">必选</span> `Example: 10.0.1.0/8`

The local subnet of the SSL\-VPN server. It refers to the local CIDR block that clients access through the SSL\-VPN connection.


* N represents the sequence number of a SSL\-VPN server's local subnet.

* Separate multiple CIDR blocks with ampersands (`&`).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can specify up to <strong>5</strong> local subnets. They must not conflict with CIDR blocks of <code>ClientIpPool</code>.</div>




**ClientIpPool ** <span data-label="purple"> String </span><span data-api-tag="require|OjDLOW">必选</span> `Example: 192.168.1.0/24`

The client IP pool of the SSL\-VPN server. In SSL\-VPN, the client IP pool consists of CIDR blocks allocated to clients' virtual network interfaces for secure access. It is not related to the client's internal network blocks.


* Mask for Client IP pool: `/16` to `/28`.

* The client IP pool must not conflict with the `LocalSubnet` CIDR block or any IPsec\-VPN connection routes.

* The client IP pool must not overlap with `100.64.0.0/10`, `169.254.0.0/16`, `127.0.0.0/8`, `224.0.0.0/4`, or `240.0.0.0/4`.

* The available IP count in the client IP pool must be at least four times the SSL Max Connections value configured when creating the VPN gateway. For example, if the SSL Max Connections is set to 10, the client IP pool must contain more than 40 available IP addresses.



**SslVpnServerName ** <span data-label="purple"> String </span>`Optional` `Example: test-ssl-vpn`

The name for the SSL\-VPN server to be created.


* Must start with a Chinese character, letter, or digit. May include Chinese characters, letters, digits, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If left blank, it defaults to the ID of the SSL\-VPN server.



**Description ** <span data-label="purple"> String  </span>`Optional` `Example: This is a description`

The description for the SSL\-VPN server to be created.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, digits, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, it defaults to an empty string.



**Protocol ** <span data-label="purple"> String </span>`Optional` `Example: UDP`

The protocol used by the SSL\-VPN server. Values:


* TCP (default): Transmission Control Protocol.

* UDP: User Datagram Protocol



**Cipher ** <span data-label="purple"> String  </span>`optional` `Example: AES-128-CBC`

The encryption algorithm of the SSL\-VPN server


* AES\-128\-CBC (default)

* AES\-192\-CBC

* AES\-256\-CBC

* None (no encryption)



**Auth ** <span data-label="purple"> String </span>`Optional` `Example: SHA1`

The authentication algorithm of the SSL\-VPN server.


* SHA1 (default)

* MD5

* None (no encryption)



**Compress ** <span data-label="purple"> Boolean  </span>`Optional` `Example: false`

Specify whether to compress data transmission


* true: Compress communication.

* false (default): Do not compress communication.



**ClientToken ** <span data-label="purple"> String </span>`optional` `Example: 02fb3da4-130e-11e9-8e44-0016e04****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



**ProjectName ** <span data-label="purple"> String </span>`optional` `Example: Project_1`

The project to which the SSL\-VPN server belongs. If left blank, the `default` is used. That is, the created resource belongs to the default project.



**Port ** <span data-label="purple"> Integer  </span>`optional` `Example: 1194`

The port used by the SSL\-VPN server. Default: 1194.


* Port range: 1 to 65535.

* Unsupported ports: 22, 68, 179, 323, 500, and 4500.



**Tags.N.Key ** <span data-label="purple"> String </span>`optional` `Example: key1`

The tag key of the SSL\-VPN server.


* N represents the sequence number of a tag key. Valid range: 1\-20.

* Separate multiple tag keys with ampersands (&).


The naming rules are as follows:


* Must not start with volc: or sys:, regardless of case.

* May include language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* Must be 1 to 128 characters.


> Note: Tag keys of the same resource must be unique.



**Tags.N.Value** <span data-label="purple">String</span> `optional` `Example: value1`

The tag value of the SSL\-VPN server.


* N represents the sequence number of a tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).


The naming rules are as follows:


* May include language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* May be left blank. Must be 0 to 256 characters in length.

* Case\-sensitive. Cannot start or end with a space.


> Note: To provide Tags.N.Value, you must provide Tags.N.Key.



**LogEnabled ** <span data-label="purple"> Boolean  </span>`Optional` `Example: true`

Specify whether to enable SSL\-VPN connection log. Values:


* true: Enable

* false (default): Disable



**DnsServerIpAddresses.N ** <span data-label="purple"> String  </span>`optional` `Example: 1.1.1.1`

The IP address of the DNS server. You can specify up to two IPv4 addresses.



**DnsDomain ** <span data-label="purple"> String </span>`Optional` `Example: ivolcs.com`

The DNS domain for resolution. This parameter takes effect only when `DnsServerIpAddresses` is specified.



**ClientCertSessionPolicy ** <span data-label="purple"> String  </span>`Optional` `Example: AllowConcurrent`

Specify whether to enable certificate reuse. Values:


* AllowConcurrent (default): Enable

* PreemptExisting: Disable



**SsoAuthEnabled ** <span data-label="purple"> Boolean </span>`Optional` `Example: false`

Enable two\-factor authentication. Values:


* true: Enable

* false (default): Disable



**SamlData ** <span data-label="purple"> String  </span>`optional` `Example: GZ4ZDU0MmMwODYtYzAyKioqIiB4bWxuczptZD0idXJuOm9hc2lzOm5hbWVzOnRjOlNBTUw6Mi4wOm1ldGFkYXRhIj4=`

The SAML metadata of the identity provider (IdP). It must be in XML format and base64\-encoded.

This parameter is required when `SsoAuthEnabled` is `true`.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

The request ID.



**SslVpnServerId ** <span data-label="purple"> String  </span>`Example: vss-zm55pqtvk17oq32zd****`

The instance ID of the SSL\-VPN server



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET /?Action=CreateSslVpnServer&Version=2020-04-01&VpnGatewayId=vgw-12bfa2du17q7y1rk****&LocalSubnets.1=10.0.1.0/8&ClientIpPool=192.168.1.0/24&SslVpnServerName=test-ssl-vpn&Description=This is a descrption&Protocol=UDP&Cipher=AES-128-CBC&Auth=SHA1&Compress=false&ClientToken=02fb3da4-130e-11e9-8e44-0016e04****&ProjectName=Project_1&Port=1194&Tags.1.Key=key1&Tags.1.Value=value1&LogEnabled=true&DnsServerIpAddresses.1=1.1.1.1&DnsDomain=ivolcs.com&ClientCertSessionPolicy=AllowConcurrent&SsoAuthEnabled=false&SamlData=GZ4ZDU0MmMwODYtYzAyKioqIiB4bWxuczptZD0idXJuOm9hc2lzOm5hbWVzOnRjOlNBTUw6Mi4wOm1ldGFkYXRhIj4= HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSslVpnServer",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "SslVpnServerId": "vss-zm55pqtvk17oq32zd****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. A name must not exceed 128 characters. |
|400 |InvalidParameter.ClientCertSessionPolicy |The specified ClientCertSessionPolicy is invalid. |The specified client certificate session policy is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidClientIpPool.ConflictRoute |The specified ClientIpPool conflicts with that of VPN gateway route table cidr. |The specified client IP pool conflicts with the destination address in the VPN gateway route table. |
|400 |InvalidSslVpnClientIpPool.Conflict |The specified ClientIpPool conflicts with that of VPN gateway route. |The specified client IP pool conflicts with the VPN gateway route. |
|400 |InvalidSslVpnServerAuth.Malformed |The specified Auth is malformed. |The specified authentication algorithm for the SSL\-VPN server is invalid. |
|400 |InvalidSslVpnServerCipher.Malformed |The specified Cipher is malformed. |The specified encryption algorithm for the SSL\-VPN server is invalid. |
|400 |InvalidSslVpnServerClientIpPool.Malformed |The specified ClientIpPool is malformed. |The specified client CIDR is invalid. |
|400 |InvalidSslVpnServerClientIpPoolMask.Malformed |The netmask length of client IP pool must be greater than or equal to 16 and less than or equal to 28. |The specified client IP pool mask must be between 16 and 28 inclusive. |
|400 |InvalidSslVpnServerLocalSubnet.Conflict |There are conflicting CIDRs in the specified LocalSubnets. |The specified local subnet contains conflicting CIDR blocks. |
|400 |InvalidSslVpnServerLocalSubnet.Malformed |The specified LocalSubnet is malformed. |The specified Local Subnet is invalid. |
|400 |InvalidSslVpnServerProtocol.Malformed |The specified Protocol is malformed. |The specified protocol for the SSL\-VPN server is invalid. |
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|400 |InvalidVpnGateway.SslNotEnabled |SSL of the specified VPN gateway is not enabled. |The current VPN gateway does not have SSL enabled. |
|400 |LimitExceeded.SslVpnServerEachVpnGateway |You've reached the limit on the number of SSL servers per VPN gateway that you can create. |You have reached the maximum number of SSL\-VPN servers that you can created per VPN gateway instance. |
|400 |LimitExceeded.SslVpnServerLocalSubnets |You've reached the limit on the number of local subnets per SSL server that you can create. |You have reached the maximum number of local subnets that you can configure per SSL\-VPN server. |
|400 |InvalidSslVpnServerClientIpPool.VpcRouteEntry |Failed to create route entry in the system route table of the VPC contains the specified VPN gateway for the client ip pool. |The request to add a route targeting the client IP pool to the VPN gateway's VPC route table failed. |
|400 |QuotaExceeded.RouteEntry |Route entry of a route table number exceeded quota. |You have reached the maximum number of routes that can be created. |
|400 |InvalidClientIpPool.NotEnough |The support ip numbers of ClientIpPool is smaller than SslMaxConnections of vpn gateway. |The IP count supported by the client IP pool is less than the SSL Max Connections value selected for the gateway. |
|400 |InvalidSslVpnServerPort.Malformed |The specified ssl vpn server port is invalid. |The value of the specified SSL\-VPN server port is invalid. |
|400 |QuotaExceeded.VpcRouteEntry |You've reached the limit on the number of route entry in the system route table of the VPC contains the specified VPN gateway that you can create. |You have reached the maximum of routes that you can create in the system route table of the VPC to which the specified VPN gateway belongs. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|403 |Forbidden.ClientCertSessionPolicyNotGranted |Client certificate session policy feature is not enabled in this region. |The session policy feature for client certificate is unavailable in the current region. |
|403 |Forbidden.VpnGatewayBlocked |The specified VPN gateway is blocked. |The current VPN gateway is currently blocked. No actions are allowed. |
|404 |InvalidVpnGateway.NotFound |The specified VPN gateway does not exist. |The specified VPN gateway does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|409 |InvalidRouteCidr.Conflict |The specified CIDR block conflicts with that of another route in your route table. |The specified CIDR block conflicts with another rule's CIDR block in the associated route table. |
|409 |InvalidSslVpnServerVpcRouteEntry.Conflict |The specified ClientIpPool conflicts with that of another route in the system route table of the VPC contains the VPN gateway. |The specified client IP pool conflicts with the CIDR block of another rule in the system route table of the VPC to which the VPN gateway belongs. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|412 |InvalidVpnGateway.Expired |The specified VPN gateway has expired. |The specified VPN gateway is expired. |
