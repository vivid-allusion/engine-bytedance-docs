---
title: "ModifyListenerAttributes - Modifying the specified listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-ModifyListenerAttributes"
---

Call the ModifyListenerAttributes API to modify the specified listener.

## Instructions

* Submit up to 5 API requests per second.

* If the following optional parameters are not configured, the existing configurations will be preserved.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyListenerAttributes&groupName=%E7%9B%91%E5%90%AC%E5%99%A8&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: ModifyListenerAttributes`

Action to execute. Set the value to ModifyListenerAttributes.

**Version ** string必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**AccessLogRecordCustomizedHeadersEnabled** string `optional` `Example: on`

Whether to enable the "record custom headers in access logs" feature for this listener. Valid values:

* on: Enable.

* off: Disable.

**XRealIpEnabled ** string`optional` `Example: on`

The listener enables/disables the X\-real\-ip header. Valid values:

* on (default): Enable.

* off: Disable.

**ListenerName ** string`optional` `Example: test`

Listener name.

* Cannot start with http:// or https://.

* Must start with a letter or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Length must be between 1 and 128 characters.

**Enabled ** string`optional` `Example: on`

Enable/Disable the listener. Values:

* on: Enable.

* off: Disable.

**CertificateSource ** string`optional` `Example: cert_center`

The source of the default certificate. Valid values:

* alb: Indicates the certificate uploaded via ALB. [Standard edition ALB instance](https://docs.byteplus.com/en/docs/clb/Comparison-between-instance-editions) does not support this value.

* cert_center: Represents an SSL certificate purchased from or uploaded to the BytePlus Certificate Center.

> **tip**

> Each time you modify the default certificate, you must specify this parameter. Otherwise, the default value is alb, and the system will process it as an alb certificate.

**CACertificateId ** string`optional` `Example: cert-******`

ID of the CA certificate associated with the listener. When modifying the CA certificate of an HTTPS listener and the value of CACertificateSource is alb, this parameter must be specified.

**CertCenterCertificateId ** string`optional` `Example: cert-********`

Certificate ID from the Certificate Center.

When modifying the server certificate of an HTTPS listener and the certificate source is cert_center, this parameter must be specified.

**EnableHttp2 ** string`optional` `Example: off`

HTTP/2.0 feature switch. This parameter is only valid for HTTPS listeners. Valid values:

* on: Enable.

* off: Disable.

**EnableQuic ** string`optional` `Example: off`

QUIC feature switch. This parameter is only valid for HTTPS listeners. Valid values:

* on: Enable.

* off: Disable.

   Only standard edition ALB instances support QUIC. To use the QUIC feature, please contact your account manager.

**CustomizedCfgId ** string`optional` `Example: ccfg-*****`

Associate custom configuration.

* Only custom configurations with an Active status can be bound.

* When deleting a custom configuration, set this field to an empty string. If this parameter is not provided, no modification will be made.

**AclStatus ** string`optional` `Example: off`

Enable access control.

* Valid values:

   * on: Enable.

   * off: Do not enable.

* If left blank, no changes will be made to the access control configuration.

* Configuring this parameter will clear the already configured values in the AclType and AclIds parameters.

* If you change this parameter value from on to off, it will clear the values in the AclType and AclIds parameters.

* If you change this parameter value from off to on, you must simultaneously set values for the AclType and AclIds parameters.

**PcaLeafCertificateId ** string`optional` `Example: cert-********`

ID of the certificate bound to the listener.

When modifying the server certificate of an HTTPS listener and the certificate source is pca_leaf, this parameter must be specified.

**AclType ** string`optional` `Example: black`

Method of access control. Valid values:

* white: Allowlist mode. Indicates that the listener forwards requests only from the IP addresses or CIDR blocks set in the selected access control policy group. If no IPs are added to the selected policy group, the listener does not forward any requests.

* black: Denylist mode. Indicates that the listener denies requests only from the IP addresses or CIDR blocks set in the selected access control policy group. If no IPs are added to the selected policy group, the listener forwards all requests.

   When the AclStatus parameter is set to on, AclType and AclIds.N are required.

**CACertificateSource ** string`optional` `Example: pca_root`

Source of the CA certificate associated with the listener.

This parameter is only valid for HTTPS listeners and is used for mutual authentication.

When modifying the CA certificate, you must specify this parameter; otherwise, it defaults to alb. Valid values:

* alb: Indicates the certificate uploaded via ALB. Standard Edition ALB instances do not support certificates from this source.

* pca_root: Represents a private root CA certificate purchased from or uploaded to the BytePlus Certificate Center.

* pca_sub: Represents a private sub CA certificate purchased from or uploaded to the BytePlus Certificate Center.

**Description ** string`optional` `Example: test`

Description of the listener.

* Cannot start with http:// or https://.

* Must start with a letter or Chinese character and may include numbers, half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Must be 1 to 255 characters.

**DomainExtensions.N.DomainExtensionId ** string[]`optional` `Example: DomainExtensions.1.DomainExtensionId=dc-qwertasdf&DomainExtensions.2.DomainExtensionId=dc-poiuylkjhg`

Additional domain ID. Required only for deletion and modification operations.

* Parameter \- N: Indicates the serial number of the domain name.

* An HTTPS listener can associate with a maximum of 20 additional domains.

**PcaRootCACertificateId ** string`optional` `Example: cert-******`

ID of the CA certificate associated with the listener. When modifying the CA certificate of an HTTPS listener and the value of CACertificateSource is pca_root, this parameter must be specified.

**DomainExtensions.N.Domain ** string[]`optional` `Example: DomainExtensions.1.Domain=abc.com&DomainExtensions.2.Domain=def.com`

Domain name.

* Parameter \- N: Indicates the serial number of the domain name.

* An HTTPS listener can associate with a maximum of 20 additional domains

* Specific format requirements are as follows:

   * It generally cannot be empty. However, if the instance supports automatic extended certificate selection (i.e., `SniAutoMatch` is `on`), then `DomainExtensions.N.Domain` must be passed as an empty string.

   * Must contain at least one '.', and cannot start or end with '.'.

   * Only lowercase letters, numbers, '.', '\-', and '\*' are allowed.

   * Length must be between 1 and 128 characters.

   * Wildcard domain: Use "\*" to replace one or more characters.

      * The "\*" must be at the beginning or end of the domain name.

      * "\*" cannot appear twice in the same domain name.

      * No characters other than '.' are allowed before or after '\*'.

      * Valid examples:  *.com, www.test.* .

      * Invalid example: *aaa.com, www.* .com

   * Exact Domain Name​​: Must comply with domain name specifications (e.g., www.test.com).

   * Domain names under the same HTTPS listener cannot be duplicated.

   * Matching domain names is case\-insensitive.

**PcaSubCACertificateId ** string`optional` `Example: cert-******`

ID of the CA certificate associated with the listener. When modifying the CA certificate of an HTTPS listener and the value of CACertificateSource is pca_sub, this parameter must be specified.

**DomainExtensions.N.Action ** string[]`optional` `Example: DomainExtensions.1.Action=create&DomainExtensions.2.Action=modify`

The operation to perform on the specified additional domain.

* Parameter \- N: Represents the serial number of a domain. An HTTPS listener can associate with a maximum of 20 additional domains.

* Valid values:

   * create: Add.

   * modify: Modify.

   * delete: Delete.

**DomainExtensions.N.CertificateSource ** string[]`optional` `Example: DomainExtensions.1.CertificateSource=cert_center&DomainExtensions.2.CertificateSource=alb`

The server certificate source used by the domain name.

* Valid values:

   * alb: Indicates the certificate uploaded via ALB. [Standard edition ALB instance](https://docs.byteplus.com/en/docs/clb/Comparison-between-instance-editions) does not support this value.

   * cert_center: Represents an SSL certificate purchased from or uploaded to the BytePlus Certificate Center.

* Parameter \- N: Represents the serial number of a domain. An HTTPS listener can associate with a maximum of 20 additional domains, with values ranging from 1 to 20.

* Each time you modify the default certificate, you must specify this parameter. Otherwise, the default value is alb, and the system will process it as an alb certificate.

**DomainExtensions.N.CertCenterCertificateId ** string[]`optional` `Example: DomainExtensions.1.CertCenterCertificateId=cert-qwertyuqwert&DomainExtensions.2.CertCenterCertificateId=cert-zxcvbgasdfn`

The server certificate used by the domain.

* When modifying an extended certificate and the certificate source is cert_center, this parameter must be specified.

* Parameter \- N: Represents the serial number of a domain. An HTTPS listener can associate with a maximum of 20 additional domains, with values ranging from 1 to 20.

**ListenerId ** string必选 `Example: lsn-abc*******`

ID of the listener to be modified.

**ServerGroupId ** string`optional` `Example: rsp-******`

The default server group ID associated with the listener.

**AclIds.N ** string[]`optional` `Example: AclIds.1=acl-3cj44nv0jhhxc6c6rrtet****& AclIds.2=acl-2febxt4pu0zy85oxruw0t****`

The ID of the ACL bound to the listener.

* Parameter \- N: Indicates the serial number of the access control list, with a maximum of 5.

* Separate multiple access control list IDs with ampersands ( & ).

* When the AclStatus parameter is set to on, AclType and AclIds.N are required.

**DomainExtensions.N.CertificateId ** string[]`optional` `Example: DomainExtensions.1.CertificateId=cert-qwertyuqwert&DomainExtensions.2.CertificateId=cert-zxcvbgasdfn`

The server certificate used by the domain name.

* When modifying an extended certificate and the certificate source is alb, this parameter must be specified.

* Parameter \- N: Represents the serial number of a domain. An HTTPS listener can associate with a maximum of 20 additional domains.

**CertificateId ** string`optional` `Example: cert-******`

The certificate ID managed by ALB\-side certificate management.

When modifying the server certificate of an HTTPS listener and the certificate source is alb, this parameter must be specified.

**DomainExtensions.N.PcaLeafCertificateId ** string[]`optional` `Example: DomainExtensions.1.PcaLeafCertificateId=pca_leaf-qwertyuqwert&DomainExtensions.2.PcaLeafCertificateId=pca_leaf-zxcvbgasdfn`

The server certificate used by the domain name.

* Effective when the certificate source is pca_leaf.

* Parameter \- N: Represents the serial number of a domain. An HTTPS listener can associate with a maximum of 20 additional domains, with values ranging from 1 to 20.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 20210811152539010225146063030****`

