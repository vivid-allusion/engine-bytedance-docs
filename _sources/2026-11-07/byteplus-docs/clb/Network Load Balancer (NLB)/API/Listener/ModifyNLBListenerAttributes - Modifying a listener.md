---
title: "ModifyNLBListenerAttributes - Modifying a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyNLBListenerAttributes"
---

You can call the ModifyNLBListenerAttributes API to modify a listener.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyNLBListenerAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

If you do not configure the following optional parameters, their existing values remain unchanged.



**Action ** <span data-label="purple">String </span><span data-api-tag="require|B7vw0d">必选</span> `Example: ModifyNLBListenerAttributes`

Action to execute. Set the value to ModifyNLBListenerAttributes.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|ukOG4X">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**ListenerId ** <span data-label="purple">String </span><span data-api-tag="require|wIL956">必选</span> `Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.

You can call the [DescribeNLBListeners](https://docs.byteplus.com/en/docs/clb/DescribeNLBListeners) API to get the listener ID.



**ListenerName ** <span data-label="purple">String </span>`optional` `Example: mylistener`

Listener name.


* Must start with a letter, number, or Chinese character. May include the following symbols: periods (.), underscore (_), and hyphen (\-).

* The length limit is 1 to 128 characters.



**ConnectionTimeout ** <span data-label="purple">Integer </span>`optional` `Example: 800`

The connection timeout period of the listener.


* When the parameter Protocol is TCP or TLS, the value range is 10\-900 seconds.

* When the parameter Protocol is UDP, the value range is 10\-120 seconds.



**Enabled ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Enable the listener. Valid values:


* true: Enabled.

* false: Disabled.



**ServerGroupId ** <span data-label="purple">String </span>`optional` `Example: rsp-bp1o94dp5i6ea****`

The Server Group ID attached to the listener.

You can call the [DescribeNLBServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups) API to query the server group ID.


* When it is TCP listener, the protocol of the backend server must be TCP.

* When it is UDP listener, the protocol of the backend server must be UDP.

* When it is TLS listener, the protocol of the backend server must be TCP. And does not support selecting the following server groups:

   * IP address\-type server groups are not supported to associate.

   * Server groups that do not support enabling the Proxy\-Protocol protocol.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a listener.`

Description of the listener.


* Must start with a letter or a Chinese character. It may contain numbers, half\-width commas ( , ), half\-width periods ( . ), underscores ( _ ), spaces ( ), equal signs ( = ), hyphens ( \- ), full\-width commas (， ), and full\-width periods ( 。 ).

* Must be 1 to 255 characters.



**CertificateSource ** <span data-label="purple">String </span>`optional` `Example: SSL`

The source of the server certificate for the TLS listener. Valid values:


* SSL: Certificate Center \- SSL certificate.

* PCALeaf: Certificate Center \- private CA's private certificate.



**CertificateId ** <span data-label="purple">String </span>`optional` `Example: cert-3tjuxoukkq3vj0ww****`

For the server certificate ID of a TLS listener, only private certificates issued by SSL certificates in BytePlus Certificate Center are supported.

> The SM certificate is currently in invite\-only beta. For trial requests, please contact your account manager.



**PCACertificateId ** <span data-label="purple">String </span>`optional` `Example: cert-3tjuxoukkq3vj0ww****`

The server certificate ID for the TLS listener. Only private certificates from the BytePlus Certificate Center Private CA are supported.

> Description:

> SM certificate and the private CA feature of the Certificate Center are currently in the invite\-only beta stage. To request a trial, please contact your account manager.



**CAEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Enable mutual authentication for the TLS listener. Valid values:


* true: Enable mutual authentication.

* false: Disable mutual authentication.

> This feature is currently in the invite\-only Beta stage. For a trial, contact your account manager.



**CACertificateSource ** <span data-label="purple">String </span>`optional` `Example: PCARoot`

The source of the CA certificate for the TLS listener. Valid values:


* PCARoot: Private CA's private root CA certificate.

* PCASub: Private sub\-CA certificate of private CA.

> Description:

> * When CAEnabled is set to true, this parameter is required.



**CACertificateId ** <span data-label="purple">String </span>`optional` `Example: pca-********`

For CA certificates associated with TLS listeners, BytePlus Certificate Center supports uploading certificates from both private root CA and private subordinate CA certificate modules.

> Description:

> * When CAEnabled is set to true, this parameter is required.

> * Certificate validity status: Enabled, Not Expired, and Not Revoked.

> * SM certificate is in the invite\-only Beta stage. For trial requests, please contact your account manager.



**SecurityPolicyType ** <span data-label="purple">String </span>`optional` `Example: system`

TLS security policy type. Valid values:


* custom: Custom policy.

* system: System policy.



**SecurityPolicyId ** <span data-label="purple">String </span>`optional` `Example: tls_cipher_policy_1_0`

TLS security policy ID, supporting both system security policies and custom security policies.


* System security policy values:

   * tls_cipher_policy_1_0

   * tls_cipher_policy_1_1

   * tls_cipher_policy_1_2

   * tls_cipher_policy_1_2_strict

   * tls_cipher_policy_1_2_strict_with_1_3

* Custom security policy: Pass in a custom security policy ID.


You can call the [DescribeNLBSecurityPolicies](https://docs.byteplus.com/en/docs/clb/DescribeNLBSecurityPolicies) API to query the ID of the custom security policy.



**Cps ** <span data-label="purple">Integer </span>`optional` `Example: 9`

New connection rate limit.


* Value range: 0~1000000.

* 0 means no rate limit.

* When new connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The new connections rate limiting feature is currently in invite\-only beta. Contact your account manager to try it.</div>




**MaxConnections ** <span data-label="purple">Integer </span>`optional` `Example: 0`

Max connection rate limiting.


* Value range: 0~10000000.

* 0 means no rate limit.

* When max connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The max connections rate limiting feature is currently in Invite\-only Beta. To request a trial, contact your account manager.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2024092952539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=ModifyNLBListenerAttributes&Version=2020-04-01&ListenerId=lsn-2fek3rgsxhrsw5oxruwec****&ListenerName=mylistener&ConnectionTimeout=800&Enabled=true&ServerGroupId=rsp-bp1o94dp5i6ea****&Description=This is a listener.&CertificateSource=SSL&CertificateId=cert-3tjuxoukkq3vj0ww****&PCACertificateId=cert-3tjuxoukkq3vj0ww****&CAEnabled=true&CACertificateSource=PCARoot&CACertificateId=pca-********&SecurityPolicyType=system&SecurityPolicyId=tls_cipher_policy_1_0 HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyNLBListenerAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2024092952539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCACertificate.UnSupportAction |The specified CACertificate does not support this action, due to the content of the ca certificate is illegal. |The specified CA certificate is invalid and does not support the current operation. |
|400 |InvalidCACertificateId.CAEnabledMismatch |The specified CACertificateId not match with CAEnabled. |The specified CACertificateId does not match the CAEnabled setting of the listener. |
|400 |InvalidCACertificateSource.CACertificateIdMismatch |The specified CACertificateSource not match with CACertificateId. |The specified CACertificateSource does not match the specified CACertificateId. |
|400 |InvalidCACertificateSource.CAEnabledMismatch |The specified CACertificateSource not match with CAEnabled. |The specified CACertificateSource does not match the CAEnabled setting of the listener. |
|400 |InvalidCACertificateSource.Malformed |The specified CACertificateSource is malformed. |The specified CACertificateSource parameter format is invalid. |
|400 |InvalidCAEnabled.Malformed |The specified CAEnabled is malformed. |The specified CAEnabled parameter format is invalid. |
|400 |InvalidCAEnabled.ProtocolMismatch |The specified CAEnabled not match with Protocol. |The specified CAEnabled does not match the listener protocol type. |
|400 |InvalidCertificate.DomainTotalCount |The specified Certificate does not support this action, due to the total number of the certificate domain is illegal. |The operation is not supported for the specified certificate because the total number of domains exceeds the allowed limit. |
|400 |InvalidCertificate.DomainTotalLength |The specified Certificate does not support this action, due to the total length of the certificate domain is illegal. |The operation is not supported for the specified certificate because the total character length of all domain names exceeds allowed limits. |
|400 |InvalidCertificate.UnSupportAction |The specified Certificate does not support this action, due to the content of the certificate is illegal. |The specified certificate is invalid and does not support the current operation. |
|400 |InvalidCertificateId.ProtocolMismatch |The specified CertificateId not match with Protocol. |The specified CertificateId does not match the listener protocol type. |
|400 |InvalidCertificate.Conflict |The specified Certificate already in use. |The specified certificate is already in use by this listener. |
|400 |InvalidCertificateLength.Malformed |The specified CertificateLength is malformed. |The specified CertificateLength parameter format is invalid. |
|400 |InvalidCertificateSource.CertificateIdMismatch |The specified CertificateSource not match with CertificateId. |The specified CertificateSource does not match the specified CertificateId. |
|400 |InvalidCertificateSource.Malformed |The specified CertificateSource is malformed. |The specified CertificateSource parameter format is invalid. |
|400 |InvalidCertificateSource.PCACertificateIdMismatch |The specified CertificateSource not match with PCACertificateId. |The specified CertificateSource does not match the specified PCACertificateId. |
|400 |InvalidCertificateSource.ProtocolMismatch |The specified CertificateSource not match with Protocol. |The specified CertificateSource does not match the listener protocol type. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken parameter format is invalid. |
|400 |InvalidConnectionTimeout.Malformed |The specified ConnectionTimeout is malformed. |The specified ConnectionTimeout parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidEnabled.Malformed |The specified Enabled is malformed. |The specified Enabled parameter format is invalid. |
|400 |InvalidIPAddressVersion.TypeMismatch |The specified IPAddressVersion and Type are not matched. |The specified IP type is incompatible with the server group type. |
|400 |InvalidListener.InvalidStatus |The specified Listener is not in the correct status for the request. |The specified listener's status is incompatible with this request. |
|400 |InvalidListenerName.Malformed |The specified ListenerName is malformed. |The specified ListenerName parameter format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified CLB's state is incompatible with this request. |
|400 |InvalidLoadBalancerBillingStatus.InvalidStatus |The specified LoadBalancer is not in the correct billing status for the request. |The specified CLB's billing state is incompatible with this request. |
|400 |InvalidPCACertificateId.ProtocolMismatch |The specified PCACertificateId not match with Protocol. |The specified PCACertificateId does not match the listener protocol type. |
|400 |InvalidPrivateKey.Malformed |The specified PrivateKey is malformed. |The specified PrivateKey parameter format is invalid. |
|400 |InvalidPublicKey.Malformed |The specified PublicKey is malformed. |The specified PublicKey parameter format is invalid. |
|400 |InvalidPublicKey.PrivateKeyMisMatch |The PublicKey and PrivateKey are not matched. |The specified public key does not match the private key. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidSecurityPolicy.InvalidStatus |The specified SecurityPolicy is not in the correct status for the request. |The specified security policy is in a state that cannot respond to this request. |
|400 |InvalidSecurityPolicyId.ProtocolMismatch |The specified SecurityPolicyId not match with Protocol. |The specified SecurityPolicyId does not match the listener protocol type. |
|400 |InvalidSecurityPolicyType.Malformed |The specified SecurityPolicyType is malformed. |The specified SecurityPolicyType parameter format is invalid. |
|400 |InvalidSecurityPolicyType.ProtocolMismatch |The specified SecurityPolicyType not match with Protocol. |The specified SecurityPolicyType does not match the listener protocol type. |
|400 |InvalidSecurityPolicyType.SecurityPolicyIdMismatch |The specified SecurityPolicyType not match with SecurityPolicyId. |The specified SecurityPolicyType does not match the specified SecurityPolicyId. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidServerGroup.ListenerPortMismatch |The specified ServerGroup.AnyPortEnabled and Listener.Port are not matched. |The specified AnyPortEnabled attribute of the backend server group does not match the Port setting of the listener. |
|400 |InvalidServerGroup.ListenerProtocolMismatch |The specified ServerGroup.Protocol and Listener.Protocol are not matched. |The specified server group protocol does not match the listener protocol. |
|400 |InvalidServerGroup.LoadBalancerMismatch |The specified ServerGroup and LoadBalancer is mismatched. |The specified server group does not match the instance. |
|400 |InvalidServerGroup.LoadBalancerVpcMismatch |The specified ServerGroup's Vpc is not matched with LoadBalancer. |The specified VPC of the server group does not match the CLB instance. |
|400 |InvalidServerGroupProxyProtocolType.UnSupportAction |The specified ProxyProtocolType of ServerGroup does not support this action. |The specified backend server group does not support the current actions due to the Proxy\-Protocol constraints. |
|400 |InvalidServerGroupType.UnSupportAction |The specified Type of ServerGroup does not support this action. |The specified server group type does not support this action. |
|400 |InvalidSite.NotSupportBidirectionalAuthentication |The specified site does not support listener bidirectional authentication. |Mutual authentication for listeners is not enabled in the specified account environment. |
|400 |OperationFailed.QueryPcaService |The request for the specified resource operation failed due to an abnormal access issue with the pca service. |The operation request on the specified resource failed due to an access exception with the Certificate Center PCA service. |
|400 |QuotaExceed.ServerNumberEachInstance |You've reached the limit on the number of servers that you can mount on instance. |The quota limit for the number of backend servers that can be mounted on a single instance has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |No permission to perform this operation on the specified service. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidCACertificate.NotFound |The specified CACertificate does not exist. |The specified CA certificate does not exist. |
|404 |InvalidCertificate.NotFound |The specified Certificate does not exist. |The specified certificate does not exist. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified CLB does not exist. |
|404 |InvalidSecurityPolicy.NotFound |The specified SecurityPolicy does not exist. |The specified security policy does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|404 |ServiceRoleForLoadBalancer.NotFound |ServiceRoleForLoadBalancer does not exist. |The CLB service\-attached role does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource operation conflicts. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
