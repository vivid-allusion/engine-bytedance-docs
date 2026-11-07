---
title: "ModifyListenerDomainExtensions - Managing the additional domains of an HTTPS listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyListenerDomainExtensions"
---

Use the ModifyListenerDomainExtensions API to manage the additional domains of an HTTPS listener.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Add, modify, or remove additional domains, where a single operation supports up to 20 domains.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyListenerDomainExtensions&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|VZAu5k">必选</span> `Example: ModifyListenerDomainExtensions`

Action to execute. Set the value to **ModifyListenerDomainExtensions**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Hs4xGy">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ListenerId ** <span data-label="purple">String </span><span data-api-tag="require|DXySN5">必选</span> `Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.

You can call the [DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) API to query the listener ID.



**AddDomainExtensions.N.Domain ** <span data-label="purple">String </span>`optional` `Example: www.test.com`

The domain name of the additional domain to be added, supporting wildcard domains and exact domains. The requirements are as follows:


* Must contain at least one `.` but must not start or end with `.`.

* Only letters, numbers, `.`, `-`, and `*` are allowed.

* Length must be between 1 and 128 characters.

* Wildcard domain: Use `*` to replace one or more characters.

   * `*` must be at the beginning or end of the domain name.

   * `*` cannot appear twice in the same domain name.

   * No characters other than `.` are allowed before or after `*`.

   * Valid examples: `*.com, www.test.*`.

   * Invalid examples: `*aaa.com`, `www.*.com`.

* Exact Domain Name​​: Must comply with domain name specifications (e.g., `www.test.com`).



**AddDomainExtensions.N.CertificateSource ** <span data-label="purple">String </span>`optional` `Example: cert_center`

The certificate source of the additional domain to be added. Valid values:


* cert_center: SSL certificate from the BytePlus Certificate Center.



**AddDomainExtensions.N.CertCenterCertificateId ** <span data-label="purple">String </span>`optional` `Example: cert-ahfhds****`

The certificate ID of the additional domain to be added.



**ModifyDomainExtensions.N.DomainExtensionId ** <span data-label="purple">String </span>`optional` `Example: de-fskghsj****`

ID of the additional domain to be modified.



**ModifyDomainExtensions.N.CertificateSource ** <span data-label="purple">String </span>`optional` `Example: cert_center`

The certificate source of the additional domain to be modified. Valid values:


* cert_center: SSL certificate from the BytePlus Certificate Center.



**ModifyDomainExtensions.N.CertCenterCertificateId ** <span data-label="purple">String </span>`optional` `Example: cert-dar48thejr****`

The certificate ID of the additional domain to be modified.



**RemoveDomainExtensions.N.DomainExtensionId ** <span data-label="purple">String </span>`optional` `Example: de-wtrg1fdjgh53df***`

The ID of the additional domain to be removed.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyListenerDomainExtensions&Version=2020-04-01&ListenerId=lsn-2fek3rgsxhrsw5oxruwec****&AddDomainExtensions.1.Domain=www.test.com&AddDomainExtensions.1.CertificateSource=cert_center&AddDomainExtensions.1.CertCenterCertificateId=cert-ahfhds****&ModifyDomainExtensions.1.DomainExtensionId=de-fskghsj****&ModifyDomainExtensions.1.CertificateSource=cert_center&ModifyDomainExtensions.1.CertCenterCertificateId=cert-dar48thejr****&RemoveDomainExtensions.1.DomainExtensionId=de-wtrg1fdjgh53df***
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
        "Action": "ModifyListenerDomainExtensions",
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
|400 |InvalidAddDomainExtensions.CertificateSource.Malformed |The specified AddDomainExtensions.CertificateSource is malformed. |The specified AddDomainExtensions.CertificateSource parameter format is invalid. |
|400 |InvalidAddDomainExtensions.Domain.Malformed |The specified AddDomainExtensions.Domain is malformed. |The specified AddDomainExtensions.Domain parameter format is invalid. |
|400 |InvalidCertificate.UnSupportAction |The specified Certificate does not support this action, due to the content of the certificate is illegal. |The specified certificate is malformed and does not support the current operation. |
|400 |InvalidCertificateLength.Malformed |The specified CertificateLength is malformed. |The specified CertificateLength format is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidListenerProtocol.UnSupportAction |The specified Protocol of Listener does not support this action. |The specified listener does not support this operation due to its protocol type. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidModifyDomainExtensions.CertificateSource.Malformed |The specified ModifyDomainExtensions.CertificateSource is malformed. |The specified ModifyDomainExtensions.CertificateSource parameter format is invalid. |
|400 |InvalidPrivateKey.Malformed |The specified PrivateKey is malformed. |The specified PrivateKey format is invalid. |
|400 |InvalidPublicKey.Malformed |The specified PublicKey is malformed. |The specified PublicKey format is invalid. |
|400 |InvalidPublicKey.PrivateKeyMisMatch |The PublicKey and PrivateKey are not matched. |The specified public key does not match the private key. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |LimitExceeded.AddDomainExtensionNumber |You've reached the limit on the number of adding domain extensions that you can operate. |The maximum number of additional domains that can be added in a single operation has been reached. |
|400 |LimitExceeded.ModifyDomainExtensionNumber |You've reached the limit on the number of modifying domain extensions that you can operate. |The maximum number of additional domains that can be modified in a single operation has been reached. |
|400 |LimitExceeded.RemoveDomainExtensionNumber |You've reached the limit on the number of removing domain extensions that you can operate. |The maximum number of additional domains that can be removed in a single operation has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'AddDomainExtensions.CertificateSource'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as AddDomainExtensions.CertificateSource. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ModifyDomainExtensions.DomainExtensionId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ModifyDomainExtensions.DomainExtensionId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ListenerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ListenerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ModifyDomainExtensions.CertCenterCertificateId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ModifyDomainExtensions.CertCenterCertificateId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'AddDomainExtensions.Domain'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as AddDomainExtensions.Domain. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'RemoveDomainExtensions.DomainExtensionId'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as RemoveDomainExtensions.DomainExtensionId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'AddDomainExtensions.CertCenterCertificateId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as AddDomainExtensions.CertCenterCertificateId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ModifyDomainExtensions.CertificateSource'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as ModifyDomainExtensions.CertificateSource. |
|400 |OperationFailed.QueryCertificateService |The request for the specified resource operation failed due to an abnormal access issue with the certificate center service. |The operation request on the specified resource failed due to an access exception with the Certificate Center service. |
|400 |QuotaExceed.DomainExtNumberEachListener |You've reached the limit on the number of DomainExtension that you can operate. |The maximum number of additional domains that can be associated with the listener has been reached. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to perform operations on the certificate of certificate center. |You are not authorized to operate on the specified certificate from the certificate center. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidCertificate.NotFound |The specified Certificate does not exist. |The specified certificate does not exist. |
|404 |InvalidDomainExtensions.NotFound |The specified DomainExtensions does not exist. |The specified additional domain does not exist. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|409 |InvalidAddDomainExtensions.DomainConflict |The specified AddDomainExtensions.Domain already exists. |The specified AddDomainExtensions.Domain already exists. |
|409 |InvalidDomainExtensionId.Conflict |The specified DomainExtensionId already exists in request. |The specified DomainExtensionId already exists in the request. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |InvalidLoadBalancer.Expired |The specified LoadBalancer has expired. |The specified CLB has expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
