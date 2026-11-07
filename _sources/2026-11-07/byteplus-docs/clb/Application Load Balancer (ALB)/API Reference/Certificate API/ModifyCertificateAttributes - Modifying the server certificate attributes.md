---
title: "ModifyCertificateAttributes - Modifying the server certificate attributes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-ModifyCertificateAttributes"
---

Call the ModifyCertificateAttributes API to modify the server certificate attributes.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 10 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyCertificateAttributes&groupName=%E8%AF%81%E4%B9%A6&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|T9yDvC">必选</span> `Example: ModifyCertificateAttributes`

Action to execute. Set the value to ModifyCertificateAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|EpZQnF">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**Description ** <span data-label="purple">string </span>`optional` `Example: tes-Description`

Certificate description.



**CertificateName ** <span data-label="purple">string </span>`optional` `Example: test`

Certificate name.


* Cannot start with http:// or https://.

* Must start with a letter or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.



**CertificateId ** <span data-label="purple">string </span><span data-api-tag="require|pvTUd2">必选</span> `Example: cert-123***765`

Certificate ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210816110638****2514606306AF947C`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=ModifyCertificateAttributes&CertificateId=cert-2fe5jqh****hs5oxruwk7x9ze&CertificateName=test&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "ModifyCertificateAttributes",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202108161106****22514606306AF947C"
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
|400 |InvalidCertificate.InvalidStatus |The specified Certificate is not in the correct status for the request. |The specified certificate is in a status that cannot respond to this request. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidCertificateName.Malformed |The specified CertificateName is malformed. |The specified CertificateName parameter format is invalid. |
|400 |InvalidCertificateType.FunctionMismatch |The specified Certificate's type and Function do not match. |The type of the specified certificate does not match the expected functionality. |
|404 |InvalidServerCertificate.NotFound |The specified Server Certificate does not exist. |The specified server certificate does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
