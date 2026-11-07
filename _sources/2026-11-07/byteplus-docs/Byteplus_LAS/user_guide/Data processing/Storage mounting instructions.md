---
title: "Storage mounting instructions"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Storage_mounting_instructions"
---

LAS provides multiple storage mounting solutions, supporting the mounting of corresponding storage products to LAS development machines or tasks as shared file systems. After mounting, you can operate remote data as if it were local files, with minimal code modifications. This article introduces the key points of storage mounting operations.

<span id="3f3f1fea"></span>
# Supported storage products and protocols

Comparison details are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/973bad1f185247a6bda5cd95a1db364a~tplv-goo7wpa0wc-image.image) </span>


|Storage products |Mounting protocol |Mounting principle |Notes/Limitations |
|---|---|---|---|
|vePFS |* FSX |* You need to create the FSX protocol service and the access point in the VPC where the instance is located, and then mount via the access point. |* The availability zone of the vePFS instance must be the same as the availability zone of the LAS queue.<br><br>* When creating access points in certain types of vePFS instances, additional access point fees may be incurred. For details, refer to the vePFS billing documentation. |
||* Native |* To use this method, submit a ticket to BytePlus technical support to create a mounting service for you, and then mount via this service.<br><br>* To use a dedicated LAS queue (that is, an EMR Serverless queue resource), create the mount service in the EMR product and bind it to the queue resource. |* You can apply for up to 2 mounting services per region; each mounting service can be associated with up to 5 vePFS instances. |
|NAS |* FSX |* You need to create the FSX access point, and then mount via the access point. |* NAS must be selected as cache type.<br><br>* The access point and LAS must be in the same VPC. |
|TOS |* S3FS<br><br>* FSX |* You need to obtain access keys AK and SK with TOS access permissions. Use AK and SK to perform mounting and encrypted authentication. |* TOS and LAS must be in the same region. |


<span id="0dc87e38"></span>
# Mount vePFS

After creating the vePFS file system, you can refer to the following content to select the required mounting method and mount vePFS to LAS.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When mounting vePFS to LAS, you must first complete the preparation steps on the vePFS side, including setting up the access point or mounting service, before proceeding to mount in LAS.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a dedicated LAS queue (that is, EMR Serverless queue resources) and have already completed the vePFS mounting preparation in the EMR Serverless queue (with an existing FSX access point or mount service), you do not need to perform the following vePFS instance preparation. You can directly mount vePFS in LAS using the existing FSX access point or mount service. For detailed instructions on mounting vePFS in EMR Serverless, see <a href="https://docs.byteplus.com/en/docs/E-MapReduce/Mount_vePFS">Mount vePFS</a>.</div>



<span id="95723a87"></span>
## Preparation: Based on FSX

When mounting using the FSX method, you need to create the FSX protocol service and access point on the vePFS side. This operation is not required when using the Native method.


1. Create an FSX protocol service. To mount vePFS using the FSX protocol, you need to create an FSX protocol service for the veFSX file system.

2. Create access point. When mounting vePFS via the FSX protocol, you also need to create an access point for the FSX protocol service in vePFS for subsequent mounting and access.

   The key configuration parameters are described as follows.

   
   |Key parameters |Configuration instructions |
   |---|---|
   |Private network |Ensure that the VPC configured in the network information remains consistent with the VPC used for mounting storage in LAS later. |
   |Root directory of the access point |Enter "/" (to restrict access to files under a specific directory, enter the specific directory). |
   


<span id="a854d081"></span>
## Preparation: Based on Native

When mounting using the Native method, you need to submit a ticket to contact technical support personnel. Technical support will create the mounting service for you. Once completed, you can mount vePFS in LAS using the Native method.

<span id="fca1acf6"></span>
## Mount vePFS

In the "Storage path mounting" of the development machine or task, select "Mount vePFS" and configure the relevant parameters.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, mounting multiple vePFS paths is supported. Up to 20 vePFS paths can be mounted per region. When using the Native mounting method, you can apply for up to 2 mounting services and mount up to 5 Native\-type vePFS paths.</div>



|Development machine configuration interface diagram |Task configuration interface diagram |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f61c431785f48d98c0c5ba1d4a4177b~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2796ab615d5d449aa5a14e0c71816e29~tplv-goo7wpa0wc-image.image) </span> |


There are differences in the configuration key points for FSX and Native. The comparison is as follows.