Request ID.

## Request example

```text
GET /?Action=ModifyListenerAttributes&ListenerId=lsn-2fek3rgsxhrsw5oxruwec****&Version=2020-04-01&ListenerName=test&Enabled=off HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "ModifyListenerAttributes",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202108161106****22514606306AF947C"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |OperationDenied.AccountArrears |The request on the specified resource is denied due to the account being in arrears status. |The request to operate on this resource was rejected because the account is in an overdue payment state. |
|400 |InvalidListenerName.Malformed |The specified ListenerName is malformed. |The specified ListenerName format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidAclStatus.Malformed |The specified AclStatus is malformed. |The specified AclStatus parameter format is invalid. |
|400 |InvalidDomainExtensions.Action.Malformed |The specified DomainExtensions.Action is malformed. |The specified DomainExtensions.Action parameter format is invalid. |
|400 |InvalidDomainExtensions.DomainExtensionId.Duplicated |The specified DomainExtensions.DomainExtensionId is duplicated. Only one type domain extension action is supported on one domain extension in one request. |The specified DomainExtensions.DomainExtensionId is duplicated. Only one type of operation is supported for the additional domains specified in a single request. |
|400 |InvalidDomainExtensions.Certificate.InvalidStatus |The specified DomainExtension Certificate is not in the correct status for the request. |The specified additional domain certificate is in a status that cannot respond to this request. |
|400 |InvalidDomainExtensions.Domain.Duplicated |The specified DomainExtensions.Domain is duplicated. Domain Extensions in one listener can not be same. |The specified DomainExtensions.Domain is duplicated. Additional domains associated with one listener cannot be duplicated. |
|400 |InvalidDomainExtensions.Domain.Malformed |The specified DomainExtensions.Domain is malformed. |The specified DomainExtensions.Domain parameter format is invalid. |
|400 |InvalidIndexOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |OperationDenied.DualStackEnableQuicUnsupported |The request on the specified Listener is denied due to the dual stack load balancer listener not support to enable quic. |The request to operate on this listener was rejected because dual\-stack ALB instances currently do not support enabling QUIC on listeners. |
|400 |InvalidEnableHttp2.Malformed |The specified EnableHttp2 is malformed. |The specified EnableHttp2 parameter format is invalid. |
|400 |InvalidCACertificate.InvalidStatus |The specified CA Certificate is not in the correct status for the request. |The specified CA certificate is in a state that cannot respond to this request. |
|400 |InvalidServerCertificate.InvalidStatus |The specified Server Certificate is not in the correct status for the request. |The specified server certificate is in a status that cannot respond to this request. |
|400 |InvalidCertificateType.FunctionMismatch |The specified Certificate's type and Function do not match. |The type of the specified certificate does not match the expected functionality. |
|400 |InvalidVpcForServerGroup.LoadBalancerMismatch |The specified VPC of ServerGroup and LoadBalancer do not match. |The specified server group and the ALB instance do not belong to the same VPC. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidEnableQuic.Malformed |The specified EnableQuic is malformed. |The specified EnableQuic parameter format is invalid. |
|400 |QuotaExceed.RulePerGroup |You've reached the limit on the number of rules per server group you can associate with, resource xxx, usage xx/xx. |The maximum number of forwarding rules that can be associated with a single server group has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |QuotaExceed.ListenerPerAcl |You've reached the limit on the number of listeners per ACL you can associate with, resource xxx, usage xx/xx. |The maximum number of listeners that can be associated with a single ACL has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |QuotaExceed.AclPerListener |You've reached the limit on the number of ACLs per listener you can associate with, resource xxx, usage xx/xx. |The maximum number of ACLs that can be associated with a single listener has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |QuotaExceed.ListenerPerCustomizedCfg |You've reached the limit on the number of listeners per CustomizedCfg you can associate with, resource xxx, usage xx/xx. |The maximum number of listeners that can be associated with a single custom configuration has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |QuotaExceed.SniDomainPerListener |You've reached the limit on the number of sni domains per listener you can associate with, resource xxx, usage xx/xx. |The maximum number of SNI domains that can be associated with a single listener has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |QuotaExceed.ServerPerInstance |You've reached the limit on the number of backend servers per ALB you can associate with, resource xxx, usage xx/xx. |The maximum number of backend servers that can be associated with a single instance has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |OperationFailed.OperateGtmFailed |The request on the specified resource failed due to operating gtm failed. |The request to operate on this resource failed because the operation on the GTM instance failed. |
|400 |InvalidEnabled.Malformed |The specified Enabled is malformed. |The specified Enabled format is invalid. |
|400 |InvalidCustomizedCfg.InvalidStatus |The specified CustomizedCfg is not in the correct status for the request. |The specified custom configuration is in a state that cannot respond to the request. |
|400 |InvalidAclId.Duplicated |The specified AclId is duplicated. |The specified AclId is duplicated. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'AclIds'. |This request does not contain the required parameter. Please ensure the request includes all required parameters, such as: AclIds. |
|400 |InvalidAclType.Malformed |The specified AclType is malformed. |The specified AclType parameter format is invalid. |
|400 |OperationFailed.QueryCertificateService |The request on the specified resource failed due to the query on Certificate Service failed. |The request to operate on this resource failed because the request to the Certificate Center service failed. |
|400 |LimitExceed.DomainExtension |You've reached the limit on the number of domain extensions that you can operate at a time. |The maximum number of additional domains that can be processed in a single operation has been reached. |
|400 |InvalidDomainExtensions.CertificateSource.Malformed |The specified DomainExtensions.CertificateSource is malformed. |The specified DomainExtensions.CertificateSource parameter format is invalid. |
|400 |OperationFailed.QueryIAM |The request on the specified resource failed due to the query on IAM failed. |The request to operate on this resource failed because the IAM request failed. |
|400 |InvalidCertificateServiceSSLCertificate.InvalidStatus |The specified Certificate Service SSL Certificate is not in the correct status for the request. Please check if the certificate has been issued. |The specified Certificate Center SSL certificate is in a status that cannot respond to this request. Confirm the certificate has been issued. |
|400 |InvalidCertificateSource.Malformed |The specified CertificateSource is malformed. |The format of the specified CertificateSource is invalid. |
|400 |InvalidProxyProtocolDisabled.Malformed |The specified ProxyProtocolDisabled is malformed. |The specified ProxyProtocolDisabled parameter format is invalid. |
|400 |InvalidCertificateId.Duplicated |The specified CertificateId is duplicated. Certificates in one listener can not be same. |The specified CertificateId is duplicated. Certificates under a single listener cannot be duplicated. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|400 |InvalidALRCHEnabled.Malformed |The specified AccessLogRecordCustomizedHeadersEnabled is malformed |The specified AccessLogRecordCustomizedHeadersEnabled parameter format is invalid. |
|400 |InvalidXRealIpEnabled.Malformed |The specified XRealIpEnabled is malformed. |The specified XRealIpEnabled parameter format is invalid. |
|400 |QuotaExceed.AclEntriesPerInstance |You've reached the limit on the number of ACL entries per instance you can associate with, resource xxx, usage xx/xx. |The maximum number of ACL entries that can be associated with a single instance has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |OperationDenied.AclAndSecurityGroupConflict |The request on the specified LoadBalancer is denied due to acls and security groups cannot be used at the same time. |The operation request for this ALB instance is rejected because access control and security groups cannot be used simultaneously. |
|400 |QuotaExceed.ListenerPerCert |You've reached the limit on the number of listeners per server certificate you can associate with, resource xxx, usage xx/xx. |The maximum number of listeners that can be associated with a single server certificate has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |QuotaExceed.ListenerPerCACert |You've reached the limit on the number of listeners per CA certificate you can associate with, resource xxx, usage xx/xx. |The maximum number of listeners that can be associated with a single CA certificate has been reached. The resource is xxx. Used: xx. Quota: xx. |
|400 |InvalidCertificate.InvalidStatus |The specified Certificate is not in the correct status for the request. |The specified certificate is in a status that cannot respond to this request. |
|403 |Forbidden |You are not authorized to disable X\-real\-ip header. |You do not have permission to disable the X\-real\-ip header. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified ALB instance does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|404 |InvalidServerCertificate.NotFound |The specified Server Certificate does not exist. |The specified server certificate does not exist. |
|404 |InvalidCACertificate.NotFound |The specified CA Certificate does not exist. |The specified CA certificate does not exist. |
|404 |InvalidDomainExtensions.Certificate.NotFound |The specified DomainExtension Certificate does not exist. |The specified additional domain certificate does not exist. |
|404 |InvalidDomainExtension.NotFound |The specified Domain Extension does not exist. |The specified additional domain does not exist. |
|404 |InvalidAcl.NotFound |The specified ACL does not exist. |The specified ACL does not exist. |
|404 |InvalidCustomizedCfg.NotFound |The specified CustomizedCfg does not exist. |The specified custom configuration does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
