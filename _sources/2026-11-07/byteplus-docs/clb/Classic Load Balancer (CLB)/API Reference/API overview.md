---
title: "API overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/API-overview"
---

This topic describes all the APIs of Classic Load Balancer (CLB). You are advised to use the [CLB SDK](https://docs.byteplus.com/en/docs/6406/114434) to call these APIs.

## CLB instances

|API Action |Functionality |
|---|---|
|[CreateLoadBalancer](https://docs.byteplus.com/en/docs/clb/CreateLoadBalancer) |Create a CLB instance. |
|[DeleteLoadBalancer](https://docs.byteplus.com/en/docs/clb/DeleteLoadBalancer) |Deletes a CLB instance. |
|[ModifyLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerAttributes) |Modifies the specified CLB instance. |
|[DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) |Query Classic Load Balancer (CLB) instances. |
|[DescribeLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancerAttributes) |Query the details of the specified CLB instance. |
|[ConvertLoadBalancerBillingType](https://docs.byteplus.com/en/docs/clb/ConvertLoadBalancerBillingType) |Changes the billing method of a CLB instance. |
|[RenewLoadBalancer](https://docs.byteplus.com/en/docs/clb/RenewLoadBalancer) |Renews a CLB instance of the Yearly/Monthly Subscription type. |
|[SetLoadBalancerRenewal](https://docs.byteplus.com/en/docs/clb/SetLoadBalancerRenewal) |Settings the renewal Type for Subscription Classic Load Balancer (CLB) instances. |
|[DescribeLoadBalancersBilling](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancersBilling) |Queries the billing information of the specified CLB instance. |
|[DescribeZones](https://docs.byteplus.com/en/docs/clb/DescribeZones) |Queries the mappings between the active and standby availability zones in the current region. |

## Listener

|API Action |Functionality |
|---|---|
|[CreateListener](https://docs.byteplus.com/en/docs/clb/CreateListener) |Creating a listener. |
|[DeleteListener](https://docs.byteplus.com/en/docs/clb/DeleteListener) |Delete the listener. |
|[ModifyListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyListenerAttributes) |Modifies the specified listener. |
|[DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) |Query listener. |
|[DescribeListenerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeListenerAttributes) |View the details of a specified listener. |
|[DescribeListenerHealth](https://docs.byteplus.com/en/docs/clb/DescribeListenerHealth) |Queries the health check information of the server associated with the specified listener. |
|[ModifyListenerDomainExtensions](https://docs.byteplus.com/en/docs/clb/ModifyListenerDomainExtensions) | Manage the additional domains of an HTTPS listener. |

## Backend server group

|API Action |Functionality |
|---|---|
|[CreateServerGroup](https://docs.byteplus.com/en/docs/clb/CreateServerGroup) |Create Server Group. |
|[DeleteServerGroup](https://docs.byteplus.com/en/docs/clb/DeleteServerGroup) |Deletes a server group. |
|[ModifyServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/ModifyServerGroupAttributes) |Modifies the specified server group. |
|[DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) |Query the Server Group. |
|[DescribeServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/DescribeServerGroupAttributes) |View the details of the specified Server Group. |
|[AddServerGroupBackendServers](https://docs.byteplus.com/en/docs/clb/AddServerGroupBackendServers) |Adds a server to the specified server group. |
|[RemoveServerGroupBackendServers](https://docs.byteplus.com/en/docs/clb/RemoveServerGroupBackendServers) |Remove backend servers for the specified backend server group. |

## ACL

|API Action |Functionality |
|---|---|
|[CreateAcl](https://docs.byteplus.com/en/docs/clb/CreateAcl) |Create an IAM policy group. |
|[DeleteAcl](https://docs.byteplus.com/en/docs/clb/DeleteAcl) |Delete an Identity and Access Management (IAM) policy group. |
|[ModifyAclAttributes](https://docs.byteplus.com/en/docs/clb/ModifyAclAttributes) |Modifies the specified ACL policy group. |
|[DescribeAcls](https://docs.byteplus.com/en/docs/clb/DescribeAcls) |Queries the Identity and Access Management (IAM) policy group. |
|[DescribeAclAttributes](https://docs.byteplus.com/en/docs/clb/DescribeAclAttributes) |View the details of the specified Identity and Access Management (IAM) policy group. |
|[AddAclEntries](https://docs.byteplus.com/en/docs/clb/AddAclEntries) |Adds IP entries to the specified ACL policy group. |
|[RemoveAclEntries](https://docs.byteplus.com/en/docs/clb/RemoveAclEntries) |Removes IP entries from the specified ACL policy group. |

## Forwarding rule

|API Action |Functionality |
|---|---|
|[CreateRules](https://docs.byteplus.com/en/docs/clb/CreateRules) |Add forwarding rules for a specified HTTP/HTTPS listener. |
|[DeleteRules](https://docs.byteplus.com/en/docs/clb/DeleteRules) |Deletes a forwarding rule of the specified HTTP or HTTPS listener. |
|[ModifyRules](https://docs.byteplus.com/en/docs/clb/ModifyRules) |Modify the backend server group or description of a forwarding rule in the specified HTTP/HTTPS listener. |
|[DescribeRules](https://docs.byteplus.com/en/docs/clb/DescribeRules) |Query the forwarding rules in the specified HTTP/HTTPS listener. |

## Certificate

|API Action |Functionality |
|---|---|
|[UploadCertificate](https://docs.byteplus.com/en/docs/clb/UploadCertificate) |Uploads a CA certificate or server certificate. |
|[DescribeCertificates](https://docs.byteplus.com/en/docs/clb/DescribeCertificates) |Queries the certificate list. |
|[DeleteCertificate](https://docs.byteplus.com/en/docs/clb/DeleteCertificate) |Deletes a certificate. |
|[ModifyCertificateAttributes](https://docs.byteplus.com/en/docs/clb/ModifyCertificateAttributes) |Modifies the name and description of the specified certificate. |

## Access log (Layer\-7)

|API Action |Functionality |
|---|---|
|[EnableAccessLog](https://docs.byteplus.com/en/docs/clb/EnableAccessLog) |Enables Layer\-7 access log collection for the specified CLB instance. |
|[DisableAccessLog](https://docs.byteplus.com/en/docs/clb/DisableAccessLog) |Disable the Layer 7 access log collection feature for a specified CLB instance. |

## Health check log

|API Action |Functionality |
|---|---|
|[CreateHealthCheckLogProject](https://docs.byteplus.com/en/docs/clb/CreateHealthCheckLogProject) |Create a log project for the CLB health check. |
|[DescribeHealthCheckLogProjectAttributes](https://docs.byteplus.com/en/docs/clb/DescribeHealthCheckLogProjectAttributes) |Query the information about a log project of the CLB health check. |
|[DeleteHealthCheckLogProject](https://docs.byteplus.com/en/docs/clb/DeleteHealthCheckLogProject) |Delete a log project of the CLB health check. |
|[AttachHealthCheckLogTopic](https://docs.byteplus.com/en/docs/clb/AttachHealthCheckLogTopic) |Bind a log topic to a specified CLB instance. |
|[DetachHealthCheckLogTopic](https://docs.byteplus.com/en/docs/clb/DetachHealthCheckLogTopic) |Unbind a log topic from a specified CLB instance. |
|[DescribeHealthCheckLogTopicAttributes](https://docs.byteplus.com/en/docs/clb/DescribeHealthCheckLogTopicAttributes) |Query the information about the CLB instance bound to a specified log topic. |

## Tag APIs

|API Action |Functionality |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/clb/TagResources) |Add a user tag to a CLB resource. |
|[UntagResources](https://docs.byteplus.com/en/docs/clb/UntagResources) |Delete user tag of a CLB resource. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/clb/ListTagsForResources) |Queries the tag information of CLB resources meeting the query criteria. |
