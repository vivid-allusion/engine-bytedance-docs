---
title: "ModifySslVpnServer - Modifying an SSL-VPN server"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/ModifySslVpnServer"
---

Call ModifySslVpnServer to modify the name, description, local subnet, client IP pool, encryption algorithm, and authentication algorithm for an SSL\-VPN server.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Leaving optional parameters of this API unset means no modifications to them.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifySslVpnServer&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|GKQTdO">必选</span> `Example: ModifySslVpnServer`

The action that you want to perform. Value: ModifySslVpnServer.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|4an93j">必选</span> `Example: 2020-04-01`

The API version.



**SslVpnServerId ** <span data-label="purple"> String  </span><span data-api-tag="require|kZbfUc">必选</span> `Example: vss-zm55pqtvk17oq32zd****`

The ID of the SSL\-VPN server to be modified. You can call [DescribeSslVpnServers](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnServers) to query the ID of the SSL\-VPN server.



**Description ** <span data-label="purple"> String  </span>`optional` `Example: This is a ssl description`

The description of the SSL\-VPN server.


* Must start with a Chinese character, letter, or digit. May include Chinese characters, letters, digits, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.



**SslVpnServerName ** <span data-label="purple"> String  </span>`optional` `Example: test-ssl-vpn`

The name of the SSL\-VPN server.


* Must start with a Chinese character, letter, or digit. May include Chinese characters, letters, digits, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.



**Auth ** <span data-label="purple"> String  </span>`optional` `Example: SHA1`

The authentication algorithm.


* SHA1

* MD5

* None (no encryption)



**Cipher ** <span data-label="purple"> String </span>`optional` `Example: AES-128-CBC`

The encryption algorithm.


* AES\-128\-CBC

* AES\-192\-CBC

* AES\-256\-CBC

* None (no encryption)



**Client IP Pool ** <span data-label="purple"> String </span>`optional` `Example: 192.168.1.0/24`

The client IP pool.


* This client IP pool must not conflict with the `LocalSubnet` CIDR block or any IPsec\-VPN connection routes.

* This CIDR block must not overlap with the local subnet, `100.64.0.0/10`, `169.254.0.0/16`, `224.0.0.0/3`, `127.0.0.0/8`, or `240.0.0.0/4`.

* The IP count covered by the mask is at least **4** times the SSL Max Connections value configured for the VPN gateway.



**Compress ** <span data-label="purple"> Boolean  </span>`optional` `Example: false`

Specify whether to compress communication.


* true: Compress communication.

* false: Do not compress communication.



**LocalSubnets.N ** <span data-label="purple"> String </span>`optional` `Example: 172.XX.1.0/24`

The local subnet.


* Recommended mask for Local Subnet: `/8` to `/32`.

* The local subnet must not conflict with the client IP pool.



**Port ** <span data-label="purple"> Integer </span>`optional` `Example: 1194`

The port used by the SSL\-VPN server.


* Port range: 1\-65535.

* Unsupported ports: 22, 68, 179, 323, 500, and 4500.



**Protocol ** <span data-label="purple"> String </span>`optional` `Example: UDP`

The protocol used by the SSL\-VPN server. Values:


* TCP: Transmission Control Protocol

* UDP: User Datagram Protocol



**LogEnabled ** <span data-label="purple"> Boolean </span>`optional` `Example: true`

Specify whether to enable SSL\-VPN connection log. Values:


* true: Enable

* false: Disable



**DnsServerIpAddresses.N ** <span data-label="purple"> String </span>`optional` `Example: 1.1.1.1`

The IP address of the DNS server. You can specify up to two IPv4 addresses.



**DnsDomain ** <span data-label="purple"> String  </span>`optional` `Example: ivolcs.com`

The DNS domain for resolution. This parameter takes effect only when `DnsServerIpAddresses` is specified.



**ClientCertSessionPolicy ** <span data-label="purple"> String </span>`optional` `Example: PreemptExisting`

Specify whether to enable certificate reuse. Values:


* AllowConcurrent (default): Enable

* PreemptExisting: Disable



**SsoAuthEnabled ** <span data-label="purple"> Boolean </span>`optional` `Example: false`

Specify whether to enable two\-factor authentication. Values:


* true: Enable

* false (default): Disable



**SamlData ** <span data-label="purple"> String  </span>`optional` `Example: GZ4ZDU0MmMwODYtYzAyKioqIiB4bWxuczptZD0idXJuOm9hc2lzOm5hbWVzOnRjOlNBTUw6Mi4wOm1ldGFkYXRhIj4=`

The SAML metadata of the identity provider (IdP). It must be in XML format and base64\-encoded.

