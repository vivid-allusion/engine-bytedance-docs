---
title: "Overview of storage mounting"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Overview_of_storage_mounting"
---

EMR Serverless provides multiple storage mounting solutions, supporting the mounting of corresponding storage products to EMR Serverless compute groups or jobs as shared file systems. After mounting, you can operate remote data just like local files, with minimal code modification.

<span id="21f68f30"></span>
# Supported storage products and protocols

The currently supported storage products for mounting include: TOS, NAS, and vePFS. Comparison details are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b3b6857b1b84b84a297ce830cf9ddab~tplv-goo7wpa0wc-image.image) </span>


|Supported storage products |Types of storage mounting protocols |Key points for mounting |
|---|---|---|
|vePFS |* FSX |* You need to create the FSX protocol service and access point yourself. |
||* Native |* Fixed compute resources in dedicated queues support the native vePFS mounting capability. This method is disabled by default. To enable it, contact BytePlus technical support to apply for inclusion in the feature allowlist.<br><br>* vePFS can be added as EMR global storage. After adding, EMR will automatically create the vePFS mounting service for you, which is used for mounting. |
|NAS |* FSX |* NAS must be of the cache type.<br><br>* You need to create the FSX access point yourself. |
|TOS |* FSX<br><br>* S3FS |* You need to obtain access keys AK and SK with TOS access permissions. Mounting and encrypted authentication are achieved through AK and SK. |


<span id="e53f5be7"></span>
# Limits


|Details |Note |
|---|---|
|General limits |* The currently supported compute group types for mounting storage include: general compute group, Ray Cluster, and Ray Serve.<br><br>* The total number of mount paths per compute group cannot exceed 20. |
|Network requirements |When mounting storage using the FSX method, ensure that the access point VPC and the EMR storage network VPC are the same VPC. |
|vePFS mounting |When mounting vePFS using the native method, adding EMR global storage automatically creates the vePFS mounting service, enabling storage mounting.<br><br><br>* When the first vePFS is added as EMR global storage in EMR, EMR will create a mounting service for you and bind the vePFS instance to this mounting service.<br><br>* When continuing to add vePFS as EMR global storage:<br><br>   * When the VPC/subnet associated with the vePFS to be added **matches** the VPC/availability zone of the existing mounting service, the added vePFS will be bound to the previously created mounting service.<br><br>   * When the VPC/subnet associated with the vePFS to be added **does not match** the VPC/availability zone of the existing mounting service, EMR will create a new mounting service for you, and the added vePFS will be bound to this newly created mounting service.<br><br><br>Mounting service quantity limits:<br><br><br>* When adding EMR global storage, each region supports creating up to 2 mounting services; each mounting service can be associated with up to 2 vePFS instances.<br><br>* When associating a queue with vePFS, each queue can be associated with only one mounting service, and up to two vePFS instances within the same mounting service. |


<span id="96ff27be"></span>
# Procedure

The following introduces the general procedure for mounting various storage products. For detailed operation guidance, refer to [Mount vePFS](https://docs.byteplus.com/docs/E-MapReduce/Mount_vePFS), [Mount NAS](https://docs.byteplus.com/docs/E-MapReduce/Mount_NAS), and [Mount TOS](https://docs.byteplus.com/docs/E-MapReduce/Mount_TOS).


|Procedure |vePFS\-FSX |vePFS\-Native |NAS\-FSX |TOS\-FSX |TOS\-S3FS |
|---|---|---|---|---|---|
|1. Prerequisites |Enable vePFS and EMR queue |Enable vePFS and EMR queue |Enable NAS and EMR queue |Enable TOS and EMR queue; obtain AK and SDK |Enable TOS and EMR queue; obtain AK and SDK |
|2. Access point configuration |Manually create access point |Add EMR global storage, automatically creates an access service |Manually create access point |No operation required |No operation required |
|3. EMR queue storage network configuration |Configure EMR queue storage network |Configure EMR queue storage network |Configure EMR queue storage network |Configure EMR queue storage network |No operation required |
|4. Storage mounting |Mount storage in a queue, compute group, or task |Mount storage in a queue, compute group, or task |Mount storage in a queue, compute group, or task |Mount storage in a queue, compute group, or task |Mount storage in a queue, compute group, or task |
