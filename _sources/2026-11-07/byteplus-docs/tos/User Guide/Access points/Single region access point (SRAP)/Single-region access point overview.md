---
title: "Single-region access point overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Single-region-access-point-overview"
---

A Single\-Region Access Point is an access entry provided by TOS that allows independent permission configuration, offering a dedicated access domain name for storage buckets. You can create multiple access points for the same storage bucket, and configure customized access control policies and network access methods for different business requirements or user groups.

<span id="409d88ed"></span>
## Application Scenarios

A single\-region access point is suitable for scenarios in which multiple business lines share the same storage bucket and require permission isolation. For example:


* Enterprise Multi\-Business Line Data Isolation: Within an enterprise, dozens or even hundreds of business lines need to access their own independent datasets in the same storage bucket, and such access must be isolated. As hundreds of business lines share a single storage bucket, the complexity and management difficulty of bucket policies will increase significantly. You can configure independent entry points using single\-region access points, breaking down large bucket policies into multiple independent, business\-specific policies. Users only need to focus on the authorization objects and operation permissions for a single entry point, without considering the permission logic of other business scenarios, thereby simplifying permission configuration in large\-scale data sharing scenarios.

* AI/Big Data Training Environment Isolation: The AI team uses object storage as the training data lake, but wishes to ensure that only training clusters running within designated VPCs can access the data, thereby preventing the test environment from misreading sensitive data. You can configure VPC access policies through single\-region access points, allowing only specified VPCs to access data via the access point and achieving VPC\-level access isolation.


<span id="dbb09f98"></span>
## Functional Features


* Independent Access Domain Name: A single\-region access point provides an independent access domain name for the storage bucket, allowing access to bucket resources through this domain name. It also supports providing an entry point for the TOS accelerator, enabling AZ\-level domain name resolution and scheduling capability.

* Permissions are organized by access point: each access point can be configured with an independent access control policy. When users access resources within TOS through an access point, they are permitted to do so only according to the resources, conditions, and operations authorized in the access point policy, thereby enabling differentiated data access control for different business lines and roles.

* Network Access Control: Single\-region access points support the configuration of network access methods, allowing restrictions so that only specified VPCs or public networks can access storage resources, thereby enabling flexible network access management.


<span id="e6d86758"></span>
## Workflow


1. [Create Single Region Access Point](https://docs.byteplus.com/docs/tos/Create-single-region-access-point)

2. [Use Single-Region Access Point](https://docs.byteplus.com/docs/tos/Use-a-single-region-access-point)
