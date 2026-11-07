---
title: "DescribeCACertificates - Querying a CA certificate list"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeCACertificates"
---

Call the DescribeCACertificates API to query the CA certificate list.

## Instructions

A single account can query up to 100 CA certificates at a time. Submit up to 40 API requests per second.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeCACertificates&serviceCode=alb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选`Example: DescribeCACertificates`

The interface name. The current API name is `DescribeCACertificates`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. Current API version is `2020-04-01`.

**CACertificateIds.N ** String[]`optional` `Example: CACertificateIds.1=cert-123*** 765&CACertificateIds.2=cert-234****876`

ID of the CA certificate.

* Parameter \- N: Represents the serial number of certificate. The valid range is 1 to 100.

* Separate multiple certificates with ampersands (&).

**CACertificateName ** String`optional` `Example: test`

Name of the CA certificate.

**PageSize ** Integer`optional` `Example: 20`

Number of rows per page for paginated queries. Valid range: 1 to 100. Default value: 10.

**PageNumber** Integer `optional` `Example: 1`

The page number of the list. Default: 1.

**ProjectName ** String `optional` `Example value: default`

Name of the project to which the CA certificate belongs.

**TagFilters.N.Key ** String[]`optional` `Example: TagFilters.1.Key=k1&TagFilters.2.Key=k2`

The tag key.

* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns certificates tagged with all the specified keys.

* Duplicate values are not allowed.

**TagFilters.N.Values.N ** String[]`optional` `Example: TagFilters.1.Value.1=v1&TagFilters.1.Value.2=v2&TagFilters.2.Value.1=v3`

The tag value.

* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns certificates that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).

> **tip**

* > If this parameter is passed in, TagFilters.N.Key must be passed in first.

* > Passing an empty string queries for certificates with an empty tag value.

## Response parameters

**RequestId ** String`Example: 20210816110638****2514606306AF947C`

Request ID.

**PageSize ** Integer`Example: 20`

The number of rows on the current page.

**PageNumber** Integer `Example: 1`

Current page number.

**TotalCount ** Integer`Example: 50`

Total number of CA certificates that meet the criteria.

**CACertificates ** Object[]`Example: -`

List of CA certificates that meet the criteria.

**CACertificateId ** String`Example: cert-123***765`

CA certificate ID.

**CACertificateName ** String`Example: test`

CA certificate name.

**CertificateType ** String`Example: CA`

CA certificate type.

* CA: CA certificate.

**Description ** String`Example: test`

CA certificate description.

**CreateTime ** String`Example: 2021-12-14T11:13:40+08:00`

Creation time of the CA certificate.

**ExpiredAt ** String`Example: 2021-12-14T11:13:40+08:00`

Expiration time of the CA certificate.

**DomainName ** String`Example: test.com`

Domain name of the CA certificate.

**San ** String`Example: www.test.com,*.test.com`

List of certificate additional domain names, with multiple domains separated by commas (','), including (commonName, DnsName, IP).

**Listeners ** String[]`Example: [lsn-123 *****112,lsn-234 *****567]`

List of the listener associated with the CA certificate.

**Status ** String`Example: Active`

Status of the CA certificate.

* Creating

* Active: Running.

* Deleting

**ProjectName** String `Example: default`

Name of the project to which the CA certificate belongs.

**Tags ** Object[]`Example: --`

List of tags associated with the CA certificate.

**Key ** String`Example: key`

The tag key of the custom tag.

**Value ** String`Example: value`

The tag value of the custom tag.

## Request examples

```JSON
GET /?Action=DescribeCACertificates&CACertificateIds.1=cert-2fe5jqh****hs5oxruwk7x9ze&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "DescribeCACertificates",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210816110638****2514606306AF947C",
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 1,
        "Certificates": [
            {
                "CACertificateId": "cert-2fe5k****c16o5oxruvtk3qf5",
                "CACertificateName": "test",
                "CertificateType": "server",
                "Description": "test",
                "CreateTime": "2021-12-14T11:13:40+08:00",
                "ExpiredAt": "2021-12-14T11:13:40+08:00",
                "DomainName": "*.a.cdn-build.net",
                "Listeners": [
                    "lsn-1g0e0p14****88ibuxxpnwden",
                    "lsn-1g0e0p90e****8ibuxwy36kc1"
                ]
            }
        ]
    }
}
```

## Error codes

If the response body contains an Error field, it indicates the API request failed. This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Error-codes).

|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |LimitExceed.CACertificate |You've reached the limit on the number of CA certificates that you can operate at a time. |You have reached the maximum number of CA certificates that can be operated in a single operation. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidCACertificateName.Malformed |The specified CACertificateName is malformed. |The specified CACertificateName parameter format is invalid. |
|400 |LimitExceed.TagFilters.Values |You've reached the limit on the number of tag filter values that you can operate at a time. |You have reached the maximum number of tag values that can be operated on in a single request. |
|400 |InvalidTagFilters.Key.Malformed |The specified TagFilters.Key is malformed. |The specified TagFilters.Key parameter format is invalid. |
|400 |InvalidTagFilters.Value.Malformed |The specified TagFilters.Value is malformed. |The specified TagFilters.Value parameter format is invalid. |
|400 |InvalidTagFilters.Key.Duplicated |The specified TagFilters.Key is duplicated. |The specified TagFilters.Key is duplicated. |
