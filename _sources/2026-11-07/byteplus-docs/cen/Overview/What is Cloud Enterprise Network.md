---
title: "What is Cloud Enterprise Network"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Product-Overview-01"
---

Cloud Enterprise Network (CEN) provides the capability to quickly build high\-speed, high\-quality, and stable networks between cross\-region Virtual Private Clouds (VPCs) and on\-premises data centers (IDCs), enabling you to establish a global cloud network with enterprise\-scale and communication capabilities.

> **tip**

> The multi\-IDC intercommunication is in the beta stage. If you need a trial, please contact your account manager.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6bd73f96da8780e636cf35aa7712476d.png)

## Compositions

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_516c5af76be090f366521fdb2f1d9e2f.png)

|Item |Explanation |
|---|---|
|CEN instance |It is used to attach different network instances, enabling private network interconnectivity between instances within the same region or across different regions. |
|Network instance |This topic refers to instances that can be attached to a CEN instance. Supported types include:<br><br><br>* **Virtual Private Cloud**: Once a VPC is attached to a CEN instance, it can establish private network connectivity with other attached network instances.<br><br>* **Direct Connect Gateway**: Attaching a Direct Connect Gateway to a CEN instance enables connectivity between the on\-premises IDC connected to the gateway and other cloud\-based network instances attached to the CEN. The Direct Connect Gateway must be used in conjunction with the Direct Connect service. For detailed information, see [What is Direct Connect](https://docs.byteplus.com/en/docs/directconnect/What-is-Direct-Connect). |
|Bandwidth package |When different network instances require cross\-region private network interconnection, you need to associate a bandwidth package with your CEN instance. The bandwidth package also serves as the basis for billing. |
|Inter\-region bandwidth |To enable private connectivity between network instances across different regions, you must allocate private interconnection bandwidth from the bandwidth package between the respective interconnected regions. |
