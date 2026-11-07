---
title: "API release notes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/API_Updates"
---

This topic introduces the API updates of the Network Load Balancer (NLB).

<span id="SRYv5r9c"></span>
## September 2026


|API name |Release note |Associated features |
|---|---|---|
|[CreateNetworkLoadBalancer](https://docs.byteplus.com/en/docs/clb/CreateNetworkLoadBalancer) |New request parameter: DNSAffinity. |NLB instance |
|[ModifyNetworkLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerAttributes) |New request parameter: DNSAffinity. ||
|[DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) |New response parameter: DNSAffinity. ||
|[DescribeNetworkLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancerAttributes) |New response parameter: DNSAffinity. ||
|[CreateNLBListener](https://docs.byteplus.com/en/docs/clb/CreateNLBListener) |New request parameters: Cps, MaxConnections. |Listener |
|[ModifyNLBListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNLBListenerAttributes) |New request parameters: Cps, MaxConnections. ||
|[DescribeNLBListeners](https://docs.byteplus.com/en/docs/clb/DescribeNLBListeners) |New response parameter: Cps, MaxConnections. ||
|[DescribeNLBListenerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeNLBListenerAttributes) |New response parameter: Cps, MaxConnections. ||


<span id="dU8OFReY"></span>
## September 2025


|API name |Release note |Associated features |
|---|---|---|
|[DescribeNetworkLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancerAttributes) |Added response parameter: AccessLog structure, representing the access log information of an NLB instance. |NLB instance |
|[ModifyNetworkLoadBalancerAccessLog](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerAccessLog) |Added API to modify the access log configuration of an NLB instance. ||
|[ModifyNetworkLoadBalancerNetworkType](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerNetworkType) |New error code: Forbidden. ||
|[ModifyNLBListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNLBListenerAttributes) |New error code: InvalidCertificate.Conflict. |Listener |
|[DescribeNLBServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups)<br><br> |* New request parameters: InstanceIds.N, ServerIps.N.<br><br>* New error codes: InvalidServers.Ip.Malformed, LimitExceeded.ServerInstanceIdNumber, LimitExceeded.ServerIpNumber. |Server group |


<span id="V7MZ6FTd"></span>
## July 2025


|API name |Release note |Associated features |
|---|---|---|
|[CreateNLBListener](https://docs.byteplus.com/en/docs/clb/CreateNLBListener) |New request parameters: CACertificateId, CACertificateSource, CAEnabled, CertificateId, CertificateSource, PCACertificateId, SecurityPolicyType. |Listener |
|[ModifyNLBListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNLBListenerAttributes) |||
|[DescribeNLBListenerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeNLBListenerAttributes) |New response parameters: CACertificateId, CACertificateSource, CAEnabled, CertificateSource, PCACertificateId. ||
|[DescribeNLBListeners](https://docs.byteplus.com/en/docs/clb/DescribeNLBListeners) |||
|[DescribeNLBListenerCertificates](https://docs.byteplus.com/en/docs/clb/DescribeNLBListenerCertificates) |* New request parameter: Domain.<br><br>* New response parameter: CertificateSource. ||
|[DescribeNLBListenerHealth](https://docs.byteplus.com/en/docs/clb/DescribeNLBListenerHealth) |New request parameters: MaxResults, NextToken. ||
|[ModifyNLBListenerAdditionalCertificates](https://docs.byteplus.com/en/docs/clb/ModifyNLBListenerAdditionalCertificates) |Added API to modify the certificate of an NLB listener. ||
|[CreateNetworkLoadBalancer](https://docs.byteplus.com/en/docs/clb/CreateNetworkLoadBalancer) |New request parameter: ProjectName. |NLB instance |


<span id=".MjAyNOW5tDEw5pyI"></span>
## **June** 2025


|API name |Release note |Associated features |
|---|---|---|
|All APIs |First beta release of the API. |Network Load Balancer |
