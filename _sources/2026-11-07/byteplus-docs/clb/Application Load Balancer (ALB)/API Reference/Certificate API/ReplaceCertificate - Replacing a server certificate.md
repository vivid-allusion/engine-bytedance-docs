---
title: "ReplaceCertificate - Replacing a server certificate"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ReplaceCertificate"
---

Call the ReplaceCertificate API to replace the server certificate.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 5 API requests per second.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Method: **GET**

* URL:  **/?Action=ReplaceCertificate&Version=2020\-04\-01**


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ReplaceCertificate&groupName=%E8%AF%81%E4%B9%A6&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|TWApxV">必选</span> `Example: ReplaceCertificate`

Action to execute. Set the value to ReplaceCertificate.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|qvE8w8">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**OldCertificateId ** <span data-label="purple">string </span><span data-api-tag="require|oZ4ZKP">必选</span> `Example: cert-123***765`

ID of the server certificate to be replaced.



**CertificateId ** <span data-label="purple">string </span>`optional` `Example: cert-123***765`

The ID of the new certificate uploaded from ALB.

When replacing with an existing certificate, i.e., UpdateMode is stock and CertificateSource is alb, this parameter is required and takes effect.



**ProjectName ** <span data-label="purple">string </span>`optional` `Example: test`

The project to which the certificate belongs. When UpdateMode is set to new, this field takes effect.



**CertificateName ** <span data-label="purple">string </span>`optional` `Example: test`

Certificate name.


* Cannot start with http:// or https://.

* Must start with a letter or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.

* If left blank, it defaults to the certificate ID.



**CertificateSource ** <span data-label="purple">string </span>`optional` `Example: cert_center`

The source of the new server certificate. Valid values:


* alb: Indicates the certificate uploaded via ALB.

* cert_center: Indicates a certificate uploaded via BytePlus Certificate Center.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the replacement mode is using an existing certificate, i.e., the value of UpdateMode is stock, this parameter is required and takes effect. If left blank, it defaults to alb.</div>




**Description ** <span data-label="purple">string </span>`optional` `Example: test`

Certificate description.



**CertCenterCertificateId ** <span data-label="purple">string </span>`optional` `Example: cert-123***765`

New certificate ID from Certificate Center.

When replacing with an existing certificate, i.e., UpdateMode is stock and CertificateSource is cert_center, this parameter is required and takes effect.



**PrivateKey ** <span data-label="purple">string </span>`optional` `Example: private`

Certificate private key.

When UpdateMode is new, this field is required and takes effect. The format is as follows:


* Format 1:


\-\-\-\-\-BEGIN RSA PRIVATE KEY\-\-\-\-\-

Certificate private key (BASE 64 encoding)

\-\-\-\-\-END RSA PRIVATE KEY\-\-\-\-\-


* Format 2:


\-\-\-\-\-BEGIN EC PARAMETERS\-\-\-\-\-

Certificate private key (BASE 64 encoding)

\-\-\-\-\-END EC PARAMETERS\-\-\-\-\-

\-\-\-\-\-BEGIN EC PRIVATE KEY\-\-\-\-\-

Certificate private key (BASE 64 encoding)

\-\-\-\-\-END EC PRIVATE KEY\-\-\-\-\-



**PublicKey ** <span data-label="purple">string </span>`optional` `Example: public`

The certificate public key. When UpdateMode is new, this field is required and takes effect. The format is as follows:

\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-

Server public key certificate (BASE 64 Encoding)

\-\-\-\-\-END CERTIFICATE\-\-\-\-\-

!!! No blank lines in the middle!!!

\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-

Intermediate Issuing Authority Public Key Certificate (BASE 64 Encoding)

\-\-\-\-\-END CERTIFICATE\-\-\-\-\-



**UpdateMode ** <span data-label="purple">string </span><span data-api-tag="require|B62dE4">必选</span> `Example: new`

The mode for replacing the certificate. Valid values:


* new: Upload a new certificate to replace.

* stock: Replace with an existing certificate.



**Tags.N.Value ** <span data-label="purple">string[] </span>`optional` `Example: Tags.1.Value=v1&Tags.2.Value=v2`

The tag value of the custom tag.


* To provide this parameter, provide Tags.N.Key first.

* The specific rules are as follows:

   * The length limit is 0 to 256 characters.

   * Case\-sensitive.

   * Must not start or end with a space.

   * May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).



**Tags.N.Key ** <span data-label="purple">string[] </span>`optional` `Example: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the custom tag. The specific rules are as follows:


* Must be 1 to 128 characters.

* Case\-sensitive.

* Cannot start with any case‑insensitive combination of volc: or sys:.

* Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

* Duplicate tag keys are not allowed for the same resource.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210816110638****2514606306AF947C`

Request ID.



**CertificateId ** <span data-label="purple">string </span>`Example: cert-*****`

