---
title: "UploadCertificate - Uploading a certificate"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/UploadCertificate"
---

Call the UploadCertificate API to upload a server certificate.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is not recommended to call this API. For easier unified certificate management, it is recommended that you call <a href="https://docs.byteplus.com/en/docs/6638/1186018">ImportCertificate</a> from the certificate center to upload SSL certificates.</div>


<span id=".5L2_55So6K-05piO"></span>
## Instructions

Under one account, a maximum of 100 certificates can be uploaded per region.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UploadCertificate&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|eF1XLQ">必选</span> `Example: UploadCertificate`

Action to execute. Set the value to **UploadCertificate**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|rEPE2a">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**CertificateName ** <span data-label="purple">String </span>`optional` `Example: mycert1`

Certificate name.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.

* If left blank, it defaults to the certificate ID.



**PublicKey ** <span data-label="purple">String </span><span data-api-tag="require|vqrthI">必选</span> `Example: pubkeycontent`

The public key content of the certificate.



**PrivateKey ** <span data-label="purple">String </span><span data-api-tag="require|VKMAzX">必选</span>`Example: privatekeycontent`

The private key content of the certificate.



**Description ** <span data-label="purple">String </span>`optional` `Example: mycert`

The certificate description. Default: Empty string.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

Name of the project to which the certificate belongs. If left blank, it defaults to default.



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The tag key.


* N represents the sequence number of a tag key. Valid range: 1 to 20.

* Separate multiple tag keys with &.

* Must not start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Duplicate tag keys are not allowed for the same resource.</div>




**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: value1`

The tag value.


* N represents the sequence number of a tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters. If left blank, this parameter defaults to an empty string.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete it.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**CertificateId ** <span data-label="purple">String </span>`Example: cert-3tjuxoukkq3vj0ww****`

Certificate ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=UploadCertificate&Version=2020-04-01&CertificateName=mycert1&PublicKey=pubkeycontent&PrivateKey=privatekeycontent&Description=mycert&ProjectName=default&Tags.1.Key=key1&Tags.1.Value=value1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UploadCertificate",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "CertificateId": "cert-3tjuxoukkq3vj0ww****",
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidCertificateDescription.Malformed |The specified CertificateDescription is malformed. |The specified CertificateDescription parameter format is invalid. |
|400 |InvalidCertificateLength.Malformed |The specified CertificateLength is malformed. |The specified CertificateLength format is invalid. |
|400 |InvalidCertificateName.Malformed |The specified CertificateName is malformed. |The specified CertificateName parameter format is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidPrivateKey.Malformed |The specified PrivateKey is malformed. |The specified PrivateKey format is invalid. |
|400 |InvalidProject.Malformed |The specified Project is malformed. |The format of the specified Project is invalid. |
|400 |InvalidPublicKey.Malformed |The specified PublicKey is malformed. |The specified PublicKey format is invalid. |
|400 |InvalidPublicKey.PrivateKeyMisMatch |The PublicKey and PrivateKey are not matched. |The specified public key does not match the private key. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.ServiceManagedTag |You've reached the limit on the number of service managed tags that you can create. |You have reached the limit for the number of managed resource tag key\-value pairs that can be created in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'PublicKey'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as PublicKey. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'PrivateKey'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as PrivateKey. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |QuotaExceed.CertificateNumber |You've reached the limit on the number of Certificate that you can create. |The quota limit for the number of certificates that can be created has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |Forbidden |You are not authorized to perform operations on the system tag. |No permission to tag the specified resource with a system tag. |
|403 |Forbidden |You are not authorized to perform operations on the service managed tag. |No permission to tag the specified resource with managed tags. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
