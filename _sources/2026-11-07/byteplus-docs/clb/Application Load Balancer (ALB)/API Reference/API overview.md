---
title: "API overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Sample-responses"
---

Welcome to use BytePlus Application Load Balancer (ALB). You can use the Open API described in this document to perform related operations on ALB services, such as instance management, configuring a listener, creating a backend server group, configuring a health check policy, managing a certificate, and more.

You can use HTTP requests to call the APIs of BytePlus cloud services. Add request parameters to the request and send an HTTP request to the service address of the API. The system returns result data based on the content of the request. Before using HTTP requests, you need to understand the following:

* [Call method](https://docs.byteplus.com/docs/clb/ALB-Signature-method)

* [Common error codes](https://docs.byteplus.com/docs/clb/Error-codes)

## ALB instance

|**API** |**Notes** |
|---|---|
|[CreateLoadBalancer](https://docs.byteplus.com/docs/clb/ALB-CreateLoadBalancer) |Creating an ALB instance. |
|[DeleteLoadBalancer](https://docs.byteplus.com/docs/clb/ALB-DeleteLoadBalancer) |Deleting an ALB instance. |
|[ModifyLoadBalancerAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyLoadBalancerAttributes) |Modifying the specified ALB instance. |
|[DescribeLoadBalancers](https://docs.byteplus.com/docs/clb/ALB-DescribeLoadBalancers) |Querying an ALB instance list. |
|[DescribeLoadBalancerAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeLoadBalancerAttributes) |Querying the details of an ALB instance. |
|[ModifyLoadBalancerType](https://docs.byteplus.com/docs/clb/ModifyLoadBalancerType) |Changing the ALB instance network type. |
|[ModifyLoadBalancerZones](https://docs.byteplus.com/docs/clb/ModifyLoadBalancerZones) |Changing the ALB instance availability zone. |
|[CloneLoadBalancer](https://docs.byteplus.com/docs/clb/CloneLoadBalancer) |Cloning an ALB instance. |
|[DescribeZones](https://docs.byteplus.com/docs/clb/ALB-DescribeZones) |Querying the ALB supported AZ List. |

## Listener

|**API** |**Notes** |
|---|---|
|[CreateListener](https://docs.byteplus.com/docs/clb/ALB-CreateListener) |Creating a listener. |
|[DeleteListener](https://docs.byteplus.com/docs/clb/ALB-DeleteListener) |Deleting a listener. |
|[ModifyListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyListenerAttributes) |Modifying the specified listener. |
|[DescribeListeners](https://docs.byteplus.com/docs/clb/ALB-DescribeListeners) |Querying a listener list. |
|[DescribeListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeListenerAttributes) |Querying the details of specified listener. |
|[DescribeListenerHealth](https://docs.byteplus.com/docs/clb/ALB-DescribeListenerHealth) |Query the health check information of backend servers associated with a specified listener. |

## Server Group

|**API** |**Notes** |
|---|---|
|[CreateServerGroup](https://docs.byteplus.com/docs/clb/ALB-CreateServerGroup) |Creating a server group. |
|[DeleteServerGroup](https://docs.byteplus.com/docs/clb/ALB-DeleteServerGroup) |Deleting a server group. |
|[DescribeServerGroups](https://docs.byteplus.com/docs/clb/ALB-DescribeServerGroups) |Querying a server group list. |
|[DescribeServerGroupAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeServerGroupAttributes) |Querying the server group details. |
|[ModifyServerGroupAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyServerGroupAttributes) |Modifying the specified server group details. |
|[AddServerGroupBackendServers](https://docs.byteplus.com/docs/clb/ALB-AddServerGroupBackendServers) |Adding the backend servers to a specified server group. |
|[ModifyServerGroupBackendServers](https://docs.byteplus.com/docs/clb/ModifyServerGroupBackendServers) |Modifying a backend server within the specified server group. |
|[RemoveServerGroupBackendServers](https://docs.byteplus.com/docs/clb/ALB-RemoveServerGroupBackendServers) |Removing a backend server from the specified server group. |
|[DescribeServerGroupBackendServers](https://docs.byteplus.com/docs/clb/DescribeServerGroupBackendServers) |Querying the information of backend servers in the specified server group. |

## Health Check

|**API** |**Notes** |
|---|---|
|[CreateHealthCheckTemplates](https://docs.byteplus.com/docs/clb/CreateHealthCheckTemplates) |Creating a health check template. |
|[DeleteHealthCheckTemplates](https://docs.byteplus.com/docs/clb/DeleteHealthCheckTemplates) |Deleting the health check template. |
|[DescribeHealthCheckTemplates](https://docs.byteplus.com/docs/clb/DescribeHealthCheckTemplates) |Getting the health check template list. |
|[ModifyHealthCheckTemplatesAttributes](https://docs.byteplus.com/docs/clb/ModifyHealthCheckTemplatesAttributes) |Modifying the health check template attributes. |

## Forwarding rule

|**API** |**Notes** |
|---|---|
|[CreateRules](https://docs.byteplus.com/docs/clb/ALB-CreateRules) |Adding the forwarding rules to a listener. |
|[DeleteRules](https://docs.byteplus.com/docs/clb/ALB-DeleteRules) |Deleting a forwarding rule. |
|[DescribeRules](https://docs.byteplus.com/docs/clb/ALB-DescribeRules) |Getting the list of forwarding rules. |
|[ModifyRules](https://docs.byteplus.com/docs/clb/ALB-ModifyRules) |Modifying a forwarding rule. |

## Certificate interface

|**API** |**Notes** |
|---|---|
|[UploadCertificate](https://docs.byteplus.com/docs/clb/ALB-UploadCertificate) |Uploading a server certificate. |
|[DeleteCertificate](https://docs.byteplus.com/docs/clb/ALB-DeleteCertificate) |Deleting an unassociated server certificate. |
|[DescribeCertificates](https://docs.byteplus.com/docs/clb/ALB-DescribeCertificates) |Querying the server certificate list. |
|[ModifyCertificateAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyCertificateAttributes) |Modifying the server certificate attributes. |
|[ReplaceCertificate](https://docs.byteplus.com/docs/clb/ReplaceCertificate) |Replacing a server certificate. |
|[UploadCACertificate](https://docs.byteplus.com/docs/clb/UploadCACertificate) |Uploading a CA certificate. |
|[DeleteCACertificate](https://docs.byteplus.com/docs/clb/DeleteCACertificate) |Deleting an unassociated CA certificate. |
|[DescribeCACertificates](https://docs.byteplus.com/docs/clb/DescribeCACertificates) |Querying a CA certificate list. |
|[ModifyCACertificateAttributes](https://docs.byteplus.com/docs/clb/ModifyCACertificateAttributes) |Modifying the CA certificate attributes. |
|[ReplaceCACertificate](https://docs.byteplus.com/docs/clb/ReplaceCACertificate) |Replacing a CA certificate. |
|[DescribeAllCertificates](https://docs.byteplus.com/docs/clb/DescribeAllCertificates) |Querying all certificate lists. |

## Access Log

|**API** |**Notes** |
|---|---|
|[EnableAccessLog](https://docs.byteplus.com/docs/clb/ALB-EnableAccessLog) |Enabling an access log. |
|[DisableAccessLog](https://docs.byteplus.com/docs/clb/ALB-DisableAccessLog) |Disabling an access log. |
|[EnableTLSAccessLog](https://docs.byteplus.com/docs/clb/EnableTLSAccessLog) |Enabling access log delivery to TLS and bind the LB to the Topic. |
|[DisableTLSAccessLog](https://docs.byteplus.com/docs/clb/DisableTLSAccessLog) |Disabling access log delivery to TLS and unbind the binding relationship between the Topic and the LB. |

## Health check log

|**API** |**Notes** |
|---|---|
|[EnableHealthLog](https://docs.byteplus.com/docs/clb/EnableHealthLog) |Enabling health check log collection and bind the LB to the Topic. |
|[DisableHealthLog](https://docs.byteplus.com/docs/clb/DisableHealthLog) |Disabling health check log collection and unbind the binding relationship between the Topic and the LB. |

## Access control

|**API** |**Notes** |
|---|---|
|[CreateAcl](https://docs.byteplus.com/docs/clb/ALB-CreateAcl) |Creating an ACL. |
|[DeleteAcl](https://docs.byteplus.com/docs/clb/ALB-DeleteAcl) |Deleting an ACL. |
|[ModifyAclAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyAclAttributes) |Modifying the specified ACL. |
|[DescribeAcls](https://docs.byteplus.com/docs/clb/ALB-DescribeAcls) |Querying an ACL list. |
|[DescribeAclAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeAclAttributes) |Querying the details of the specified ACL. |
|[AddAclEntries](https://docs.byteplus.com/docs/clb/ALB-AddAclEntries) |Adding the IP entries to a specified ACL. |
|[RemoveAclEntries](https://docs.byteplus.com/docs/clb/ALB-RemoveAclEntries) |Deleting the IP entries from the specified ACL. |

## Custom configuration

|**API** |**Notes** |
|---|---|
|[CreateCustomizedCfg](https://docs.byteplus.com/docs/clb/CreateCustomizedCfg) |Creating a custom configuration. |
|[DeleteCustomizedCfg](https://docs.byteplus.com/docs/clb/DeleteCustomizedCfg) |Deleting a custom configuration. |
|[ModifyCustomizedCfgAttributes](https://docs.byteplus.com/docs/clb/ModifyCustomizedCfgAttributes) |Modifying the specified custom configuration. |
|[DescribeCustomizedCfgs](https://docs.byteplus.com/docs/clb/DescribeCustomizedCfgs) |Querying the custom configuration list. |
|[DescribeCustomizedCfgAttributes](https://docs.byteplus.com/docs/clb/DescribeCustomizedCfgAttributes) |Querying the details of a specified custom configuration. |

## Tag interface

|**API** |**Notes** |
|---|---|
|[TagResources](https://docs.byteplus.com/docs/clb/ALB-TagResources) |Adding the tags to resources. |
|[UntagResources](https://docs.byteplus.com/docs/clb/ALB-UntagResources) |Deleting the tags for resources. |
|[ListTagsForResources](https://docs.byteplus.com/docs/clb/ALB-ListTagsForResources) |Querying the resource tags. |
