---
title: "DescribeSslVpnServers - Querying SSL-VPN servers"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnServers"
---

Call DescribeSslVpnServers to query information about SSL\-VPN servers.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeSslVpnServers&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|FmAIq9">必选</span> `Example: DescribeSslVpnServers`

The action that you want to perform. Value: DescribeSslVpnServers.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|3bLXad">必选</span> `Example: 2020-04-01`

The API version.



**VpnGatewayId ** <span data-label="purple"> String </span>`optional` `Example: vgw-2feyp1wmtx14w****`

The ID of the VPN gateway used by the SSL\-VPN server. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) to query the ID of the VPN gateway.



**SslVpnServerName ** <span data-label="purple"> String  </span>`optional` `Example: Ssl_Servers`

The name of the SSL\-VPN server.



**SslVpnServerIds.N ** <span data-label="purple"> String  </span>`optional` `Example: vss-12b8vv10jfx8g****`

The ID of the SSL\-VPN server.


* N represents the sequence number of an SSL\-VPN server ID.

* Separate multiple IDs with ampersands (&).



**PageSize ** <span data-label="purple"> Integer  </span>`optional` `Example: 20`

The page size of the query results. Maximum: 100. Default: 20.



**PageNumber** <span data-label="purple">Integer</span> `optional` `Example: 1`

The page number of the query result.


* Set this parameter to a non\-negative integer.

* If you omit it or set it to 0, the value defaults to 1.



**ProjectName ** <span data-label="purple"> String </span>`optional` `Example: Project_1`

The project to which the SSL\-VPN server belongs.



**TagFilters.N.Key ** <span data-label="purple"> String  </span>`optional` `Example: key1`

The specified tag key when querying resources by tag.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with ampersands (&).

* Duplicate values are not allowed.



**TagFilters.N.Values.M ** <span data-label="purple"> String </span>`optional` `Example: value1`

The specified tag value when querying resources by tag.


* The first N represents the sequence number of a tag key. Valid range: 1–10.

* The second N represents the sequence number of a tag value. Valid range: 1–3. That is, you can query up to three tag values for the same tag key.

* Separate multiple tag values with ampersands (&).

* To provide this parameter, you must provide TagFilters.N.Key.

* If you only provide TagFilters.N.Key without this parameter, the system queries all tag values of the same tag key.

* If you provide an empty string, the system queries tags with an empty tag value.

* If you set multiple TagFilters.N.Values.M values for the same TagFilters.N.Key, these TagFilters.N.Values.M values are combined with a logical OR.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

The request ID.



**PageSize ** <span data-label="purple"> Integer  </span>`Example: 20`

The number of entries on the current page.



**PageNumber** <span data-label="purple">Integer</span> `Example: 1`

The current page number.



**TotalCount ** <span data-label="purple"> Integer </span>`Example: 1`

The total number of SSL\-VPN servers meeting the query conditions.



**SslVpnServers ** <span data-label="purple"> Object[]  </span>`Example: -`

The collection of SSL\-VPN server information.


**SslVpnServerId ** <span data-label="purple"> String </span>`Example: vss-zm55pqtvk17oq32zd****`

The instance ID of the SSL\-VPN server



**SslVpnServerName ** <span data-label="purple"> String  </span>`Example: test-ssl-vpn`

The name of the SSL\-VPN server.



**VpnGatewayId ** <span data-label="purple"> String </span>`Example: vgw-12bfa2du17q7y1rk****`

The ID of the VPN gateway used by the SSL\-VPN server.



**Description ** <span data-label="purple"> String  </span>`Example: This is a description`

The description of the SSL\-VPN server.



**Status ** <span data-label="purple"> String  </span>`Example: Available`

The status of the SSL\-VPN server.


* Available

* Creating

* Pending: Action in progress​

* Deleting



**LocalSubnets ** <span data-label="purple"> String[]  </span>`Example: 10.0.0.0/24`

The local subnet of the SSL\-VPN server.



**ClientIpPool ** <span data-label="purple"> String </span>`Example: 192.168.1.0/24`

The client IP pool of the SSL\-VPN server.



**Protocol ** <span data-label="purple"> String  </span>`Example: UDP`

The protocol used by the SSL\-VPN server. Values:


* TCP: Transmission Control Protocol

* UDP: User Datagram Protocol



**Cipher ** <span data-label="purple"> String </span>`Example: AES-128-CBC`

