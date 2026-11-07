---
title: "Application scenarios"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Product-Overview-03"
---

## Multi\-VPC interconnection scenarios

By attaching multiple Virtual Private Clouds (VPCs) from the same or different regions to the same CEN instance, you can enable network connectivity between these VPCs within or across regions.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_acddb7b30f08c38fee48420d7b84f3d4.png)

## Cloud Service access via Direct Connect scenario

To achieve network connectivity between an on\-premises IDC (connected via a Direct Connect Gateway) and cloud services in the 100.64.0.0/10 segment, attach the VPCs (in the same region as the cloud services) and the Direct Connect Gateway to the same CEN instance, then configure cloud service access.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7a9368ccdb633431a523ac573aa13e7e.png)

## Hybrid Cloud scenarios

By attaching VPCs and Direct Connect Gateways from different regions to the same CEN instance, you can enable cross\-region network connectivity between multiple cloud\-based VPCs and on\-premises IDCs, building a hybrid cloud environment.

Communication in a hybrid cloud requires the use of Direct Connect services, see [What is Direct Connect](https://docs.byteplus.com/en/docs/directconnect/What-is-Direct-Connect) for details.

> **tip**

> The multi\-IDC intercommunication is in the beta stage. If you need a trial, please contact your account manager.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_705acc91145c047be2945b69f2b24966.png)
