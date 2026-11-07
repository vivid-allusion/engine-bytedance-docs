---
title: "Instance metadata overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Instance-metadata-overview"
---

VCI integrates with the Metadata Server and supports the binding of IAM roles and the acquisition of STS tokens for the bound roles via the Metadata Server, to implement business logic and permission control.

<span id=".5Yqf6IO95LyY5Yq_"></span>
## Feature advantages

Obtaining STS tokens through the Metadata Server improves the standardization and security of access authentication for VCIs and the add\-ons deployed in them.


* This avoids the risk of leaking access keys (including access key IDs and secret access keys) that may arise from specifying access keys directly, while enabling more fine\-grained permission control.

* It makes it easier to obtain basic information about VCI instances, such as the hostname, instance ID, instance specifications, and the region or availability zone they belong to.


<span id=".55u45YWz6ZO-5o6l"></span>
## References

You can retrieve metadata inside VCIs and perform system configuration to complete information initialization. For related operations on metadata, see [Querying instance metadata](https://docs.byteplus.com/en/docs/vke/Viewing-instance-metadata).
