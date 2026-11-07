---
title: "ModifyNLBListenerAdditionalCertificates - Attaching or detaching an additional certificate for TLS listeners"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyNLBListenerAdditionalCertificates"
---

Call the ModifyNLBListenerAdditionalCertificates API to attach or detach additional certificates to a specified TLS listener.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyNLBListenerAdditionalCertificates&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: ModifyNLBListenerAdditionalCertificates`

Action to execute. Set the value to ModifyNLBListenerAdditionalCertificates.

**Version ** String必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**ListenerId ** String必选 `Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.

**AssociateCertificateSource ** String`optional` `Example: SSL`

The type of extended certificate to be attached. Valid values:

* SSL: SSL certificate.

* PCALeaf: PCA private certificate.

> When the AssociateCertificateSource parameter is specified, the AssociateCertificateIds.N parameter becomes mandatory, otherwise the operation will fail.

**AssociateCertificateIds.N ** String`optional` `Example: cert-bp1o94dp5i6eb****`

Additional certificates to be attached.

* Parameter \- N: Represents the serial number of the additional certificate. The valid range is 1 to 15.

* Separate additional certificate IDs with ampersands (&).

**DisassociateCertificateIds.N ** String`optional` `Example: cert-bp2o05dp6i7eb****`

Additional certificates to be detached.

* Parameter \- N: Represents the serial number of the additional certificate. The valid range is 1 to 15.

* Separate additional certificate IDs with ampersands (&).

## Response parameters

**RequestId ** String`Example: 2024092952539010225146063030****`

Request ID.

## Request examples

```json
GET /?Action=ModifyNLBListenerAdditionalCertificates&Version=2020-04-01&ListenerId=lsn-2fek3rgsxhrsw5oxruwec**** HTTP/1.1 
Host: clb.cn-beijing.byteplusapi.com.cn 
Date: 20260310T094038Z 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyNLBListenerAdditionalCertificates",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2024092952539010225146063030****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidAssociateCertificateIds.AssociateCertificateSourceMismatch |The specified AssociateCertificateIds is not matched with AssociateCertificateSource. |The specified AssociateCertificateIds does not match AssociateCertificateSource. |
|400 |InvalidAssociateCertificateIds.Malformed |The specified AssociateCertificateIds is malformed. |The specified AssociateCertificateIds parameter format is invalid. |
|400 |InvalidAssociateCertificateSource.Malformed |The specified AssociateCertificateSource is malformed. |The specified AttachCertificateSource parameter format is invalid. |
|400 |InvalidCertificate.DomainTotalCount |The specified Certificate does not support this action, due to the total number of the certificate domain is illegal. |The current action is not supported because the total number of the specified certificate's domains is invalid. |
|400 |InvalidCertificate.DomainTotalLength |The specified Certificate does not support this action, due to the total length of the certificate domain is illegal. |The specified certificate does not support the current action because its domain name length is invalid. |
|400 |InvalidCertificate.UnSupportAction |The specified Certificate does not support this action, due to the content of the certificate is illegal. |The specified certificate is malformed and does not support the current operation. |
|400 |InvalidCertificateLength.Malformed |The specified CertificateLength is malformed. |The specified CertificateLength format is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidDisassociateCertificateIds.Malformed |The specified DisassociateCertificateIds is malformed. |The specified DisassociateCertificateIds parameter format is invalid. |
|400 |InvalidListener.InvalidStatus |The specified Listener is not in the correct status for the request. |The specified listener cannot respond to this request due to its status. |
|400 |InvalidListenerProtocol.UnSupportAction |The specified Protocol of Listener does not support this action. |The specified listener does not support this operation due to its protocol type. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancerBillingStatus.InvalidStatus |The specified LoadBalancer is not in the correct billing status for the request. |The specified load balancer cannot respond to this request due to its billing status. |
|400 |InvalidPrivateKey.Malformed |The specified PrivateKey is malformed. |The specified PrivateKey format is invalid. |
|400 |InvalidPublicKey.Malformed |The specified PublicKey is malformed. |The specified PublicKey format is invalid. |
|400 |InvalidPublicKey.PrivateKeyMisMatch |The PublicKey and PrivateKey are not matched. |The specified public key does not match the private key. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |LimitExceeded.AdditionalCertificateNumber |You've reached the limit on the number of additional certificates that you can operate. |You have reached the maximum number of additional certificates that can be processed in a single operation. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ListenerId'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as ListenerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |OperationFailed.QueryPcaService |The request for the specified resource operation failed due to an abnormal access issue with the pca service. |The operation request on the specified resource failed due to an access exception with the Certificate Center PCA service. |
|400 |QuotaExceed.AdditionalCertificateNumber |You've reached the limit on the number of additional certificates that you can create. |You have reached the quota limit for additional certificates per listener. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidAction.NotFound |The specified Action does not exist. |The specified Action does not exist. |
|404 |InvalidCACertificate.NotFound |The specified CACertificate does not exist. |The specified CA certificate does not exist. |
|404 |InvalidCertificate.NotFound |The specified Certificate does not exist. |The specified certificate does not exist. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |ServiceRoleForLoadBalancer.NotFound |ServiceRoleForLoadBalancer does not exist. |The service\-attached role of the load balancer does not exist. |
|409 |InvalidCertificate.Conflict |The specified certificate already exists. |The specified certificate already exists. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
