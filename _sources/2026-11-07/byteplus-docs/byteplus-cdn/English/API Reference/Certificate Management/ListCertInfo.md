---
title: "ListCertInfo"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-listcertinfo"
---

For certificates that meet the filtering criteria, obtain the domain names associated with these certificates.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=ListCertInfo&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `ListCertInfo`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Source |String |Yes |Indicates the location where the certificate is stored. Currently, this parameter value can only be `cert_center`, which refers to BytePlus Certificate Center. |`cert-center` |
|CertId |String |No |Indicates a certificate ID to retrieve the certificate with that ID. |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|ConfiguredDomain |String |No |Indicates a list of domain names for acceleration, to obtain certificates that have been bound to any domain name on the list. |`www.example.com,www.test.com` |
|FuzzyMatch |Boolean |No |When `Name` is specified, `FuzzyMatch` indicates the matching method used by the CDN when filtering certificates by `Name`. The parameter can have the following values:<br><br><br>* `true`: indicates fuzzy matching.<br><br>* `false`: indicates exact matching.<br><br><br>If you don not specify `Name`, `FuzzyMatch` is not effective.<br><br>The default value of `FuzzyMatch` is `false`. |`true` |
|Name |String |No |Indicates a domain name used to obtain certificates that include that domain name in the SAN field. The domain name can be a wildcard domain. For example, \*.example.com can match certificates containing img.example.com or www.example.com, etc., in the SAN field. |`www.example.com` |
|PageNum |Long |No |For the list of certificates that meet the filter criteria, this parameter Indicates a page number. The certificates actually returned by this API are those on the page specified by the page number.<br><br>The certificates returned by this API are paginated based on `PageSize`. Assuming the API returns 100 certificates and you specified `PageSize` as `10`, then the returned certificates are spread across 10 pages. If you specify `PageNum` as `2`, it means to retrieve the certificates on the second page.<br><br>If there are no certificates on the specified page, the `CertInfo` parameter value in the return results will be `null`.<br><br>The default value for `PageNum` is `1`. |`1` |
|PageSize |Long |No |Indicates the number of certificates per page.<br><br>The range of values for this parameter is 1\-100, with the default being `10`. |`10` |
|Status |String |No |Indicates a list of states to retrieve certificates that are in any of the states on the list. The parameter can have the following values:<br><br><br>* `running`: indicates certificates with a remaining validity period of more than 30 days.<br><br>* `expired`: indicates certificates that have expired.<br><br>* `expiring_soon`: indicates certificates with a remaining validity period of 30 days or less but have not yet expired. |`expired,running` |
|SortRule |Object |No |Indicates a sorting rule to sort the certificates returned by this API. The default rule is to sort the returned certificates in ascending order by the `ExpireTime` parameter in the response. | |
|Asc |Boolean |No |Indicates the method of sorting. The parameter can have the following values:<br><br><br>* `false`: indicates that the certificates in the list are sorted in descending order.<br><br>* `true`: indicates that the certificates in the list are sorted in ascending order.<br><br><br>The default value for this parameter is `true`. |`true` |
|OrderBy |String |No |Indicates the field by which the returned certificates are sorted. If you have specified `SortRule`, `OrderBy` is required. The current value of `OrderBy` must be `ExpireTime`, which means sorting the certificates by their expiration time. |`ExpireTime` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|PageNum |Long |Indicates the `PageNum` you specified in the request parameters. |`1` |
|PageSize |Long |Indicates the `PageSize` you specified in the request parameters. |`10` |
|Total |Long |Indicates the number of certificates that meet the filtering criteria. The value of this parameter is not affected by `PageSize` and `PageNum`. |`2` |
|CertInfo |Object[] |Indicates the list of certificates returned by this API.<br><br>Note that the certificates in the list are those on the page indicated by the `PageNum` parameter, not necessarily all certificates that meet the filtering criteria. | |
|Source |String |For a certificate in the list, this parameter indicates the location where the certificate is stored, with the following value:<br><br><br>* `cert_center`: indicates BytePlus Certificate Center. |`cert_center` |
|CertId |String |Indicates the ID of the certificate. |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|CertName |String |Indicates the content of the `Common Name (CN)` field of the certificate. |`*.example.com` |
|Status |String |Indicates the status of the certificate. The parameter can have the following values:<br><br><br>* `running`: indicates the certificate has a remaining validity period of more than 30 days.<br><br>* `expired`: indicates the certificate has expired.<br><br>* `expiring_soon`: indicates the certificate has a remaining validity period of 30 days or less but has not yet expired. |`running` |
|EffectiveTime |Long |Indicates the issuance time of the certificate. The unit is Unix timestamp. |`1655856000` |
|ExpireTime |Long |Indicates the expiration time of the certificate. The unit is Unix timestamp. |`1687478399` |
|DnsName |String |Indicates the domain names in the `SAN` field of the certificate. |`www.test.com,*www.example.com` |
|Desc |String |Indicates the remark of the certificate. |`Test` |
|ConfiguredDomain |String |Indicates the list of domain names associated with the certificate. If the certificate has not been associated with any domain name, the parameter value is `null`. |`www.example.com, www.test.com` |
|CertFingerprint |Object |Indicates the fingerprint information of the certificate. | |
|Sha1 |String |Indicates a fingerprint based on the SHA\-1 encryption algorithm, composed of 40 hexadecimal characters. |`4f6c4bd5402e8f848837bf1334740ece0671ae4d` |
|Sha256 |String |Indicates a fingerprint based on the SHA\-256 encryption algorithm, composed of 64 hexadecimal characters. |`24e49e0888f91a25f1503b452aa7cf0cf30da637810eaee5309b0be6c3931c9d` |
|ExpiringCount |Long |Indicates the number of certificates with the status `expiring_soon` among those that meet the filtering criteria. However, this parameter is not currently effective, therefore its value is always `0`. |`0` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=ListCertInfo&Version=2021-03-01
{
    "Source": "cert_center",
    "Name": "www.example.com",
    "Status": "running,expired",
    "SortRule": {
        "Asc": false,
        "OrderBy": "ExpireTime"
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240315094304D1302166C42C534627B0",
        "Action": "ListCertInfo",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertInfo": [
            {
                "CertId": "cert-7b94354335aa424993ce48fa355f1e5e",
                "CertName": "www.example.com",
                "ConfiguredDomain": "www.example.com",
                "Desc": "Test",
                "DnsName": "www.example.com",
                "EffectiveTime": 1708992000,
                "ExpireTime": 1740700799,
                "Source": "cert_center",
                "Status": "running"
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```


&nbsp;
