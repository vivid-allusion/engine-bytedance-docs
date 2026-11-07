---
title: "DeleteCertificate - Deleting a certificate"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DeleteCertificate"
---

Call the DeleteCertificate API to delete a certificate.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteCertificate&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|8F9mMb">必选</span>`Example: DeleteCertificate`

Action to execute. Set the value to **DeleteCertificate**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|QqDxYP">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**CertificateId ** <span data-label="purple">String </span><span data-api-tag="require|kTJqC9">必选</span> `Example: cert-3tjuxoukkq3vj0ww****`

Certificate ID.

You can call the [DescribeCertificates](https://docs.byteplus.com/en/docs/clb/DescribeCertificates) API to query the certificate ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteCertificate&Version=2020-04-01&CertificateId=cert-3tjuxoukkq3vj0ww****
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
        "Action": "DeleteCertificate",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidCertificate.InUse |The specified Certificate is in use. |The specified certificate is currently in use. |
|400 |InvalidCertificate.InvalidStatus |The specified Certificate is not in the correct status for the request. |The specified certificate is in a status that cannot respond to this request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'CertificateId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as CertificateId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request does not contain required parameters. Ensure the request includes all required parameters, such as . |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidCertificate.NotFound |The specified Certificate does not exist. |The specified certificate does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
