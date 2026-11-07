---
title: "CreateNLBListener - Adding a listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CreateNLBListener"
---

Call the CreateNLBListener API to add a listener for a Network Load Balancer (NLB) instance.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateNLBListener&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: CreateNLBListener`

Action to execute. Set the value to CreateNLBListener.

**Version ** String必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**LoadBalancerId ** String必选 `Example: nlb-bp1o94dp5i6ea****`

The ID of the NLB instance.

You can call the [DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) API to get the NLB instance ID.

**ListenerName ** String`optional` `Example: test`

Listener name.

* Must start with a letter or Chinese character and may contain numbers, periods (.), underscores (_), and hyphens (\-).

* Length limit: 1 to 128 characters.

* If this parameter is not passed in, the default value will be "protocol\-port", For example, TCP\-80.

**Protocol ** String必选 `Example: TCP`

Listener protocol. Valid values:

* TCP

* UDP

* TLS

> **tip**

* > Dual\-stack NLB instances do not currently support TLS.

* > The TLS listener is in the invite\-only Beta stage. For trial requests, please contact the account manager.

**Port ** Integer必选 `Example: 80`

The port used by the listener to receive requests.

* The value range for a single port: 1 to 65535.

* 0 indicates enabling listening on all ports, port range listening.

> **tip**

* > TLS protocol listeners do not support enabling full port listening.

* > Within the same NLB instance, TLS and TCP listeners cannot share the same port; however, both can coexist on the same port as a UDP listener.

**StartPort ** Integer`optional` `Example: 1`

The start port for full port listening. Value range: 1\-65535.

> **tip**

> The parameter `Port` is required when it is "0".

**EndPort ** Integer`optional` `Example: 65535`

End port for full port listening. Value range: 1\-65535.

> **tip**

> When the parameter `Port` is "0", this parameter is required, and its value must be greater than `StartPort`.

**Enabled ** Boolean`optional` `Example: true`

Enable the listener. Valid values:

* true (default): Enable.

* false: Disable.

**CertificateSource ** String`optional` `Example: SSL`

The source of the server certificate for the TLS listener. Valid values:

* SSL (default): Certificate Center \- SSL certificate.

* PCALeaf: Certificate Center \- Private certificate of the private CA.

**CertificateId ** String`optional` `Example: cert-3tjuxoukkq3vj0ww****`

For the server certificate ID of a TLS listener, only private certificates issued by SSL certificates in BytePlus Certificate Center are supported.

> The SM certificate is currently in invite\-only beta. For trial requests, please contact your account manager.

**PCACertificateId ** String`optional` `Example: cert-3tjuxoukkq3vj0ww****`

The server certificate ID for the TLS listener. Only private certificates from the BytePlus Certificate Center Private CA are supported.

> Description:

> SM certificate and private CA of the Certificate Center are in beta stage. For trial requests, please contact your account manager.

**CAEnabled ** Boolean`optional` `Example: true`

Enable mutual authentication for the TLS listener. Valid values:

* true: Enable mutual authentication.

* false (default): Disable mutual authentication.

> This feature is currently in the invite\-only Beta stage. For a trial, contact your account manager.

**CACertificateSource ** String`optional` `Example: PCARoot`

The source of the CA certificate for the TLS listener. Valid values:

* PCARoot: Private CA's private root CA certificate.

* PCASub: Private sub\-CA certificate of private CA.

> Description:

> * When CAEnabled is set to true, this parameter is required.

**CACertificateId ** String`optional` `Example: pca-********`

For CA certificates associated with TLS listeners, BytePlus Certificate Center supports uploading certificates from both private root CA and private subordinate CA certificate modules.

> When CAEnabled is set to true, this parameter is required.

> * Certificate validity status: Enabled, Not Expired, and Not Revoked.

> * SM certificate is in the invite\-only Beta stage. For trial requests, please contact your account manager.

**SecurityPolicyType ** String`optional` `Example: system`

TLS security policy type. Valid values:

* custom: Custom policy.

* system (default): System policy.

**SecurityPolicyId ** String`optional` `Example: tls_cipher_policy_1_0`

TLS security policy ID, supporting both system security policies and custom security policies.

* System security policy values:

   * tls_cipher_policy_1_0

   * tls_cipher_policy_1_1

   * tls_cipher_policy_1_2

   * tls_cipher_policy_1_2_strict

   * tls_cipher_policy_1_2_strict_with_1_3

* Custom security policy: Enter the custom security policy ID.

When protocol is TLS, this parameter is required.

**ConnectionTimeout ** Integer`optional` `Example: 800`

The connection timeout period of the listener.

* When the parameter Protocol is "TCP" or "TLS", the value range is 10 to 900 seconds, with a default of 900 seconds.

* When the parameter Protocol is "UDP", the value range is 10 to 120 seconds, with a default of 20 seconds.

**ServerGroupId ** String必选 `Example: rsp-bp1o94dp5i6ea****`

The server group ID associated with the listener.

You can call the [DescribeNLBServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups) API to get the server group ID.

* When the protocol is set to TCP, the backend servers must also use TCP.

* When the protocol is set to UDP, the backend servers must also use UDP.

* When the protocol is set to TLS, the backend servers must also use TCP. And does not support selecting the following server groups:

   * Does not support attaching server groups with IP address type.

   * Server groups that do not support enabling the Proxy\-Protocol protocol.

**Description ** String`optional` `Example: This is a listener.`

Description of the listener.

* Must start with a letter or a Chinese character. It may contain numbers, half\-width commas ( , ), half\-width periods ( . ), underscores ( _ ), spaces ( ), equal signs ( = ), hyphens ( \- ), full\-width commas (， ), and full\-width periods ( 。 ).

* Length limit: 1 to 255 characters.

* If the parameter is not passed in, it defaults to an empty string.

**Tags.N.Key ** String`optional` `Example: key1`

The tag key of the custom tag.

* N represents the serial number of a tag key. Valid range: 1 to 20.

* Separate multiple tag keys with ampersands (&).

* It cannot start with `volc:` or `sys:` in any case form.

* It can be 1 to 128 characters in length. It may contain characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example: value1`

