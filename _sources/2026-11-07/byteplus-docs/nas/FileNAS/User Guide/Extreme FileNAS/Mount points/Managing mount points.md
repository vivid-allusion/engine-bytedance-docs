---
title: "Managing mount points"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Managing-mount-points"
---

This topic introduces the steps to create a mount point.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

The mount point is the entry point for an ECS instance to access a file system. Multiple mount points can be created for a file system, and the same mount point can also be mounted by multiple nodes simultaneously, sharing the access permissions of the file system.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

The file system has been created. For specific steps, please refer to [Creating a file system](https://docs.byteplus.com/docs/nas/Creating-a-file-system).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Only one mount target can be created in the same VPC. If you need to create multiple mount targets, you will need to create a VPC that matches the number of mount targets. For detailed steps, please refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top navigation bar, select the region where the target file system is located.

3. On the left navigation bar, select **File System** \> **File System List**, and on the **File System List** page, click the name of the file system for which you want to create a mount target.

4. On the file **Overview** page, click **Mount Target** tab, click **Create Mount Targets**.

5. In the pop\-up dialog box, set the following parameters.

   
   |**Parameters** |**Description** |
   |---|---|
   |Name of Mount Target |Set the mount point name. The naming convention is as follows:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length should be between 1 and 128 characters. |
   |Private network |Choose the same VPC network as the file system and ECS instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only one mount target can be created within the same file system in a VPC network.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A mount target can be used by different ECS instances under the same VPC.</div><br> |
   |Subnet |Select the subnet under the VPC network.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For optimal performance experience, it is recommended to have the file system, ECS instances, and subnets all in the same availability zone.</div><br> |
   |Permission Group |Select the corresponding permission group.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you create a file system, the console automatically creates a default permission group that allows any IP address within the same VPC network to access the file system through the mount target. If you need to set permission groups based on business requirements, please refer to <a href="https://docs.byteplus.com/docs/nas/Managing-permission-groups">Managing permission groups</a>.</div><br> |
   

6. After setting up, click **Create**.

   Creating a mount point may take some time, please be patient.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the mounting point is created, the following ports will be opened for accessing NFS services:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">2049: Access NFS service.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">4001: Access NLM service.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">4002: Access Mount service.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">111: Access RPC bind service.   </div>