New certificate ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=ReplaceCertificate&OldCertificateId=cert-2jqh****hsx&PublicKey=***&PrivateKey=***&CertificateName=test&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "ReplaceCertificate",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202108161106****22514606306AF947C",
        "CertificateId": "cert-****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidCertificateType.FunctionMismatch |The specified Certificate's type and Function do not match. |The type of the specified certificate does not match the expected functionality. |
|400 |InvalidLoadBalancer.InvalidStatus |The related LoadBalancer is not in the correct status for the request. |The associated ALB instance is in a state that cannot respond to this request. |
|400 |InvalidCertificate.InvalidStatus |The specified Certificate is not in the correct status for the request. |The specified certificate is in a status that cannot respond to this request. |
|400 |OperationFailed.AddIntoProjectFailed |The request on the specified resource failed due to adding it into the project failed. |The request to operate on this resource failed because adding the resource to the project failed. |
|400 |QuotaExceed.CertPerRegion |You've reached the limit on the number of server certificates the current region you can create in, usage xx/xx. |The maximum number of server certificates that can be created in the current region has been reached. Used: xxx. Quota: xxx |
|400 |InvalidUpdateMode.Malformed |The specified UpdateMode is malformed. |The specified UpdateMode parameter format is invalid. |
|400 |InvalidOldCertificateType.CertificateTypeMismatch |The specified new certificate type and old certificate type do not match. The specified new certificate must be the same type as the old one. |The specified new certificate type does not match the old certificate type. The specified new certificate must be of the same type as the old certificate. |
|400 |InvalidServerCertificate.InvalidStatus |The specified Server Certificate is not in the correct status for the request. |The specified server certificate is in a status that cannot respond to this request. |
|400 |OperationFailed.QueryProject |The request on the specified resource failed due to the query on project failed. |The request to operate on this resource failed because the project query failed. |
|400 |InvalidOldServerCertificate.InvalidStatus |The specified Old Server Certificate is not in the correct status for the request. |The specified server certificate is in a status that cannot respond to this request. |
|400 |OperationDenied.NoListenerBound |The request on the specified certificate is denied due to no listener bound on the specified old certificate. |Because this old certificate is not bound to any listener, the operation request for this certificate is rejected. |
|400 |OperationDenied.ListenersBoundCountExceed |The request on the specified certificate is denied due to the count of listeners bound on the specified old certificate exceeding limit. |Because the number of listeners bound to this old certificate exceeds the limit, the operation request for this certificate is rejected. |
|400 |InvalidCertificateName.Malformed |The specified CertificateName is malformed. |The specified CertificateName parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidCertificateType.Malformed |The specified CertificateType is malformed. |The specified CertificateType parameter format is invalid. |
|400 |InvalidPublicKey.Malformed |The specified PublicKey is malformed. |The specified PublicKey format is invalid. |
|400 |InvalidPrivateKey.Malformed |The specified PrivateKey is malformed. |The specified PrivateKey format is invalid. |
|400 |InvalidPublicKey.PrivateKeyMismatch |The specified PublicKey and PrivateKey do not match. |The specified public key does not match the private key. |
|400 |InvalidCertificate.Duplicated |The specified Certificate is duplicated. The specified new certificate is not allowed to be similar to the old certificate. |The specified certificate is duplicated. The new certificate cannot be the same as the old certificate. |
|400 |InvalidCertificateSource.Malformed |The specified CertificateSource is malformed. |The format of the specified CertificateSource is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'CertificateId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as Certificate ID. |
|400 |InvalidCertificateServiceSSLCertificate.InvalidStatus |The specified Certificate Service SSL Certificate is not in the correct status for the request. Please check if the certificate has been issued. |The specified Certificate Center SSL certificate is in a status that cannot respond to this request. Confirm the certificate has been issued. |
|400 |OperationFailed.QueryIAM |The request on the specified resource failed due to the query on IAM failed. |The request to operate on this resource failed because the IAM request failed. |
|400 |OperationFailed.QueryCertificateService |The request on the specified resource failed due to the query on Certificate Service failed. |The request to operate on this resource failed because the request to the Certificate Center service failed. |
|400 |InvalidCertificateId.Duplicated |The specified CertificateId is duplicated. Certificates in one listener can not be same. |The specified CertificateId is duplicated. Certificates under a single listener cannot be duplicated. |
|400 |InvalidTags.Key.Malformed |The specified Tags.Key is malformed. |The specified Tags.Key parameter format is invalid. |
|400 |InvalidTags.Value.Malformed |The specified Tags.Value is malformed. |The specified Tags.Value parameter format is invalid. |
|400 |InvalidTags.Key.Duplicated |The specified Tags.Key is duplicated. |The specified Tags.Key is duplicated. |
|400 |QuotaExceed.ListenerPerCert |You've reached the limit on the number of listeners per server certificate you can associate with, resource xxx, usage xx/xx. |The maximum number of listeners that can be associated with a single server certificate has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|404 |InvalidServerCertificate.NotFound |The specified Server Certificate does not exist. |The specified server certificate does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidOldServerCertificate.NotFound |The specified Old Server Certificate does not exist. |The specified old server certificate does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
