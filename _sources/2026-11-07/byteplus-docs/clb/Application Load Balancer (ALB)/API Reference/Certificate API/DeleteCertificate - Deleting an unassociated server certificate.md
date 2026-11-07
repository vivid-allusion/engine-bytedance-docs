---
title: "DeleteCertificate - Deleting an unassociated server certificate"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DeleteCertificate"
---

Call the DeleteCertificate API to delete server certificates that are not associated with any listener.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Submit up to 5 API requests per second.

* The certificate must be disassociated from the listener before it can be deleted.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteCertificate&groupName=%E8%AF%81%E4%B9%A6&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|LaNpQK">必选</span> `Example: DeleteCertificate`

Action to execute. Set the value to DeleteCertificate.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|fYcL7Q">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CertificateId ** <span data-label="purple">string </span><span data-api-tag="require|1xYX7u">必选</span> `Example: cert-*****`

Certificate ID to be deleted.



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
GET /?Action=DeleteCertificate&CertificateId=cert-123***765&Version=2020-04-01 HTTP/1.1
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
        "Action": "DeleteCertificate",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210816110638****2514606306AF947C"
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
|400 |InvalidServerCertificateListener.InUse |The specified Server Certificate is being used by listeners. |The specified server certificate is in use by a listener. |
|400 |InvalidCertificate.InvalidStatus |The specified Certificate is not in the correct status for the request. |The specified certificate is in a status that cannot respond to this request. |
|400 |OperationFailed.RemoveFromProjectFailed |The request on the specified resource failed due to removing it from the project failed. |The operation request for the resource failed because removing it from the project was unsuccessful. |
|404 |InvalidServerCertificate.NotFound |The specified Server Certificate does not exist. |The specified server certificate does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
