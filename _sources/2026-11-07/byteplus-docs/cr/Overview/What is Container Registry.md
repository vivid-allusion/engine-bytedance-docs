---
title: "What is Container Registry"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/what-is-cr"
---

Container Registry (CR) provides a secure and highly available managed service for container images, Helm Charts, and other OCI artifact\-compliant cloud\-native artifacts, making it easy for enterprise users to manage the entire lifecycle of container images and Helm Charts.

<span id=".5Lqn5ZOB57G75Z6L"></span>
## Product Types

CR offers multiple types of CR instances, which you can create according to your actual needs.


* Standard Edition Instance: Provides capabilities such as dedicated data storage, dedicated Registry services, access control, image acceleration, and OCI package management, suitable for scenarios requiring secure hosting and large\-scale distribution.

* Micro Edition Instance: Provides basic image hosting capabilities for small and micro enterprises, as well as individual developers.

* Proxy repository: Acts as a proxy for external image sources such as Docker Hub, GHCR, or self\-built Docker Registry, locally caches commonly used images, enables accelerated pulling and stable access, and effectively addresses issues of slow or unstable access to overseas image sources.


<span id=".5Yqf6IO954m55oCn"></span>
## Features


* **Full Lifecycle Management**

   Supports the management of the entire lifecycle of images, including pushing, pulling, and cleaning.

* **Multi\-dimensional Security Assurance**

   Supports security scan of hosted images and generates multi\-dimensional image scanning reports along with corresponding remediation suggestions to ensure business security.

* **Multi\-region Ultra\-fast Distribution**

   Supports pulling images from the nearest location and synchronizing container images and Helm Charts between different instances in various regions, enabling single\-point pushing and global automatic synchronized distribution. It also supports large\-scale cluster pulling based on the P2P method.

* **Fine\-grained Authorization Management**

   Supports setting IAM policies for authorization management of users, differentiating resource control permissions at the user dimension.


<span id="rV8qpv0S"></span>
## Related references


* For a detailed comparison of product features for each product type, please see [product features](https://docs.byteplus.com/en/docs/cr/features).

* For quota limits of each instance, please see [usage limits](https://docs.byteplus.com/en/docs/cr/limits).

* For billing overview for each instance, please see [billing overview](https://docs.byteplus.com/en/docs/cr/billing-overview).
