---
title: "Mount FileNAS"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Mount_FileNAS"
---

FaaS supports mounting NAS, allowing data to be stored in [FileNAS](https://docs.byteplus.com/en/docs/nas/What-is-FileNAS). This article introduces how to mount NAS.

<span id="background-information"></span>
## Background information

FaaS seamlessly integrates with NAS, supporting the configuration of NAS for functions, including NAS filesystem, mount points, remote directories, local directories, and more. After configuration, functions can manage the remote NAS file system by accessing the local directory corresponding to the NAS mount point. Benefits of using NAS file mounting with FaaS include:


* Allows FaaS temporary files to be persisted to NAS, with temporary file size not limited by local disk space.

* Multiple functions can share a single NAS, enabling file sharing.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Data storage costs incurred by using NAS are charged by the NAS service; for specific charges, refer to <a href="https://docs.byteplus.com/en/docs/nas/Billing-overview">NAS Billing</a>.</div>


<span id="prerequisites"></span>
## Prerequisites


* Virtual Private Cloud (VPC)

   * BytePlus Virtual Private Cloud has been activated.

   * VPC, subnets, and security groups have been created in the deployment region of the function. For detailed actions, refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC), [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet), [Creating a security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

* NAS

   * NAS has been activated.

   * A NAS file system has been created in the deployment region of the function. For detailed actions, refer to [Creating a file system](https://docs.byteplus.com/en/docs/nas/Creating-a-file-system).

   * A mount point has been created in the target VPC. For detailed operations, refer to [Mounting a file system](https://docs.byteplus.com/en/docs/nas/Mounting-a-file-system).


<span id="usage-limit"></span>
## Usage limit


* NAS currently only supports adding mount points in the VPC. The function must enable VPC access and configure the VPC network that matches the mount point.

* A function can configure up to 10 NAS file systems.

* When the same function configures multiple NAS file systems, added file systems and remote directories can be duplicated, but local directories cannot be duplicated.

* If a function mounts both NAS and TOS, the local directories set for NAS and TOS mount points must not be duplicated.

* The default user and group for the NAS file directories mounted by the function cannot be modified.

   * For non\-native functions: UserID = 1000; GroupID = 1000.

   * For native functions: UserID = root; GroupID = root.


<span id="procedures"></span>
## Procedures


1. Support configuring NAS file systems in the following two ways:

   * Function not created

      When creating a function, in the **Advanced Configuration** area, enable VPC access and then configure NAS mounting. For detailed steps on creating a function, refer to [Function creation method selection](https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection).

   * Function created

      1. Log in to the [FaaS Control Console](https://console.byteplus.com/vefaas), and in the top navigation bar, select the region your business is located in.

      2. In the function list, click the target function name to enter the **Function Configuration** page.

      3. In the Function Configuration page, enable VPC network and configure NAS mounting.

2. Configure the VPC network and NAS mounting parameters as required, and save after configuration.

   
   |Parameter |Description |
   |---|---|
   |VPC access |Enable the VPC access feature, and configure the target Virtual Private Cloud, subnet, and security group.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The VPC configured for the function must be consistent with the VPC of the NAS mount point; subnets and availability zones are not mandatory. To achieve optimal performance experience, it is recommended that the subnet of the NAS mount point and the subnet of the function VPC be in the same availability zone.</div><br> |
   |NAS mounting |Enable the NAS mounting feature and add the information of the NAS file system to be mounted. Click`+`Add a file system, supporting up to 10 additions. The configuration for each NAS file system is as follows:<br><br><br>* **File system**: Select the NAS file system to be mounted, supporting **express\-type NAS file system** and **capacity\-type NAS file system**.<br><br>* **Mount point**: Select a NAS mount point that matches the Virtual Private Cloud configured for the current function.<br><br>* **Remote directory**: Configure the directory of the NAS file system that the function needs to access. Remote directory must start with`/`beginning. If the directory you configured does not exist on the remote NAS, FaaS will automatically create the directory for you.<br><br>* **Local directory**: Configures the local directory in the function runtime environment. The local directory must start with`/`"/opt/", please do not enter `/tmp`, `/opt/bytefaas`, `/opt/tiger/bytefaas/binary`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Combining remote and local directories allows mapping from a specific directory in the NAS file system to a local file system directory. For example: If the local directory is <code>/localPath</code> and the remote directory is <code>/demo</code>, the function can access the remote directory of the NAS mount point <Mount Point Address\>:/<fsid\>/demo by accessing the local directory /localPath.<code><Mount Point Address>:/<fsid>/demo by accessing the local directory /localPath</code>.</div><br> |
   


<span id="related-operation"></span>
## Related Operation


* **View the mounted NAS information**

   On the function configuration tab, select the NAS storage configuration card, and click the jump icon next to the name to quickly navigate to the NAS console to view detailed information about the current NAS file system.

* **View the monitoring indicators of NAS**

   On the function configuration tab, select the NAS storage configuration card and click the monitoring icon to quickly navigate to the NAS console to view the monitoring indicators of the current NAS file system.


<span id="what-to-do-next"></span>
## What to do next

Storage configuration needs to release the function to take effect. For specific actions, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).
