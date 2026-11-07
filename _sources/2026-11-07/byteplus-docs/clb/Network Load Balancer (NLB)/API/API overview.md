---
title: "API overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-API-overview-2"
---

This topic provides a detailed list of all NLB APIs.

<span id=".572R57uc5Z6L6LSf6L295Z2H6KGh5a6e5L6L"></span>
## NLB instance


|API |Feature |
|---|---|
|[CreateNetworkLoadBalancer](https://docs.byteplus.com/en/docs/clb/CreateNetworkLoadBalancer) |Create NLB instance. |
|[DeleteNetworkLoadBalancer](https://docs.byteplus.com/en/docs/clb/DeleteNetworkLoadBalancer) |Delete NLB instance. |
|[ModifyNetworkLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerAttributes) |Modify the specified NLB information. |
|[ModifyNetworkLoadBalancerBandwidthPackage](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerBandwidthPackage) |Add a public NLB instance to or remove it from a shared bandwidth package. |
|[ModifyNetworkLoadBalancerNetworkType](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerNetworkType) |Modify the network type of an NLB instance. |
|[ModifyNetworkLoadBalancerSecurityGroups](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerSecurityGroups) |Modify the security groups associated with a specified NLB instance. |
|[ModifyNetworkLoadBalancerZones](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerZones) |Modify the supported zones of a specified NLB instance. |
|[DescribeNetworkLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancerAttributes) |Query details of the specified NLB instance. |
|[DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) |Query NLB instances that meet specified conditions. |
|[DescribeNLBZones](https://docs.byteplus.com/en/docs/clb/DescribeZones) |Query Availability Zones supported by NLB in the current region. |
|[ModifyNetworkLoadBalancerAccessLog](https://docs.byteplus.com/en/docs/clb/ModifyNetworkLoadBalancerAccessLog) |Configure access log. |


<span id=".5pyN5Yqh5Zmo57uE"></span>
## Server group


|API |Feature |
|---|---|
|[CreateNLBServerGroup](https://docs.byteplus.com/en/docs/clb/CreateNLBServerGroup) |Create a server group. |
|[DeleteNLBServerGroup](https://docs.byteplus.com/en/docs/clb/DeleteNLBServerGroup) |Delete the server group. |
|[ModifyNLBServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNLBServerGroupAttributes) |Modify the specified server group. |
|[DescribeNLBServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups) |Query server groups that meet specified conditions. |
|[DescribeNLBServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroupAttributes) |Query the details of the specified server group. |


<span id=".5ZCO56uv5pyN5Yqh5Zmo"></span>
## Backend server


|API |Feature |
|---|---|
|[AddNLBBackendServers](https://docs.byteplus.com/en/docs/clb/AddNLBBackendServers) |Add backend servers to specified backend server groups. |
|[ModifyNLBBackendServersAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNLBBackendServersAttributes) |Modify a specified backend server. |
|[RemoveNLBBackendServers](https://docs.byteplus.com/en/docs/clb/RemoveNLBBackendServers) |Remove backend servers from specified server groups. |


<span id=".55uR5ZCs5Zmo"></span>
## Listener


|API |Feature |
|---|---|
|[CreateNLBListener](https://docs.byteplus.com/en/docs/clb/CreateNLBListener) |Create listener. |
|[DeleteNLBListener](https://docs.byteplus.com/en/docs/clb/DeleteNLBListener) |Delete listener. |
|[ModifyNLBListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNLBListenerAttributes) |Modify the specified listener. |
|[DescribeNLBListeners](https://docs.byteplus.com/en/docs/clb/DescribeNLBListeners) |Query listeners that meet the specified condition. |
|[DescribeNLBListenerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeNLBListenerAttributes) |View the details of a specified listener. |
|[DescribeNLBListenerHealth](https://docs.byteplus.com/en/docs/clb/DescribeNLBListenerHealth) |Query the health check information of backend servers associated with a specified listener. |
|[DescribeNLBListenerCertificates](https://docs.byteplus.com/en/docs/clb/DescribeNLBListenerCertificates) |Query the certificate information under a specified TLS listener. |


<span id=".5qCH562-"></span>
## TLS security policy

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The TLS listener is in Beta. For trial requests, please contact the account manager.</div>



|API |Feature |
|---|---|
|[CreateNLBSecurityPolicy](https://docs.byteplus.com/en/docs/clb/CreateNLBSecurityPolicy) |Create custom TLS security policy. |
|[ModifyNLBSecurityPolicyAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNLBSecurityPolicyAttributes) |Modify custom TLS security policy |
|[DeleteNLBSecurityPolicy](https://docs.byteplus.com/en/docs/clb/DeleteNLBSecurityPolicy) |Delete TLS custom security policy. |
|[DescribeNLBSecurityPolicies](https://docs.byteplus.com/en/docs/clb/DescribeNLBSecurityPolicies) |Query TLS custom security policies that match specified conditions. |
|[DescribeNLBSystemSecurityPolicies](https://docs.byteplus.com/en/docs/clb/DescribeNLBSystemSecurityPolicies) |Query TLS system security policy |


<span id=".5qCH562-"></span>
## Tag


|API |Feature |
|---|---|
|[TagNLBResources](https://docs.byteplus.com/en/docs/clb/TagNLBResources) |Add custom tags for an NLB resource. |
|[UntagNLBResources](https://docs.byteplus.com/en/docs/clb/UntagNLBResources) |Delete custom tags from an NLB resource. |
|[ListTagsForNLBResources](https://docs.byteplus.com/en/docs/clb/ListNLBTagsForResources) |Query tag information of NLB resources that meet specified conditions. |