The encryption algorithm of the SSL\-VPN server


* AES\-128\-CBC

* AES\-192\-CBC

* AES\-256\-CBC

* None (no encryption)



**ClientCertSessionPolicy ** <span data-label="purple"> String </span>`Example: AllowConcurrent`

The session policy for client certificate.


* AllowConcurrent: Reusable.

* PreemptExisting: Non\-reusable.



**Auth ** <span data-label="purple"> String </span>`Example: SHA1`

The authentication algorithm of the SSL\-VPN server.


* SHA1

* MD5

* None (no encryption)



**Compress ** <span data-label="purple"> Boolean  </span>`Example: false`

Describes whether data transmission is compressed.


* true: Compressed.

* false: Not compressed.



**CreationTime ** <span data-label="purple"> String </span>`Example: 2023-04-18T15:02:37+08:00`

The time when the SSL\-VPN server is created.



**UpdateTime ** <span data-label="purple"> String </span>`Example: 2023-05-28T18:09:12+08:00`

The time when the SSL\-VPN server is modified.



**ProjectName ** <span data-label="purple"> String </span>`Example: Project_1`

The project to which the SSL\-VPN server belongs.



**Port ** <span data-label="purple"> Integer  </span>`Example: 1194`

The port used by the SSL\-VPN server.



**IsBlocked ** <span data-label="purple"> Boolean </span>`Example: false`

Describes whether the current resource is blocked.


* true: Blocked.

* false: Not blocked.



**Tags ** <span data-label="purple"> Object[] </span>`Example: -`

Information about all tags associated with the SSL\-VPN server.


**Key ** <span data-label="purple"> String  </span>`Example: key1`

The tag key.



**Value ** <span data-label="purple"> String  </span>`Example: value1`

The tag value.




**DnsDomain ** <span data-label="purple"> String  </span>`Example: ivolcs.com`

The DNS resolution domain.



**LogEnabled ** <span data-label="purple"> Boolean </span>`Example: false`

Describe whether connection log is enabled.


* true: Enabled.

* false: Not enabled.



**SsoAuthEnabled ** <span data-label="purple"> Boolean </span>`Example: false`

Describe whether two\-factor authentication is enabled.


* true: Enabled.

* false: Not enabled.



**DnsServerIpAddresses ** <span data-label="purple"> String[]  </span>`Example: [ "[\"8.8.8.8\"", "\"1.1.1.1\"]" ]`

The DNS server IP.




<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET /?Action=DescribeSslVpnServers&Version=2020-04-01&VpnGatewayId=vgw-2feyp1wmtx14w****&SslVpnServerName=Ssl_Servers&SslVpnServerIds.1=vss-12b8vv10jfx8g****&PageSize=20&PageNumber=1&ProjectName=Project_1&TagFilters.1.Key=key1&TagFilters.1.Values.M=value1 HTTP/1.1
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
        "Action": "DescribeSslVpnServers",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 20,
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "SslVpnServers": [
            {
                "Auth": "SHA1",
                "Port": 1194,
                "Tags": [
                    {
                        "Key": "key1",
                        "Value": "value1"
                    }
                ],
                "Cipher": "AES-128-CBC",
                "Status": "Available",
                "Compress": false,
                "Protocol": "UDP",
                "DnsDomain": "ivolcs.com",
                "IsBlocked": true,
                "LogEnabled": false,
                "UpdateTime": "2023-05-28T18:09:12+08:00",
                "Description": "This is a descrption",
                "ProjectName": "Project_1",
                "ClientIpPool": "192.168.1.0/24",
                "CreationTime": "2023-04-18T15:02:37+08:00",
                "LocalSubnets": [
                    ""
                ],
                "VpnGatewayId": "vgw-12bfa2du17q7y1rk****",
                "SslVpnServerId": "vss-zm55pqtvk17oq32zd****",
                "SsoAuthEnabled": true,
                "SslVpnServerName": "test-ssl-vpn",
                "DnsServerIpAddresses": [
                    "[\"8.8.8.8\"",
                    "\"1.1.1.1\"]"
                ],
                "ClientCertSessionPolicy": "AllowConcurrent"
            }
        ],
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.SslVpnServerId |You've reached the limit on the number of SSL server IDs that you can describe. |You have reached the maximum IDs of SSL\-VPN servers that can be queried. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format specified for the tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag filter keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag filter values that can be specified in a single request. |