This parameter is required when `SsoAuthEnabled` is `true`.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`Example: 0E006-F706-4D23-88ED-E11ED28DC****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET /?Action=ModifySslVpnServer&Version=2020-04-01&SslVpnServerId=vss-zm55pqtvk17oq32zd****&Description=This is a ssl description&SslVpnServerName=test-ssl-vpn&Auth=SHA1&Cipher=AES-128-CBC&ClientIpPool=192.168.1.0/24&Compress=false&LocalSubnets.1=172.XX.1.0/24&Port=1194&Protocol=UDP&LogEnabled=true&DnsServerIpAddresses.1=1.1.1.1&DnsDomain=ivolcs.com&ClientCertSessionPolicy=PreemptExisting&SsoAuthEnabled=false&SamlData=GZ4ZDU0MmMwODYtYzAyKioqIiB4bWxuczptZD0idXJuOm9hc2lzOm5hbWVzOnRjOlNBTUw6Mi4wOm1ldGFkYXRhIj4= HTTP/1.1
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
        "Action": "ModifySslVpnServer",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "0E006-F706-4D23-88ED-E11ED28DC****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidParameter.ClientCertSessionPolicy |The specified ClientCertSessionPolicy is invalid. |The specified client certificate session policy is invalid. |
|400 |InvalidSslVpnServer.InvalidStatus |The specified SSL server is not in the correct status for the request. |The specified SSL\-VPN server cannot respond to this request due to its status. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidClientIpPool.NotEnough |The support ip numbers of ClientIpPool is smaller than SslMaxConnections of vpn gateway. |The IP count supported by the client IP pool is less than the SSL Max Connections value selected for the gateway. |
|400 |InvalidSslVpnClientIpPool.Conflict |The specified ClientIpPool conflicts with that of local subnets. |The specified client IP pool conflicts with the local subnet. |
|400 |InvalidSslVpnServerAuth.Malformed |The specified Auth is malformed. |The specified authentication algorithm for the SSL\-VPN server is invalid. |
|400 |InvalidSslVpnServerCipher.Malformed |The specified Cipher is malformed. |The specified encryption algorithm for the SSL\-VPN server is invalid. |
|400 |InvalidSslVpnServerClientIpPool.Malformed |The specified ClientIpPool is malformed. |The specified client IP pool is invalid. |
|400 |InvalidSslVpnServerClientIpPool.VpcRouteEntry |Failed to create route entry in the system route table of the VPC contains the specified VPN gateway for the client ip pool. |The request to add a route targeting the client IP pool to the VPN gateway's VPC route table failed. |
|400 |InvalidSslVpnServerClientIpPoolMask.Malformed |The netmask length of client IP pool must be greater than or equal to 16 and less than or equal to 28. |The specified client IP pool mask must be between 16 and 28 inclusive. |
|400 |InvalidSslVpnServerLocalSubnet.Conflict |There are conflicting CIDRs in the specified LocalSubnets. |The specified local subnet contains conflicting CIDR blocks. |
|400 |InvalidSslVpnServerLocalSubnet.Malformed |The specified LocalSubnet is malformed. |The specified Local Subnet is invalid. |
|400 |InvalidSslVpnServerPort.Malformed |The specified ssl vpn server port is invalid. |The value of the specified SSL\-VPN server port is invalid. |
|400 |InvalidSslVpnServerProtocol.Malformed |The specified Protocol is malformed. |The specified protocol for the SSL\-VPN server is invalid. |
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|400 |LimitExceeded.SslVpnServerLocalSubnets |You've reached the limit on the number of local subnets per SSL server that you can create. |You have reached the maximum number of local subnets that can be configured per SSL\-VPN server. |
|400 |QuotaExceeded.VpcRouteEntry |You've reached the limit on the number of route entry in the system route table of the VPC contains the specified VPN gateway that you can create. |You have reached the maximum of routes that can be created in the system route table of the VPC to which the specified VPN gateway belongs. |
|403 |Forbidden.VpnGatewayBlocked |The specified VPN gateway is blocked. |The current VPN gateway is currently blocked. No actions are allowed. |
|404 |InvalidSslVpnServer.NotFound |The specified SSL server does not exist. |The specified SSL\-VPN server does not exist. |
|404 |InvalidVpnGateway.NotFound |The specified VPN gateway does not exist. |The specified VPN gateway does not exist. |
|409 |InvalidRouteCidr.Conflict |The specified CIDR block conflicts with that of another route in your route table. |The specified CIDR block conflicts with another rule's CIDR block in the associated route table. |
|409 |InvalidSslVpnServerVpcRouteEntry.Conflict |The specified ClientIpPool conflicts with that of another route in the system route table of the VPC contains the VPN gateway. |The specified client IP pool conflicts with the CIDR block of another rule in the system route table of the VPC to which the VPN gateway belongs. |
|412 |InvalidVpnGateway.Expired |The specified VPN gateway has expired. |The specified VPN gateway is expired. |
