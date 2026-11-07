---
title: "DescribeCertificates - Querying the server certificate list"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeCertificates"
---

Call the DescribeCertificates API to query the server certificate list.

## Instructions

* A single account can query up to 100 certificates at a time.

* Submit up to 40 API requests per second.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeCertificates&serviceCode=alb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribeCertificates`

The interface name. The current API name is `DescribeCertificates`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.

**CertificateIds.N ** String[]`optional` `Example: CertificateIds.1=cert-123*** 765&CertificateIds.2=cert-234****876`

Certificate ID.

* Parameter \- N: Represents the serial number of certificate. The valid range is 1 to 100.

* Separate multiple certificates with ampersands (&).

**CertificateName ** String`optional` `Example: test`

Certificate name.

**PageSize ** Integer`optional` `Example: 20`

Number of rows per page for paginated queries. Valid range: 1 to 100. Default value: 10.

**PageNumber** Integer `optional` `Example: 1`

The page number of the list. Default: 1.

**ProjectName ** String `optional` `Example value: default`

Name of the project to which the certificate belongs.

**TagFilters.N.Key ** String[]`optional` `Example: TagFilters.1.Key=k1&TagFilters.2.Key=k2`

The tag key.

* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns certificates tagged with all the specified keys.

* Duplicate values are not allowed.

**TagFilters.N.Values.N ** String[]`optional` `Example: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2&TagFilters.2.Values.1=v3`

The tag value.

* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns certificates that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).

> **tip**

> If this parameter is passed in, TagFilters.N.Key must be passed in first.

> Passing an empty string queries for certificates with an empty tag value.

## Response parameters

**RequestId ** String`Example: 20210816110638****2514606306AF947C`

Request ID.

**PageSize ** Integer`Example: 20`

The number of rows on the current page.

**PageNumber** Integer `Example: 1`

Current page number.

**TotalCount ** Integer`Example: 50`

Total number of certificates that meet the criteria.

**Certificates ** Object[]`Example: -`

List of certificates that meet the criteria.

**CertificateId ** String`Example: cert-123***765`

Certificate ID.

**CertificateName ** String`Example: test`

Certificate name.

**CertificateType ** String`Example: server`

Certificate type.

* Server: Server certificate.

**Description ** String`Example: test`

Certificate description.

**CreateTime ** String`Example: 2021-12-14T11:13:40+08:00`

Creation time of the certificate.

**ExpiredAt ** String`Example: 2021-12-14T11:13:40+08:00`

Expiration time of the certificate.

**DomainName ** String`Example: test.com`

The domain of the certificate.

**San ** String`Example: www.test.com,*.test.com`

The list of extended domain names of the certificate, separated by commas (','), including (commonName, DnsName, IP).

**Listeners ** String[]`Example: [lsn-123 *****112,lsn-234 *****567]`

List of the listener associated with the certificate.

**Status ** String`Example: Active`

Status of the certificate.

* Creating

* Active: Running.

* Deleting

**ProjectName** String `Example: default`

Name of the project to which the certificate belongs.

**Tags ** Object[]`Example: -`

Tags associated with the certificate.

**Key ** String`Example: key`

The tag key of the custom tag.

**Value ** String`Example: value`

The tag key of the custom tag.

## Request examples

```JSON
GET /?Action=DescribeCertificates&CertificateIds.1=cert-2fe5jqh****hs5oxruwk7x9ze&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "DescribeCertificates",
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
                "CertificateId": "cert-2fe5k****c16o5oxruvtk3qf5",
                "CertificateName": "test",
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
|400 |LimitExceed.ServerCertificate |You've reached the limit on the number of server certificates that you can operate at a time. |The maximum number of server certificates that can be operated on at one time has been reached. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidCertificateName.Malformed |The specified CertificateName is malformed. |The specified CertificateName parameter format is invalid. |
|400 |LimitExceed.TagFilters.Values |You've reached the limit on the number of tag filter values that you can operate at a time. |You have reached the maximum number of tag values that can be operated on in a single request. |
|400 |InvalidTagFilters.Key.Malformed |The specified TagFilters.Key is malformed. |The specified TagFilters.Key parameter format is invalid. |
|400 |InvalidTagFilters.Value.Malformed |The specified TagFilters.Value is malformed. |The specified TagFilters.Value parameter format is invalid. |
|400 |InvalidTagFilters.Key.Duplicated |The specified TagFilters.Key is duplicated. |The specified TagFilters.Key is duplicated. |