The tag value of the custom tag.

* N specifies the serial number of the tag value. Valid values: 1–20.

* Separate multiple tag values with ampersands (&).

* The value can be 0 to 256 characters in length. If left blank, the parameter defaults to an empty value.

* May include multilingual characters, digits, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete it.

> **tip**

> To provide this parameter, provide Tags.N.Key first.

**Cps ** Integer`optional` `Example: 0`

New connection rate limit.

* Value range: 0~1000000.

* Defaults to 0; 0 means no rate limiting.

* When new connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.

> **tip**

> The new connections rate limiting feature is currently in invite\-only beta. Contact your account manager to try it.

**MaxConnections ** Integer`optional` `Example: 0`

Max connection rate limiting.

* Value range: 0~10000000.

* Defaults to 0; 0 means no rate limiting.

* When max connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.

> **tip**

> The max connections rate limiting feature is currently in Invite\-only Beta. To request a trial, contact your account manager.

## Response parameters

**RequestId ** String`Example: 2024092952539010225146063030****`

Request ID.

**ListenerId ** String`Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.

## Request example

```json
GET /?Action=CreateNLBListener&Version=2020-04-01&LoadBalancerId=nlb-bp1o94dp5i6ea****&Protocol=TCP&Port=80&ServerGroupId=rsp-bp1o94dp5i6ea**** HTTP/1.1 
Host: clb.cn-beijing.byteplusapi.com.cn 
Date: 20260310T094038Z 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateNLBListener",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "ListenerId": "lsn-2fek3rgsxhrsw5oxruwec****",
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
|400 |InvalidCACertificate.UnSupportAction |The specified CACertificate does not support this action, due to the content of the ca certificate is illegal. |The specified CA certificate is invalid and does not support the current operation. |
|400 |InvalidCACertificateId.CAEnabledMismatch |The specified CACertificateId not match with CAEnabled. |The specified CACertificateId does not match the CAEnabled setting of the listener. |
|400 |InvalidCACertificateSource.CAEnabledMismatch |The specified CACertificateSource not match with CAEnabled. |The specified CACertificateSource does not match the CAEnabled setting of the listener. |
|400 |InvalidCACertificateSource.Malformed |The specified CACertificateSource is malformed. |The specified CACertificateSource parameter format is invalid. |
|400 |InvalidCAEnabled.Malformed |The specified CAEnabled is malformed. |The specified CAEnabled parameter format is invalid. |
|400 |InvalidCAEnabled.ProtocolMismatch |The specified CAEnabled not match with Protocol. |The specified CAEnabled does not match the listener protocol type. |
|400 |InvalidCertificate.DomainTotalCount |The specified Certificate does not support this action, due to the total number of the certificate domain is illegal. |The operation is not supported for the specified certificate because the total number of domains exceeds the allowed limit. |
|400 |InvalidCertificate.DomainTotalLength |The specified Certificate does not support this action, due to the total length of the certificate domain is illegal. |The operation is not supported for the specified certificate because the total character length of all domain names exceeds allowed limits. |
|400 |InvalidCertificate.UnSupportAction |The specified Certificate does not support this action, due to the content of the certificate is illegal. |The specified certificate is invalid and does not support the current operation. |
|400 |InvalidCertificateId.ProtocolMismatch |The specified CertificateId not match with Protocol. |The specified CertificateId does not match the listener protocol type. |
|400 |InvalidCertificateLength.Malformed |The specified CertificateLength is malformed. |The specified CertificateLength parameter format is invalid. |
|400 |InvalidCertificateSource.CertificateIdMismatch |The specified CertificateSource not match with CertificateId. |The specified CertificateSource does not match the specified CertificateId. |
|400 |InvalidCertificateSource.Malformed |The specified CertificateSource is malformed. |The format of the specified CertificateSource parameter is invalid. |
|400 |InvalidCertificateSource.PCACertificateIdMismatch |The specified CertificateSource not match with PCACertificateId. |The specified CertificateSource does not match the specified PCACertificateId. |
|400 |InvalidCertificateSource.ProtocolMismatch |The specified CertificateSource not match with Protocol. |The specified CertificateSource does not match the listener protocol type. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidConnectionTimeout.Malformed |The specified ConnectionTimeout is malformed. |The specified ConnectionTimeout parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidEnabled.Malformed |The specified Enabled is malformed. |The specified Enabled parameter format is invalid. |
|400 |InvalidEndPort.Malformed |The specified EndPort is malformed. |The format of the specified EndPort parameter is invalid. |
|400 |InvalidIPAddressVersion.TypeMismatch |The specified IPAddressVersion and Type are not matched. |The specified IP type is incompatible with the server group type. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidListenerName.Malformed |The specified ListenerName is malformed. |The specified ListenerName parameter format is invalid. |
|400 |InvalidListenerPort.ProtocolMismatch |The specified Listener Port not match with Protocol. |The specified port does not match the listener protocol type. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified CLB's state is incompatible with this request. |
|400 |InvalidLoadBalancerBillingStatus.InvalidStatus |The specified LoadBalancer is not in the correct billing status for the request. |The specified CLB's billing state is incompatible with this request. |
|400 |InvalidLoadBalancerIPAddressVersion.UnSupportAction |The specified IPAddressVersion of LoadBalancer does not support this action. |The specified instance does not support the current action due to its IP address type constraint. |
|400 |InvalidPCACertificateId.ProtocolMismatch |The specified PCACertificateId not match with Protocol. |The specified PCACertificateId does not match the listener protocol type. |
|400 |InvalidPort.Malformed |The specified Port is malformed. |The specified Port format is invalid. |
|400 |InvalidPrivateKey.Malformed |The specified PrivateKey is malformed. |The specified PrivateKey format is invalid. |
|400 |InvalidProject.Malformed |The specified Project is malformed. |The specified Project parameter format is invalid. |
|400 |InvalidProtocol.Malformed |The specified Protocol is malformed. |The specified Protocol parameter format is invalid. |
|400 |InvalidPublicKey.Malformed |The specified PublicKey is malformed. |The specified PublicKey parameter format is invalid. |
|400 |InvalidPublicKey.PrivateKeyMisMatch |The PublicKey and PrivateKey are not matched. |The specified public key does not match the private key. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidSecurityPolicy.InvalidStatus |The specified SecurityPolicy is not in the correct status for the request. |The specified security policy's state is incompatible with the request. |
|400 |InvalidSecurityPolicyId.ProtocolMismatch |The specified SecurityPolicyId not match with Protocol. |The specified SecurityPolicyId does not match the listener protocol type. |
|400 |InvalidSecurityPolicyType.Malformed |The specified SecurityPolicyType is malformed. |The specified SecurityPolicyType parameter format is invalid. |
|400 |InvalidSecurityPolicyType.ProtocolMismatch |The specified SecurityPolicyType not match with Protocol. |The specified SecurityPolicyType does not match the listener protocol type. |
|400 |InvalidSecurityPolicyType.SecurityPolicyIdMismatch |The specified SecurityPolicyType not match with SecurityPolicyId. |The specified SecurityPolicyType does not match the specified SecurityPolicyId. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidServerGroup.ListenerPortMismatch |The specified ServerGroup.AnyPortEnabled and Listener.Port are not matched. |The specified AnyPortEnabled attribute of the backend server group does not match the Port setting of the listener. |
|400 |InvalidServerGroup.ListenerProtocolMismatch |The specified ServerGroup.Protocol and Listener.Protocol are not matched. |The protocol of the specified server group does not match the listener protocol. |
|400 |InvalidServerGroup.LoadBalancerMismatch |The specified ServerGroup and LoadBalancer is mismatched. |The specified server group does not match the instance. |
|400 |InvalidServerGroup.LoadBalancerVpcMismatch |The specified ServerGroup's Vpc is not matched with LoadBalancer. |The specified VPC of the server group does not match the CLB instance. |
|400 |InvalidServerGroupProxyProtocolType.UnSupportAction |The specified ProxyProtocolType of ServerGroup does not support this action. |The specified backend server group does not support the current actions due to the Proxy\-Protocol constraints. |
|400 |InvalidServerGroupType.UnSupportAction |The specified Type of ServerGroup does not support this action. |The specified Server Group type does not support the current action. |
|400 |InvalidSite.NotSupportBidirectionalAuthentication |The specified site does not support listener bidirectional authentication. |Mutual authentication for listeners is not enabled in the specified account environment. |
|400 |InvalidStartOrEndPort.Malformed |The specified StartOrEndPort is malformed. |The specified StartOrEndPort parameter format is invalid. |
|400 |InvalidStartPort.Malformed |The specified StartPort is malformed. |The specified StartPort parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.ServiceManagedTag |You've reached the limit on the number of service managed tags that you can create. |You have reached the limit for the number of managed resource tag key\-value pairs that can be created in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |OperationFailed.QueryPcaService |The request for the specified resource operation failed due to an abnormal access issue with the pca service. |The operation request on the specified resource failed due to an access exception with the Certificate Center PCA service. |
|400 |QuotaExceed.ListenerNumberEachInstance |You've reached the limit on the number of listeners that you can create. |The quota limit for the number of listeners that can be created for a single instance has been reached. |
|400 |QuotaExceed.ListenerNumberEachServerGroup |You've reached the limit on the number of listeners that you can associate. |The quota limit for the number of listeners that can be associated with a single server group has been reached. |
|400 |QuotaExceed.PortRangeListenerNumberEachInstance |You've reached the limit on the number of portRange listeners that you can create. |The quota limit for the number of full\-port listeners that can be created for a single instance has been reached. |
|400 |QuotaExceed.ServerNumberEachInstance |You've reached the limit on the number of servers that you can mount on instance. |The quota limit for the number of backend servers that can be mounted on a single instance has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |No permission to perform actions on the specified service. |
|403 |Forbidden |You are not authorized to perform operations on the service managed tag. |No permission to tag the specified resource with managed tags. |
|403 |Forbidden |You are not authorized to perform operations on the system tag. |No permission to tag the specified resource with a system tag. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidCACertificate.NotFound |The specified CACertificate does not exist. |The specified CA certificate does not exist. |
|404 |InvalidCertificate.NotFound |The specified Certificate does not exist. |The specified certificate does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified CLB does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidSecurityPolicy.NotFound |The specified SecurityPolicy does not exist. |The specified security policy does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|404 |ServiceRoleForLoadBalancer.NotFound |ServiceRoleForLoadBalancer does not exist. |The CLB service\-attached role does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource operation conflicts. |
|409 |InvalidPort.Conflict |The specified Port already exists. |The specified port already exists. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