1. Configure the "Storage path mount" parameters for the development machine or task.

   
   |Parameters |Configuration instructions \- FSX |Configuration instructions \- Native |
   |---|---|---|
   |File system name |Select the file system to be mounted from the dropdown list. ||
   |File System Access Point |Select the created access point from the dropdown list. |No selection is required for the Native scenario. Leave the access point blank. When the access point is blank, the system mounts vePFS using Native method by default. |
   |File system path |Select the file system path of the vePFS to be mounted. ||
   |Mount path |Set the path for mounting the current storage in LAS. ||
   

2. Configure the network information for the development machine or task.

   
   |Parameters |Configuration instructions \- FSX |Configuration instructions \- Native |
   |---|---|---|
   |Advanced network configuration/Network connection |* When mounting vePFS using the FSX method, ensure that the vePFS access point and LAS are in the same VPC. That is, make sure the “Advanced network configuration” switch is turned on here, and the private network matches the private network used for mounting vePFS above, both being the same VPC.<br><br>* The system will automatically preselect the corresponding VPC for you based on the configuration result of the vePFS mounted above. You can continue to select the security group for the VPC. |No configuration required. |
   


<span id="026bb2e0"></span>
# Mount NAS

<span id="645e02f4"></span>
## Preparation


1. Enable and bind FSX protocol service

   * To enable and bind the FSX protocol service for a NAS instance, contact the NAS storage team. To request service activation, please [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical personnel.

   * Ensure that the VPC where the file system instance access point is located is consistent with the VPC configured in the network information when mounting storage in subsequent LAS operations.

2. Create an access point. When mounting NAS via the FSX protocol, you also need to create an access point on NAS for subsequent mounting and access.

   The key configuration parameters are described as follows.

   
   |Key parameters |Configuration instructions |
   |---|---|
   |Private network |Ensure that the VPC configured in the network information remains consistent with the VPC used for mounting storage in LAS later. |
   |Permission group |Select the default permission group. |
   |Root directory of the access point |Enter "/" (to restrict access to files under a specific directory, enter the specific directory). |
   


<span id="db0eaac9"></span>
## Mount NAS

You can select "Mount NAS" in the "Storage path mount" section of the development machine or task, and configure the relevant parameters. Key configuration points are described as follows.


1. Configure the "Storage path mount" parameters for the development machine or task.

   
   |Parameters |Configuration instructions |
   |---|---|
   |File system name |Select the file system to be mounted from the dropdown list. |
   |File System Access Point |Select the created access point from the dropdown list. |
   |File system path |Select the file system path to be mounted. |
   |Mount path |Set the path for mounting the current storage in LAS. |
   

2. Configure the network information for the development machine or task.

   
   |Parameters |Configuration instructions \- FSX |
   |---|---|
   |Advanced network configuration/Network connection |* When mounting vePFS using the FSX method, ensure that the vePFS access point and LAS are in the same VPC and the same availability zone. That is, make sure the "Advanced network configuration" switch is turned on, and the private network is the same VPC as the one used for mounting vePFS above.<br><br>* The system will automatically preselect the corresponding VPC for you based on the configuration result of the vePFS mounted above. You can continue to select the security group for the VPC. |
   


<span id="3cbdced4"></span>
# Mount TOS

<span id="1b8a2a29"></span>
## Preparation


* Prepare access keys AK and SK with permissions to access TOS. To obtain: Log in to the BytePlus console, and create and manage your Access Key on the **Access Control** ＞ **API Access Key** page.

* Currently, only tasks based on the new exclusive queue (that is, the EMR Serverless exclusive queue) support mounting TOS using the FSX protocol. Before configuring TOS mounting with the FSX protocol on the LAS side, you need to complete the EMR Serverless queue storage network configuration on the EMR side.


<span id="f23e0f49"></span>
## Mount TOS

You can select "Mount NAS" in the "Storage path mount" section of the development machine or task, and configure the relevant parameters. Key configuration points are described as follows.


|Parameters |Configuration instructions |
|---|---|
|AK / SK |Enter the prepared AK and SK information, click "Connectivity test", and after completing the connectivity test, proceed with the configuration of subsequent parameters. |
|mount protocol |Select the mounting protocol. The following are currently supported:<br><br><br>* CSI (that is, the S3FS protocol).<br><br>* FSX: Currently, only tasks based on the new exclusive queue (that is, the EMR Serverless exclusive queue) support mounting TOS using the FSX protocol. Before configuring TOS mounting on the LAS side, you need to complete the EMR Serverless queue storage network configuration on the EMR side. |
|Source address |Select the TOS bucket path to be mounted. |
|Mount path |Set the path for mounting in LAS. |
