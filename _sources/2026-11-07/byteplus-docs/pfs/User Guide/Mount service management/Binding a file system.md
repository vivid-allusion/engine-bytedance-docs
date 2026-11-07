---
title: "Binding a file system"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Binding-a-file-system"
---

After creating a mount service, the mount service cluster exists independently and can be bound to one or more PFS file systems. Once the binding is completed, the compute nodes in the mount service cluster can access and store data.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


|Limitations |Description |
|---|---|
|Quantity limit |* A single PFS instance can be bound to a maximum of 5 mount services, and a single mount service can be bound to a maximum of 10 PFS instances.<br><br>* The same account in the same region can create up to 2 PFS instances. |
|PFS instance |* If your PFS instance needs to bind multiple mount services, all mount services must be in the same VPC.<br><br>* For optimal performance experience, it is recommended to have the PFS instance and the mount service in the same availability zone.<br><br>* A mounting service does not support multiple instances of SmartCalc version accessing through RDMA.<br><br>* Binding operations cannot be performed when the instance is in other states such as expansion or deletion.<br><br>* When performing instance binding operations, all nodes in the service cluster must be in the active state and the key file must not be damaged, otherwise the binding operation cannot be executed. |
|Mounting service |After creating the mount service, the system will automatically create 3 ECS instances to manage the client cluster. Please do not modify the initial password of the management node and ensure that the instances can log in normally. |


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region where the target file system is located.

3. Select **File System** \> **Mount Service** in the left navigation bar, and click **Binding storage instance**.

4. Set the following parameters in the pop\-up dialog box.

   
   |Parameters |Description |
   |---|---|
   |File System |Select the file system ID that needs to be bound from the drop\-down list. |
   |File System |(Optional) Set the default mount directory for the PFS file system. If not specified, it defaults to the file system ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">If you need to set a custom mount path, the parent directory must be an existing directory and the subdirectory must not be created.</div><br> |
   

5. After the settings are completed, click **OK**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It takes some time to mount the service and bind the instance. Please be patient and wait.   </div>
