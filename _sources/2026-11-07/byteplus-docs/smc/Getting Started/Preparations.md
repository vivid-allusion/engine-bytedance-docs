---
title: "Preparations"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Preparations"
---

When you use SMC to migrate a source server, you need to prepare a platform account, create a target instance, authorize SMC to access services such as ECS and EBS, and obtain an Access Key.

<span id=".5YeG5aSH54Gr5bGx5byV5pOO6LSm5Y-3"></span>
## Prepare a platform account

Prepare a platform account according to the instructions and guidelines.


* If you use the SMC service through a sub\-account, you need to configure the SMCFullAccess permission for the sub\-account, and the activity details can be viewed to [Creating a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you want to use <a href="https://docs.byteplus.com/en/docs/smc/One-click_import_from_the_console">one\-click import of migration source in the console</a> as an IAM user, attach the <strong>SMCBatchMigrationAccess</strong> policy to the IAM user.   </div>
   

* Enable the [snapshot](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots) service for the account.

* Make sure that the platform account has sufficient quotas for custom images, EIPs, security groups, and other resources in the target region to avoid migration failure due to inability to create temporary resources during the migration process. For details, see [Evaluating the quantity of cloud resources used by migration tasks](https://docs.byteplus.com/en/docs/smc/Evaluate-the-number-of-cloud-resources-used-by-Migration-Jobs).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">SMC is a free service, but the migration process involves a small amount of cloud resource charges. For more information, see <a href="https://docs.byteplus.com/en/docs/smc/Billing">Billing</a>.   </div>
   

<span id=".5o6I5p2DU01D6K6_6Zeu5pyN5Yqh6LWE5rqQ"></span>
## Authorize SMC to access service resources

Before you use SMC for the first time, you need to log in to the [SMC console](https://console.byteplus.com/ecs/source) and follow the instructions to authorize SMC to access your service resources, such as volumes, VPC, and ECS instances, on the platform.

<span id=".5YeG5aSH55uu5qCH5a6e5L6L"></span>
## Prepare the target instance

To migrate the source server to a platform ECS instance, create a target instance or migration template that meets the following requirements in advance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">During the migration, the platform will reinstall the system of the target instance. We recommend that you <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">back up data of the target instance</a> in advance.</div>


* <div data-tips="true" data-tips-type="tip">The migration template feature is currently in Beta. If you need a trial, please contact the account manager to apply.</div>


1. Learn the specifications of the target instance.

   
   |Configuration item |Description |
   |---|---|
   |Instance |Migration to Elastic Bare Metal instances is not supported. For details of instance types, refer to [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). |
   |Billing method |Pay\-as\-you\-go or Subscription ECS instances can be used as target instances for migration. For details of each billing method, please check the [Billing methods](https://docs.byteplus.com/en/docs/ecs/Billing-methods). |
   |Operating system |The operating system type must be consistent with that of the migration source.<br><br>For example, if the source server operating system is CentOS 7.9, the target instance must also use a Linux\-type image and cannot use a Windows\-type image. |
   |Volume |* The system volume and data volumes must be ESSDs or Ultra Disks. Migration to instances equipped with PTSSDs is not supported. [Learn more](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).<br><br>* We recommend that the system volume capacity of the target instance be not less than that of the migration source. Otherwise, the data from the migration source may not be fully migrated to the target instance.<br><br>* The number of data volumes mounted to the target instance must be no less than that of the source server. The capacity of each data volume on the target instance must be no less than the capacity of its corresponding data disk on the source server. Otherwise, the data on the data disks of the source server cannot be migrated to the target instance.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When migrating, SMC sorts the data volumes of the target instance and the data volumes of the source server by capacity, and migrates the data in order.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the volumes mounted to the existing instances do not meet the migration requirements, you can either mount new volumes or scale up the existing volumes. <a href="https://docs.byteplus.com/en/docs/ecs/Overview-of-volume-operations">Learn more</a>.</div><br> |
   |Network |* Before performing migration with different methods, you need to open the corresponding ports in the firewall. [Learn more](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).<br><br>   * Block replication method:<br><br>      * Migrate to Linux instances: ports `22` and `8080`.<br><br>      * Migrate to Windows instances: ports `5986` and `8080`.<br><br>   * File replication method:<br><br>      * Migrate to Linux instances: port `22`.<br><br>* Before performing migration with different networks, you need to complete the corresponding network configurations.<br><br>   * For Internet\-based migration: The target instance must be [associated with an EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).<br><br>   * For intranet\-based migration: You need to connect the migration source and the target instance VPC through a VPN gateway or Direct Connect, configure a proxy server, and complete other related operations in advance. [Learn more](https://docs.byteplus.com/en/docs/smc/Server-Migration-Task#.5pON5L2c5q2l6aqk). |
   

2. Create [target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) or[migration template](https://docs.byteplus.com/en/docs/smc/Create_and_manage_migration_templates).


<span id=".6YWN572u6L-B56e75rqQ"></span>
## Configure the migration source

<span id=".5pyN5Yqh5Zmo6L-B56e7"></span>
### Server migration

To migrate the source server to a platform ECS instance or custom image, make sure that the source server meets the following requirements and that all relevant configurations are completed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">During the migration, data replication will occur, which may result in the risk of data loss in the system disk or data disks. We recommend that you back up data of the source server in advance.</div>


* <div data-tips="true" data-tips-type="tip">To use the "block replication" migration method, we recommend that the transfer rate of the source server be greater than 50 Mbps.</div>




|Configuration item |Description |
|---|---|
|Operating system |For details, see [Operating system compatibility](https://docs.byteplus.com/en/docs/smc/Actions_System_Compatibility_Notes#.5pyN5Yqh5Zmo6L-B56e7). |
|System architecture |Only x86_64 architecture is supported. |
|File system |* The file replication migration method only supports SWAP, Ext2, Ext3, Ext4, FAT, MINIX, MSDOS, VFAT, XFS, or Btrfs file systems.<br><br>* The block replication migration method does not restrict the file system type. |
|Disk |* Up to 14 data disks are supported.<br><br>* When the source server is migrated to an ECS instance image, make sure that:<br><br>   * The system disk capacity does not exceed 2048 GiB.<br><br>   * The total disk capacity does not exceed 8 TiB. |
|Software configuration |The rsync tool 3.1.0 or later must be installed. If it is not installed or the version is too low, go to the [rsync official website](https://rsync.samba.org/) to download and install it.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Installation is required only when the migration source uses the Linux operating system.</div><br> |
|System configuration |* For Linux operating systems, [disable SELinux](https://docs.byteplus.com/en/docs/smc/Disable_SELinux).<br><br>* For Windows operating systems, [disable UAC](https://docs.byteplus.com/en/docs/smc/Disable-UAC). |
|Driver installation |Some instance types require using `root` permission to install Virtio drivers before they can operate normally. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo). |
|Network |* By default, firewalls allow outbound traffic on all ports. If your firewall does not have this configuration, open the required outbound ports in the firewall based on your selected migration method.<br><br>   * Block replication method:<br><br>      * Migrate to Linux instances: ports `22` and `8080`.<br><br>      * Migrate to Windows instances: ports `5986` and `8080`.<br><br>   * File replication method:<br><br>      * Migrate to Linux instances: port `22`.<br><br>* Before performing migration with different networks, you need to complete the corresponding network configurations.<br><br>   * For Internet\-based migration: The source server can access the public network as expected.<br><br>   * For intranet\-based migration: You need to connect the migration source and the target instance VPC through a VPN gateway or Direct Connect, configure a proxy server, and complete other related operations in advance. [Learn more](https://docs.byteplus.com/en/docs/smc/Server-Migration-Task#.5pON5L2c5q2l6aqk). |


<span id=".5pON5L2c57O757uf6L-B56e7"></span>
### Operating system migration

If you want to use the operating system migration feature to change the operating system of the ECS instance, please make sure that the instance meets the following requirements.


|Configuration item |Description |
|---|---|
|Migration source |Only platform ECS instances are supported. |
|Operating system |For details, see [Operating system compatibility](https://docs.byteplus.com/en/docs/smc/Actions_System_Compatibility_Notes#.5pON5L2c57O757uf6L-B56e7). |
|Memory |No less than 300 MiB. |
|Volume |Volume capacity requirements:<br><br><br>* /usr directory ≥ 250 MiB.<br><br>* /var directory ≥ 1.5 GiB.<br><br>* /boot directory ≥ 50 MiB. |
|Software configuration |* yum is installed and can run as expected.<br><br>* python3 is installed and can run as expected. When you execute the `python -V` command, make sure that the Python version in the command output is `python 2.x`.<br><br>* The graphical user interface is not installed. |


<span id=".6I635Y-W6K6_6Zeu5a-G6ZKl77yIQWNjZXNzIEtlee-8iQ=="></span>
## Obtain an Access Key

You can go to the platform console to obtain an Access Key. SMC will use the Access Key ID (AK) and Secret Access Key (SK) contained in the Access Key to verify the identity of the migration tool Agent. For more information, see [About access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-keys).
