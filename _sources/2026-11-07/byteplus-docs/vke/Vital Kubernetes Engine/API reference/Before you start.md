---
title: "Before you start"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/API-Usage-notes"
---

This topic mainly describes the information that you need to obtain before you call VKE APIs.

<span id=".5pGY6KaB"></span>
## Summary

BytePlus VKE is an enterprise\-grade container management platform in the cloud by using Kubernetes. It deeply integrates with the new generation of cloud\-native technologies to provide high\-performance Kubernetes container cluster management services with containers at their core. This helps you quickly create containerized applications.

<span id=".6LCD55So6K-05piO"></span>
## API call description

VKE supports API calls through HTTPS requests. For more information, see [Calling methods](https://docs.byteplus.com/en/docs/vke/Request-structure).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

Before you call an API, make sure that the following preparations are made:


* A BytePlus root user has been created and has completed the required preparations, such as real name authentication, account top\-up, and authorization. For details, see [Preparations](https://docs.byteplus.com/en/docs/vke/Preparations).

* Your account balance is not zero when coupons are excluded, and is not less than USD 100 when coupons are included. This ensures that you can create pay\-as\-you\-go resources.

* The permissions to use VKE and for VKE to use cloud resources have been granted. For information about dependent cloud service resources, see [Cloud service dependencies](https://docs.byteplus.com/en/docs/vke/Dependencies-between-VKE-and-other-cloud-services).

* ‌Current VKE cluster quota and dependent cloud service limits are within available capacity. For limits on various resources, see [Resource limits](https://docs.byteplus.com/en/docs/vke/Limits).

* If you need to create an Elastic Compute Service (ECS) instance running the Linux operating system and bind an SSH key pair to the instance, make sure that you have created a key pair in the target project. For detailed operations, see [Creating key pairs](https://docs.byteplus.com/en/docs/ecs/Creating-key-pairs).


<span id=".6LS555So6K-05piO"></span>
## Billing description

When you call APIs to create clusters, nodes, node pools, and other resources, VKE will create basic cloud resources within your account based on your request parameters. These include Load Balancer instances, NAT Gateways, EIPs, and cloud disks. These resources will incur fees. For detailed billing information, see [Product billing](https://docs.byteplus.com/en/docs/vke/Billing).
