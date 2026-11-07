---
title: "DescribeCertConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describecertconfig-9ea17"
---

For domain names that can be associated with the specified certificate, obtain the certificate configuration of these domain names. These domain names are in the SAN field of the specified certificate and have been added to the CDN.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeCertConfig&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeCertConfig`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|CertId |String |Yes |Indicates a certificate ID. The API returns the certificate configurations of the domains associated with the certificate.<br><br>You can call [ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-listcdncertinfo) to get the ID of the certificate. |`cert-5dc4bfa90c1048778abf036b03ffabf2` |
|Status |String |No |Indicates the status of the domain names, used to filter the domain names returned by this API. You can specify multiple statuses, separated by commas (,).<br><br>This parameter has the following values:<br><br><br>* `online`: Indicates the status is "Enabled".<br><br>* `offline`: Indicates the status is "Disabled".<br><br>* `configuring`: Indicates the status is "Deploying".<br><br><br>If this parameter is not specified, it means that the domain names are not filtered. |`online,configuring` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|CertNotConfig |Object[] |Indicates the list of domains that can be associated with the `CertId` but are not yet associated with any certificate. | |
|Domain |String |Indicates one of the domain names in the list. |`img.example.com` |
|Status |String |Indicates the status of the domain name. This parameter has the following values:<br><br><br>* `online`: Indicates the status is "Enabled".<br><br>* `offline`: Indicates the status is "Disabled".<br><br>* `configuring`: Indicates the status is "Deploying". |`offline` |
|DomainLock |Object |Indicates whether this domain name is locked. If a domain name is locked, you cannot modify its configurations. | |
|Remark |String |Indicates the reason why the domain name is locked.<br><br><br>* If the `Status` in the `DomainLock` struct is `on`, this parameter specifies the reason why the domain name is locked.<br><br>* If the `Status` is `off`, the value of this parameter is empty (""). |`some reason` |
|Status |String |Indicates the lock status of this domain name. The parameter can take the following values:<br><br><br>* `on`: Indicates that this domain name is locked.<br><br>* `off`: Indicates that this domain name is not locked. |`off` |
|SpecifiedCertConfig |Object[] |Indicates the list of domains that are already associated with the `CertId`. | |
|Domain |String |Indicates one of the domain names in the list. |`abc.example.com` |
|Status |String |Indicates the status of the domain name. This parameter has the following values:<br><br><br>* `online`: Indicates the status is "Enabled".<br><br>* `offline`: Indicates the status is "Disabled".<br><br>* `configuring`: Indicates the status is "Deploying". |`configuring` |
|CerStatus |String |Indicates the status of the certificate whose ID is `CertID`. The parameter can take the following values:<br><br><br>* `running`: Indicates the certificate`s validity period is more than 30 days.<br><br><br>\|\|<br><br><br>* `expired`: Indicates the certificate has expired.<br><br>* `expiring_soon`: Indicates the certificate`s validity period is less than or equal to 30 days, but it has not yet expired.<br><br><br>\|\| |`expiring_soon` |
|DomainLock |Object |Indicates whether this domain name is locked. If a domain name is locked, you cannot modify its configurations. | |
|Remark |String |Indicates the reason why the domain name is locked.<br><br><br>* If the `Status` in the `DomainLock` struct is `on`, this parameter specifies the reason why the domain name is locked.<br><br>* If the `Status` is `off`, the value of this parameter is empty (""). |`some reason` |
|Status |String |Indicates the lock status of this domain name. The parameter can take the following values:<br><br><br>* `on`: Indicates that this domain name is locked.<br><br>* `off`: Indicates that this domain name is not locked. |`on` |
|OtherCertConfig |Object[] |Indicates the list of domains that can be associated with the `CertId` but are already associated with other certificates. | |
|Domain |String |Indicates one of the domain names in the list. |`www.example.com` |
|Status |String |Indicates the status of the domain name. This parameter has the following values:<br><br><br>* `online`: Indicates the status is "Enabled".<br><br>* `offline`: Indicates the status is "Disabled".<br><br>* `configuring`: Indicates the status is "Deploying". |`online` |
|CerStatus |String |Indicates the status of the certificate associated with this domain name. The parameter can take the following values:<br><br><br>* `running`: Indicates the certificate`s validity period is more than 30 days.<br><br><br>\|\|<br><br><br>* `expired`: Indicates the certificate has expired.<br><br>* `expiring_soon`: Indicates the certificate`s validity period is less than or equal to 30 days, but it has not yet expired.<br><br><br>\|\| |`running` |
|DomainLock |Object |Indicates whether this domain name is locked. If a domain name is locked, you cannot modify its configurations. | |
|Remark |String |Indicates the reason why the domain name is locked.<br><br><br>* If the `Status` in the `DomainLock` struct is `on`, this parameter specifies the reason why the domain name is locked.<br><br>* If the `Status` is `off`, the value of this parameter is empty (""). |`some reason` |
|Status |String |Indicates the lock status of this domain name. The parameter can take the following values:<br><br><br>* `on`: Indicates that this domain name is locked.<br><br>* `off`: Indicates that this domain name is not locked. |`off` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCertConfig&Version=2021-03-01
{
    "CertId": "cert-c19"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202207131255000102121011030C701AF8",
        "Action": "DescribeCertConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertNotConfig": [
            {
                "CerStatus": null,
                "Domain": "test.example.com",
                "Status": "online"
            }
        ],
        "OtherCertConfig": [
            {
                "CerStatus": "running",
                "Domain": "img.example.com",
                "Status": "online"
            }
        ],
        "SpecifiedCertConfig": [
            {
                "CerStatus": "running",
                "Domain": "www.example.com",
                "Status": "online"
            }
        ]
    }
}
```
