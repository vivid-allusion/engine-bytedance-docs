---
title: "ListCdnCertInfo"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-listcdncertinfo"
---

Retrieve the list of certificates that meet the filtering criteria and the list of domain names associated with these certificates.

If an IAM user calls this API, the domain names in the list are those that the IAM user has permission to access.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=ListCdnCertInfo&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `ListCdnCertInfo`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|CertId |String |No |Indicates the ID of a certificate; fetches the certificate with the specified ID.<br><br>You can use [ListCertInfo](https://docs.byteplus.com/en-US/byteplus-cdn/reference/listcertinfo) to obtain the ID of the desired certificate. |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|ConfiguredDomain |String |No |Indicates a list of domain names to fetch certificates associated with each domain name in the list. Multiple domain names are separated by commas (,).<br><br>The list can include wildcard domain names. However, it's important to note that for a wildcard domain name, a certificate will meet the `ConfiguredDomain` filter condition only if the associated domain names of the certificate include the wildcard domain name. For instance, if the specified `ConfiguredDomain` is `*.example.com`, a certificate will not meet the filter condition if its associated domain names include `www.example.com` but not `*.example.com`. |`www.example.com,*.test.com` |
|DnsName |String |No |Indicates a list of domain names to fetch certificates that contain any of the listed domain names in the SAN field. Multiple domain names are separated by commas (,).<br><br>The list can include wildcard domain names. However, it's noteworthy that for a wildcard domain name, a certificate will meet the `DnsName` filter condition only if the SAN field of the certificate includes the wildcard domain name. For example, if the specified `DnsName` is `*.example.com`, a certificate will not meet the filter condition if its SAN field includes `www.example.com` but not `*.example.com`. |`*.example.com,www.test.com` |
|PageNum |Long |No |For the list of certificates returned by the API, this parameter Indicates a page number. The actual list of certificates returned by the API corresponds to the certificates on the page specified by this page number.<br><br>The API returns certificates paginated according to `PageSize`. Assuming the API returns a total of 100 certificates and you specify a `PageSize` of `10`, the certificates will be distributed across 10 pages. If you specify `PageNum` as `2`, it indicates obtaining the certificates on page 2.<br><br>If there are no certificates on the specified page, the `CertInfo` parameter in the return result will be `null`.<br><br>The default value for `PageNum` is `1`. |`1` |
|PageSize |Long |No |Indicates the number of certificates included in each page.<br><br>The range of values for this parameter is 1\-100, with a default value of `10`. |`10` |
|Source |String |No |Indicates the storage location of the certificate, fetching certificates stored at this location. Currently, the only valid value for this parameter is `cert_center`, indicating BytePlus Certificate Center. |`cert_center` |
|Status |String |No |Indicates a list of certificate statuses to fetch certificates that are in any of the listed statuses. This parameter can take the following values:<br><br><br>* `running`: Indicates that the certificate has more than 30 days remaining in its validity period.<br><br>* `expired`: Indicates that the certificate has expired.<br><br>* `expiring_soon`: Indicates that the certificate has 30 days or less remaining in its validity period but has not yet expired.<br><br><br>Multiple certificate statuses are separated by commas (,). |`running,expird` |
|Configured |Boolean |No |Indicates whether to remove certificates that are not associated with any domain names in `CertInfo` returned by this API. This parameter has the following values:<br><br><br>* `true`: Indicates that certificates not associated with any domain names are removed.<br><br>* `false`: Indicates that certificates not associated with any domain names are retained.<br><br><br>The default value for this parameter is `true`. |`true` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|PageNum |Long |Represents the value of the `PageNum` in the request parameters. |`1` |
|PageSize |Long |Represents the value of the `PageSize` in the request parameters. |`10` |
|Total |Long |Represents the number of certificates that meet the filter criteria. The value of this parameter is not affected by `PageNum` and `PageSize`. |`8` |
|CertInfo |Object[] |Represents a list of certificates that meet the filter criteria. If there are no certificates that meet the filter criteria, the value of this parameter will be `null`. | |
|Source |String |For a certificate in the returned list of certificates, this parameter represents the storage location of the certificate. Currently, the value of this parameter is `cert_center`, indicating BytePlus Certificate Center. |`cert_center` |
|CertId |String |Represents the ID of the certificate. |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|CertName |String |Represents the content of the `Common Name (CN)` field of the certificate. |`*.example.com` |
|Status |String |Represents the status of the certificate. This parameter can take the following values:<br><br><br>* `running`: Indicates that the certificate has more than 30 days remaining in its validity period.<br><br>* `expired`: Indicates that the certificate has expired.<br><br>* `expiring_soon`: Indicates that the certificate has 30 days or less remaining in its validity period but has not yet expired. |`running` |
|EffectiveTime |Long |Represents the issue time of the certificate, in Unix timestamp format. |`1655856000` |
|ExpireTime |Long |Represents the expiration time of the certificate, in Unix timestamp format. |`1687478399` |
|DnsName |String |Represents the domain names included in the certificate's SAN field, separated by commas (,). |`*.example.com,www.test.com` |
|ConfiguredDomain |String |Represents a list of domain names associated with the certificate. Multiple domain names are separated by commas (,).<br><br>If the request parameter `Configured` is `false` and the certificate is not associated with any domain name, the value of this parameter will be `null`. |`www.example.com,abc.example.com,img.example.com` |
|Desc |String |Represents the remark of the certificate. |`Test` |
|CertFingerprint |Object |Represents the fingerprint information of the certificate. | |
|Sha1 |String |Represents a fingerprint based on the SHA\-1 encryption algorithm, composed of 40 hexadecimal characters. |`4f6c4bd5402e8f848837bf1334740ece0671ae4d` |
|Sha256 |String |Represents a fingerprint based on the SHA\-256 encryption algorithm, composed of 64 hexadecimal characters. |`24e49e0888f91a25f1503b452aa7cf0cf30da637810eaee5309b0be6c3931c9d` |
|ExpiringCount |Long |Represents the number of certificates with a status of `expiring_soon` among those that meet the filter criteria. However, this parameter is currently not in effect, so the value will always be `0`. |`0` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=ListCdnCertInfo&Version=2021-03-01
{
    "DnsName": "www.example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024040112464615DB56CED2E719493783",
        "Action": "ListCdnCertInfo",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertInfo": [
            {
                "CertId": "cert-c195f679cecb4fcd9823dd8c54e6c0a2",
                "CertName": "www.example.com",
                "ConfiguredDomain": "www.example.com",
                "Desc": "UploadCert",
                "DnsName": "www.example.com,example.com",
                "EffectiveTime": 1643414400,
                "ExpireTime": 1675036799,
                "Source": "cert_center",
                "Status": "running"
            }
        ],
        "ExpiringCount": 0,
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```
