---
title: "UploadCertificate - Uploading a server certificate"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-UploadCertificate"
---

Call the UploadCertificate API to upload a server certificate.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The maximum number of certificates that can be uploaded per account per region is 100.

* Submit up to 10 API requests per second.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UploadCertificate&serviceCode=alb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|u7PQ8R">必选</span> `Example: UploadCertificate`

The interface name. The current API name is `UploadCertificate`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|P-V8O3">必选</span> `Example: 2020-04-01`

The interface version. Current API version is `2020-04-01`.



**CertificateName ** <span data-label="purple"> String </span>`optional` `Example: test`

Certificate name. The specific rules are as follows:


* Cannot start with http:// or https://.

* Must start with a letter or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.

* If left blank, it defaults to the certificate ID.



**CertificateType ** <span data-label="purple"> String  </span><span data-api-tag="require|HsdSAr">必选</span> `Example: Server`

Certificate type. Valid values:


* Server: Server certificate.



**PublicKey ** <span data-label="purple"> String  </span><span data-api-tag="require|jchdmA">必选</span> `Example: public`

Certificate public key, format:

\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-

Server public key certificate (BASE 64 Encoding)

\-\-\-\-\-END CERTIFICATE\-\-\-\-\-

!!! No blank lines in the middle!!!

\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-

Intermediate Issuing Authority Public Key Certificate (BASE 64 Encoding)

\-\-\-\-\-END CERTIFICATE\-\-\-\-\-



**PrivateKey ** <span data-label="purple"> String </span><span data-api-tag="require|zR8QoX">必选</span> `Example: private`

Certificate private key, format:


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



**Description ** <span data-label="purple"> String </span>`optional` `Example: test`

Certificate description.



**ProjectName ** <span data-label="purple">String</span> `optional` `Example value: default`

Name of the project to which the certificate belongs.



**Tags.N.Key ** <span data-label="purple"> String[] </span>`optional` `Example: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the custom tag. The specific rules are as follows:


* Must be 1 to 128 characters.

* Case\-sensitive.

* Cannot start with any case‑insensitive combination of volc: or sys:.

* Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

* Duplicate tag keys are not allowed for the same resource.



**Tags.N.Value ** <span data-label="purple"> String[]  </span>`optional` `Example: Tags.1.Value=v1&Tags.2.Value=v2`

The tag value of the custom tag. To provide this parameter, provide Tags.N.Key first. The specific rules are as follows:


* The length limit is 0 to 256 characters.

* Case\-sensitive.

* Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`Example: 20210816110638****2514606306AF947C`

Request ID.



**CertificateId ** <span data-label="purple">String</span> `Example: cert-*****`

Certificate ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=UploadCertificate&Version=2020-04-01&CertificateName=***&PublicKey=***&PrivateKey=*** HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "UploadCertificate",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
     },
    "Result": {
        "RequestId": "20210816110638****2514606306AF947C",
        "CertificateId": "cert-****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

If the response body contains an Error field, it indicates the API request failed. This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Error-codes).


|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |InvalidCertificateName.Malformed |The specified CertificateName is malformed. |The specified CertificateName parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidCertificateType.Malformed |The specified CertificateType is malformed. |The specified CertificateType parameter format is invalid. |
|400 |InvalidPublicKey.Malformed |The specified PublicKey is malformed. |The specified PublicKey format is invalid. |
|400 |InvalidPrivateKey.Malformed |The specified PrivateKey is malformed. |The format of the specified PrivateKey is invalid. |
|400 |InvalidPublicKey.PrivateKeyMismatch |The specified PublicKey and PrivateKey do not match. |The specified public key does not match the private key. |
|400 |OperationFailed.QueryProject |The request on the specified resource failed due to the query on project failed. |The request to operate on this resource failed because the project query failed. |
|400 |QuotaExceed.CertPerRegion |You've reached the limit on the number of server certificates the current region you can create in, usage xx/xx. |The maximum number of server certificates that can be created in the current region has been reached. Used: xxx. Quota: xxx |
|400 |OperationFailed.AddIntoProjectFailed |The request on the specified resource failed due to adding it into the project failed. |The request to operate on this resource failed because adding the resource to the project failed. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|400 |InvalidTags.Key.Malformed |The specified Tags.Key is malformed. |The specified Tags.Key parameter format is invalid. |
|400 |InvalidTags.Value.Malformed |The specified Tags.Value is malformed. |The specified Tags.Value parameter format is invalid. |
|400 |InvalidTags.Key.Duplicated |The specified Tags.Key is duplicated. |The specified Tags.Key is duplicated. |
