---
title: "API release notes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/API-release-notes"
---

This topic introduces the OpenAPI updates of Classic Load Balancer (CLB).

<span id="4kGBJFhD"></span>
## September 2026


|API |**Release note** |**Associated features** |
|---|---|---|
|[CreateListener](https://docs.byteplus.com/en/docs/clb/CreateListener) |Added values to request parameter SecurityPolicyId: tls_cipher_policy_1_3, tls_cipher_policy_1_2_strict_with_1_3. |Listener |


<span id="8fzbugzP"></span>
## September 2025


|API |**Release note** |**Associated features** |
|---|---|---|
|[ConvertLoadBalancerBillingType](https://docs.byteplus.com/en/docs/clb/ConvertLoadBalancerBillingType) |New request parameter: AutoRenewal. |CLB instance<br><br> |
|[DeleteLoadBalancer](https://docs.byteplus.com/en/docs/clb/DeleteLoadBalancer) |New error code: Forbidden.<br><br> ||
|[DescribeLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancerAttributes) |||
|[RenewLoadBalancer](https://docs.byteplus.com/en/docs/clb/RenewLoadBalancer) |||


<span id="l8GcyTu6"></span>
## July 2025


|API |**Release note** |**Associated features** |
|---|---|---|
|[DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) |* New request parameters: InstanceIds.N, InstanceIps.N.<br><br>* New error codes: InvalidInstanceIp.Malformed, LimitExceeded.ServerInstanceIdNumber, LimitExceeded.ServerInstanceIpNumber, InvalidPageNumber.Malformed, InvalidPageSize.Malformed. |CLB instance<br><br> |
|[CreateLoadBalancer](https://docs.byteplus.com/en/docs/clb/CreateLoadBalancer) |New error codes: InvalidEipBillingConfig.Bandwidth.Malformed, InvalidEipBillingConfig.EipBillingType.Malformed, InvalidEipBillingConfig.SecurityProtectionInstanceId.Malformed. ||
|[DeleteLoadBalancer](https://docs.byteplus.com/en/docs/clb/DeleteLoadBalancer) |New error code: InvalidForceDelete.Malformed. ||
|[DescribeLoadBalancersBilling](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancersBilling) |||
|[DescribeAcls](https://docs.byteplus.com/en/docs/clb/DescribeAcls) ||Access Control List |
|[DescribeCertificates](https://docs.byteplus.com/en/docs/clb/DescribeCertificates) |||
|[DescribeListenerHealth](https://docs.byteplus.com/en/docs/clb/DescribeListenerHealth) |New error codes: InvalidPageNumber.Malformed, InvalidPageSize.Malformed. |Listener |
|[CreateRules](https://docs.byteplus.com/en/docs/clb/CreateRules) |New error codes: InvalidListener.NotSupportRule, |Forwarding rules |
|[DescribeServerGroupsDescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) |New error codes: InvalidPageNumber.Malformed, InvalidPageSize.Malformed. New error codes: InvalidPageNumber.Malformed, InvalidPageSize.Malformed. |Backend server group |
|[ModifyServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/ModifyServerGroupAttributes) |New error code: InvalidServers.Port.Malformed. ||
|[ListTagsForResources](https://docs.byteplus.com/en/docs/clb/ListTagsForResources) |New error code: InvalidMaxResults.Malformed. |Tag |


<span id=".MjAyNOW5tDEx5pyI"></span>
## March 2025


|API |**Release note** |**Associated features** |
|---|---|---|
|[CreateLoadBalancer](https://docs.byteplus.com/en/docs/clb/CreateLoadBalancer) |New error code: Forbidden. |CLB instance |
|[DescribeLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancerAttributes) |New response parameters: TlsEnabled, TlsProjectId, TlsTopicId. ||
|[TagResources](https://docs.byteplus.com/en/docs/clb/TagResources) |Modify request parameters: Adjusted the value range of N in Tags.N.Key and Tags.N.Value. |Tag |
|[UntagResources](https://docs.byteplus.com/en/docs/clb/UntagResources) |||
|[DisableAccessLog](https://docs.byteplus.com/en/docs/clb/DisableAccessLog) |New request parameter: DeliveryType. |Access log<br><br> |
|[EnableAccessLog](https://docs.byteplus.com/en/docs/clb/EnableAccessLog)<br><br> |* Modify request parameter: BucketName changed from required to optional.<br><br>* New request parameters: DeliveryType, TlsProjectId, TlsTopicId.<br><br>* New error codes: InvalidDeliveryType.Malformed, InvalidTlsProjectId.UsedInHealthCheckLog, InvalidTlsProjectId.UsedInOtherService, InvalidTlsTopicId.TlsProjectIdMismatch, InvalidTlsTopicId.UsedInOtherService, MissingParameter, Forbidden. ||


<span id=".MjAyNOW5tDEx5pyI"></span>
## February 2025


|API |Release note |Associated features |
|---|---|---|
|[CreateLoadBalancer](https://docs.byteplus.com/en/docs/clb/CreateLoadBalancer) |* New request parameter: TimestampRemoveEnabled.<br><br>* New error codes: InvalidTimestampRemoveEnabled.Malformed, Forbidden |CLB instance |
|[ModifyLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerAttributes) |||
|[DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) |New return data: TimestampRemoveEnabled. ||
|[DescribeLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancerAttributes) |||


<span id=".MjAyNOW5tDEx5pyI"></span>
## January 2025


|API |Release note |Associated features |
|---|---|---|
|[DeleteLoadBalancer](https://docs.byteplus.com/en/docs/clb/DeleteLoadBalancer) |New request parameter: ForceDelete. |CLB instance |
|[CreateLoadBalancer](https://docs.byteplus.com/en/docs/clb/CreateLoadBalancer) |New error code: Forbidden. ||
|[UploadCertificate](https://docs.byteplus.com/en/docs/clb/UploadCertificate) ||Certificate |
|[CreateAcl](https://docs.byteplus.com/en/docs/clb/CreateAcl) ||Access Control List |
|[CreateServerGroup](https://docs.byteplus.com/en/docs/clb/CreateServerGroup) ||Server group |
|[CreateListener](https://docs.byteplus.com/en/docs/clb/CreateListener)<br><br>[ModifyListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyListenerAttributes) |* New request parameters: CACertificateId, CAEnabled.<br><br>* New new error codes: InvalidCACertificate.UnSupportAction, InvalidCAEnabled.CACertificateIdMismatch, InvalidCAEnabled.Malformed, InvalidCAEnabled.ProtocolMismatch, InvalidSite.NotSupportBidirectionalAuthentication, OperationFailed.QueryPcaService, Forbidden, InvalidCACertificate.NotFound. |Listener |
|[DescribeListenerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeListenerAttributes) |New response parameters: CACertificateId, CAEnabled, WafProtectionEnabled. ||
|[DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) |||
|[CreateRules](https://docs.byteplus.com/en/docs/clb/CreateRules) |* New request parameters: Rules.N.Tags.N.Key, Rules.N.Tags.N.Value.<br><br>* New error codes: InvalidTagKey.Malformed, InvalidTagValue.Malformed, LimitExceeded.ServiceManagedTag, LimitExceeded.TagOperation, Forbidden. |Forwarding rules |
|[DescribeRules](https://docs.byteplus.com/en/docs/clb/DescribeRules) |* New request parameters: TagFilters.N.Key, TagFilters.N.Values.N.<br><br>* New response parameter: Tags structure. ||
|[ListTagsForResources](https://docs.byteplus.com/en/docs/clb/ListTagsForResources) |Modify request parameter: Added value field rule to ResourceType. |Tag |
|[UntagResources](https://docs.byteplus.com/en/docs/clb/UntagResources) |||
|[TagResources](https://docs.byteplus.com/en/docs/clb/TagResources) |* Modify request parameter: Added value fields rule and ec to ResourceType.<br><br>* New error codes: InvalidDefaultRule.UnSupportAction, Forbidden. ||


<span id=".MjAyNOW5tDEx5pyI"></span>
## November 2024


|API |Release note |Associated features |
|---|---|---|
|[CreateListener](https://docs.byteplus.com/en/docs/clb/CreateListener)<br><br>[ModifyListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyListenerAttributes) |* New optional request parameters `CertCenterCertificateId` and `CertificateSource`.<br><br>* New error codes: `InvalidCertificate.UnSupportAction`, `InvalidCertificateLength.Malformed`, `InvalidCertificateSource.CertCenterCertificateIdMismatch`, `InvalidCertificateSource.CertificateIdMismatch`, `InvalidCertificateSource.Malformed`, InvalidPrivateKey.Malformed, `InvalidPublicKey.Malformed`, InvalidPublicKey.PrivateKeyMisMatch, `InvalidResponseCheckEnabled.ProtocolMismatch`, `OperationFailed.QueryCertificateService`, and `Forbidden`. |Listener |
|[DescribeListenerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeListenerAttributes) |New response parameters `CertCenterCertificateId` and `CertificateSource`. ||
|[DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) |* New optional request parameter `Protocol`.<br><br>* New response parameters `CertCenterCertificateId` and `CertificateSource`.<br><br>* New error code `InvalidProtocol.Malformed`. ||


<span id=".MjAyNOW5tDEw5pyI"></span>
## October 2024


|API |Release note |Associated features |
|---|---|---|
|[ModifyLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerAttributes) |New optional request parameters `AddressIpVersion` and `EniIpv6Address`. |CLB instance |
|[CreateListener](https://docs.byteplus.com/en/docs/clb/CreateListener) |* New optional request parameters `StartPort`, `EndPort`, and `HealthCheck.Port`.<br><br>* New error codes `InvalidStartOrEndPort.Malformed`, `QuotaExceed.PortRangeListenerNumberEachInstance`. |Listener |
|[ModifyListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyListenerAttributes) |* New request parameter `HealthCheck.Port`, optional.<br><br>* New error codes `InvalidStartOrEndPort.Malformed`, `QuotaExceed.PortRangeListenerNumberEachInstance`. ||
|[DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) |New return data `StartPort`, `EndPort`, and `Port`. ||
|[DescribeListenerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeListenerAttributes) |New return data `StartPort`, `EndPort`, and `Port`. ||
|[CreateServerGroup](https://docs.byteplus.com/en/docs/clb/CreateServerGroup) |* New optional request parameter `AnyPortEnabled`.<br><br>* New error code `InvalidAnyPortEnabled.Malformed`. |Server group |
|[DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) |New response data `AnyPortEnabled`. ||
|[DescribeServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/DescribeServerGroupAttributes) |New response data `AnyPortEnabled`. ||


<span id=".MjAyNOW5tDA55pyI"></span>
## September 2024


|API |Release note |Associated features |
|---|---|---|
|[DescribeCertificates](https://docs.byteplus.com/en/docs/clb/DescribeCertificates) |New response data `SubjectAlternativeNames`. |Certificate |


<span id=".MjAyNOW5tDA35pyI"></span>
## July 2024


|API |Release note |Associated features |
|---|---|---|
|[ModifyLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerAttributes) |New error code `Forbidden`. |Server group |
|[RemoveServerGroupBackendServers](https://docs.byteplus.com/en/docs/clb/RemoveServerGroupBackendServers) |New error code `Forbidden`. ||


<span id=".MjAyNOW5tDA15pyI"></span>
## May 2024


|API |Release note |Associated features |
|---|---|---|
|[CreateListener](https://docs.byteplus.com/en/docs/clb/CreateListener) |* New optional request parameters: `ClientHeaderTimeout`, `ClientBodyTimeout`, `KeepaliveTimeout`, `ProxyConnectTimeout`, `ProxySendTimeout`, `ProxyReadTimeout`, `SendTimeout`, `SecurityPolicyId`.<br><br>* New error codes: `InvalidClientBodyTimeout.Malformed`, `InvalidClientBodyTimeout.ProtocolMismatch`, `InvalidClientHeaderTimeout.Malformed`, `InvalidClientHeaderTimeout.ProtocolMismatch`, `InvalidHealthCheck.Port.Malformed`, `InvalidKeepaliveTimeout.Malformed`, `InvalidKeepaliveTimeout.ProtocolMismatch`, `InvalidProxyConnectTimeout.Malformed`, `InvalidProxyConnectTimeout.ProtocolMismatch`, `InvalidProxyReadTimeout.Malformed`, `InvalidProxyReadTimeout.ProtocolMismatch`, `InvalidProxySendTimeout.Malformed`, `InvalidProxySendTimeout.ProtocolMismatch`, `InvalidSecurityPolicyId.Malformed`, `InvalidSecurityPolicyId.ProtocolMismatch`, `InvalidSendTimeout.Malformed`, `InvalidSendTimeout.ProtocolMismatch`.<br><br>* Removed error code `Forbidden`. |Listener |
|[ModifyListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerAttributes) |* New optional request parameters: `ClientHeaderTimeout`, `ClientBodyTimeout, KeepaliveTimeout`, `ProxyConnectTimeout`, `ProxySendTimeout`, `ProxyReadTimeout`, `SendTimeout`, `SecurityPolicyId`.<br><br>* New error codes: `InvalidClientBodyTimeout.Malformed`, `InvalidClientBodyTimeout.ProtocolMismatch`, `InvalidClientHeaderTimeout.Malformed`, `InvalidClientHeaderTimeout.ProtocolMismatch`, `InvalidHealthCheck.Port.Malformed`, `InvalidKeepaliveTimeout.Malformed`, `InvalidKeepaliveTimeout.ProtocolMismatch`, `InvalidProxyConnectTimeout.Malformed`, `InvalidProxyConnectTimeout.ProtocolMismatch`, `InvalidProxyReadTimeout.Malformed`, `InvalidProxyReadTimeout.ProtocolMismatch`, `InvalidProxySendTimeout.Malformed`, `InvalidProxySendTimeout.ProtocolMismatch`, `InvalidSecurityPolicyId.Malformed`, `InvalidSecurityPolicyId.ProtocolMismatch`, `InvalidSendTimeout.Malformed`, `InvalidSendTimeout.ProtocolMismatch`.<br><br>* Removed error code `Forbidden`. ||
|[DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) |New response parameters `ClientHeaderTimeout`, `ClientBodyTimeout`, `KeepaliveTimeout`, `ProxyConnectTimeout`, `ProxySendTimeout`, `ProxyReadTimeout`, `SendTimeout`, `SecurityPolicyId`. ||
|[DescribeListenerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeListenerAttributes) |New response parameters `ClientHeaderTimeout`, `ClientBodyTimeout`, `KeepaliveTimeout`, `ProxyConnectTimeout`, `ProxySendTimeout`, `ProxyReadTimeout`, `SendTimeout`, `SecurityPolicyId`. ||


<span id="4jMgiNEW"></span>
## April 2024


|API |Release note |Associated features |
|---|---|---|
|All APIs |First release of the API. |\-\- |
