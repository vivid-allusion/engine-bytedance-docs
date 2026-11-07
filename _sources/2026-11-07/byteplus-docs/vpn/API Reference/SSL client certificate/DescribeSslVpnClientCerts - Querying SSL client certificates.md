---
title: "DescribeSslVpnClientCerts - Querying SSL client certificates"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnClientCerts"
---

Call DescribeSslVpnClientCerts to query information about SSL client certificates that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeSslVpnClientCerts&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|-Z-Lvm">必选</span> Example: `DescribeSslVpnClientCerts`

The action that you want to perform. Value: DescribeSslVpnClientCerts.



**Version ** `String` <span data-api-tag="require|euiQ1X">必选</span> Example: `2020-04-01`

The API version.



**SslVpnClientCertIds.N ** `String` `optional` Example: `vsc-12b8vwu4k5****`

ID of the SSL client certificate.


* N represents the sequence number of an SSL client certificate ID.

* Separate multiple IDs with ampersands (&).



**SslVpnClientCertName ** `String` `optional` Example: `example_ssl_client_cert`

Name of the SSL client certificate.



**SslVpnServerId ** `String` `optional` Example: `example_ssl_client`

The ID of the SSL VPN server associated with the SSL VPN client. You can call [DescribeSslVpnServers](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnServers) to query the ID of the SSL VPN server.



**PageSize ** `Integer` `optional` Example: `20`

Page size of the query results. Maximum: 100. Default: 20.



**PageNumber ** `Integer` `optional` Example: `1`

Page number of query results


* Set this parameter to a non\-negative integer.

* If you omit it or set it to 0, the value defaults to 1.



**TagFilters.N.Key ** `String` `optional` Example: `key1`

The specified tag key when querying resources by tag.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with ampersands (&).

* Duplicate values are not allowed.



**TagFilters.N.Values.M** `String` `optional` Example: `value1`

The specified tag value when querying resources by tag.


* The first N represents the sequence number of a tag key. Valid range: 1–10.

* The second N represents the sequence number of a tag value. Valid range: 1–3. That is, you can query up to three tag values for the same tag key.

* Separate multiple tag values with ampersands (&).

* To provide this parameter, you must provide TagFilters.N.Key.

* If you only provide TagFilters.N.Key without this parameter, the system will query all tag values of the same tag key.

* If you provide an empty string, the system will query tags with an empty tag value.

* If you set multiple TagFilters.N.Values.M values for the same TagFilters.N.Key, these TagFilters.N.Values.M values are combined with a logical OR.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `0ED8D006-F706-4D23-88ED-E11ED28****`

Request ID.



**PageSize ** `Integer` `optional` Example: `20`

The number of rows on the current page.



**PageNumber ** `Integer` `optional` Example: `1`

Current page number.



**TotalCount ** `Integer` `optional` Example: `33`

Total number of SSL client certificates matching the query conditions.



**SslVpnClientCerts ** `Object[]` `optional` Example: `-`

Collection of SSL client certificate information.


**Tags ** `Object[]` `optional`

Information about all tags associated with the SSL client certificate.


**Key ** `String` `optional` Example: `key1`

The tag key.



**Value ** `String` `optional` Example: `value1`

The tag value.




**Status ** `String` `optional` Example: `Available`

The status of the SSL VPN client.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**UpdateTime ** `String` `optional` Example: `2018-05-28T18:09:12+08:00`

The time when the SSL client certificate is modified.



**Description ** `String` `optional` Example: `example_ssl_vpn_client_cert_description`

Description of the SSL client certificate.



**ExpiredTime ** `String` `optional` Example: `2018-04-18T15:02:37+08:00`

The time when the SSL client certificate expires.



**CreationTime ** `String` `optional` Example: `2018-04-18T15:02:37+08:00`

The time when the SSL client certificate is created.



**SslVpnServerId ** `String` `optional` Example: `vss-zm55pqtvk17oq32zd****`

ID of the SSL VPN server.



**CertificateStatus ** `String` `optional` Example: `Expired`

Status of the SSL client certificate.


* Available

* Expiring: Displayed when the resource expires within 1 week (inclusive).

* Expired



**SslVpnClientCertId ** `String` `optional` Example: `vsc-zm55pqtvk17oq32zd****`

ID of the SSL client certificate.



**SslVpnClientCertName ** `String` `optional` Example: `example_ssl_vpn_client_cert`

Name of the SSL client certificate.




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeSslVpnClientCerts&Version=2020-04-01&SslVpnClientCertIds.1=vsc-12ads0g2fsmps17q7y2w8****&PageNumber=1&PageSize=10 HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230727200729C3CE7E861A3C6C00****",
        "Action": "DescribeSslVpnClientCerts",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20230727200729C3CE7E861A3C6C00****",
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 1,
        "SslVpnClientCerts": [
            {
                "SslVpnClientCertId": "vsc-12ads0g2fsmps17q7y2w8****",
                "SslVpnClientCertName": "test-cicd",
                "Description": "abc",
                "SslVpnServerId": "vss-imwoo6i1dfk08gbssxfj****",
                "Status": "Available",
                "CertificateStatus": "Available",
                "Tags":[
                    {
                        "Key":"k1",
                        "Value":"v1"
                    },
                    {
                        "Key":"k2",
                        "Value":"v2"
                    }
                ],
                "CreationTime": "2023-07-27T19:55:08+08:00",
                "ExpiredTime": "2026-07-27T19:55:08+08:00",
                "UpdateTime": "2023-07-27T19:57:56+08:00"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.SslVpnClientCertId |You've reached the limit on the number of SSL client certificate IDs that you can describe. |You have reached the maximum IDs of SSL client certificates that you can query. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
