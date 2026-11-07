---
title: "Check item description"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Detect_item_description"
---

This topic summarizes and describes the check items currently supported by the image detection feature, along with the recommended fixes for each item.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If an image fails a check item, the cause of failure can be found in the <code>RiskCode</code> response parameter of the <a href="https://docs.byteplus.com/en/docs/ecs/DescribeImages">DescribeImages</a> operation. If the response parameter is empty for a check item, the image passes the check.</div>



<Tabs>
<Tab zoneid="qXl9gKYZjM" title="Linux check items">
<TabTitle>Linux check items</TabTitle>


|**Check item** |**Description** |**Check result** |||Repair method ||
|---|---|---|---|---|---|---|
|||**Result** |**RiskLevel** |**RiskCode** |**One\-click repair** |**Manual repair** |
|Platform |Check the type of the image. |Example: CentOS |\- |\- |\- |\- |
|||UnKnown: The operating system type is unknown. |High: Fixing is strongly recommended. |Platform.UnKnow: The operating system type is unknown. |Not supported |\- |
|PlatformVersion |Check the version of the image. |Example: 7.9 |\- |\- |\- |\- |
|||UnKnown: The operating system version is unknown. |High: Fixing is strongly recommended. |PlatformVersion.Unknown: The operating system version is unknown. |Not supported |\- |
|KernelVersion |Check the kernel version of the image. |Example: 3.10.0\-1160.80.1.el7.x86_64 |\- |\- |\- |\- |
|BootMode |Check the boot mode of the image. |Example: UEFI |\- |\- |\- |\- |
|RtcTime\-Mode |Check the time zone of the hardware clock of the image. |Example: UTC |\- |\- |\- |\- |
|Architecture |Check the image architecture information. |Example: AMD64 |\- |\- |\- |\- |
|||UnSupported: The check is not supported. |Medium: Optimization is recommended. |Architecture.NotSupported: Images in the ARM architecture cannot be checked. |Not supported |\- |
|Image |Check whether partitions and the root file system exist in the image.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the check report does not contain the result for this check item, your image passes the check.</div><br> |UnCorrected: No partitions are found. |High: Fixing is strongly recommended. |Image.NoPartition: No partition is found in the image. |Not supported |The image is invalid, and no bootable file system partitions are located. Please follow the [instructions for creating a Linux image ](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images)to recreate the image. |
|||||Image.NoRootFileSystem: Root file system is not found in the image. |Not supported |The image is invalid, and the root file system cannot be located. Please follow the [instructions for creating a Linux image](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images) to recreate the image. |
|OFED |Check whether the RDMA network interface driver is installed in the image. |Example: OFED\-internal\-23.10\-1.1.9 |\- |\- |\- |\- |
|||UnAvailable: The RDMA network interface driver is not installed. |\- |\- |Not supported |If the image is used to create an instance mounted with an RDMA network interface, install the RDMA network interface driver. |
|DOCA |Check whether the NVIDIA DOCA framework is installed in the image. |Example: 535.161.08 |\- |\- |\- |\- |
|||UnAvailable: The DOCA framework is not installed. |\- |\- |Not supported |If the image is used to create an HPC\-optimized instance, install DOCA. |
|NVIDIA |Check whether the NVIDIA driver is installed in the image. |Example: 2.5.0\-0.0.1 |\- |\- |\- |\- |
|||UnAvailable: The NVIDIA driver is not installed. |\- |\- |Not supported |If the image is used to create a GPU Compute Service (GPU) instance, [install the NVIDIA driver](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-drivers). |
|Virtio |Check whether the Virtio driver is installed. |Supported: No risks are found. |\- |\- |\- |\- |
|||UnSupported: The Virtio driver is not installed. |High: Fixing is strongly recommended. |Kernel.NotFound: The kernel file is not found, which may cause system startup exceptions. |Supported |If the Virtio driver is not installed, install the Virtio driver according to the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlv6amx5Yqo). |
|||||Virtio.NotInstalled: The Virtio driver is not installed. As a result, the instance may not work as expected. |Supported ||
|||||KernelConfig.NotFound: The kernel configuration file is not found, which may cause system startup exceptions. |Supported ||
|Virtio1.1 |Check whether the Virtio 1.1 driver is installed. |Supported: No risks are found. |\- |\- |\- |\- |
|||UnSupported: The Virtio 1.1 driver is not installed. |High: Fixing is strongly recommended. |Virtio110.NotInstalled: The Virtio1.1 driver is not installed. If the kernel version of your image is higher than 5.4.x, you do not need to install Virtio1.1. |Supported |If the Virtio 1.1 driver is not installed, install the Virtio 1.1 driver according to the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo). |
|Cloud\-init |Check whether Cloud\-init is correctly installed or configured. |Available: No risks are found. |\- |\- |\- |\- |
|||UnAvailable: Cloud\-init is not installed or configured correctly. |High: Fixing is strongly recommended. |CloudInit.LocalServiceNotFound: The Cloud\-init service is not installed, which may cause system initialization failures. |Supported |Install and configure Cloud\-init following the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.56ys5Zub5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFQ2xvdWQtaW5pdA==). |
|||||CloudInit.NotInstalled: The Cloud\-init service is not installed, which may cause system initialization failures. |Supported ||
|||||CloudInit.ServiceNotFound: The Cloud\-init service is not installed, which may cause system initialization failures. |Supported ||
|||||CloudInit.ConfigServiceNotFound: The Cloud\-init service is not installed, which may cause system initialization failures. |Supported ||
|||||CloudInit.FinalServiceNotFound: The Cloud\-init service is not installed, which may cause system initialization failures. |Supported ||
|||||DataSource.NotExisted: The Cloud\-init data source configuration is missing, which may cause system initialization failures. |Supported ||
|||||DataSource.NotCorrected: The Cloud\-init data source is incorrect, which may cause system initialization failures. |Supported ||
|/etc/shadow |Check whether the /etc/shadow file meets the requirements. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The /etc/shadow file is unavailable. |High: Fixing is strongly recommended. |Shadow.NotExisted: The password file does not exist. You cannot reset the password in the console. |Supported |Retain the /etc/shadow file. |
|||||Shadow.NotWritten: No write permissions on the password file are granted. You cannot reset the password in the console. |Supported |Do not use the chattr command to lock files. |
|Passwd/Chpasswd |Check whether the passwd and chpasswd commands exist. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The passwd and chpasswd commands are not found. |High: Fixing is strongly recommended. |ChangPasswordCommand.NotExisted: The passwd/chpasswd command does not exist. You cannot reset the password in the console. |Not supported |Retain the passwd and chpasswd commands. |
|/etc/fstab |Check whether the /etc/fstab file configuration is correct. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The /etc/fstab file configuration is incorrect. |High: Fixing is strongly recommended. |RootPartitionMounted.NotCorrected: Improper mounting of the root partition during system startup does not comply with specifications and may result in system startup failures. |Supported |Check the configuration of the /etc/fstab file. |
|||||DeviceMounted.NotCorrected: Device mounting during startup is not performed correctly, which may cause system startup exceptions. |Supported ||
|||||DataVolumeMounted.NotCorrected: A data volume is mounted by using the /etc/fstab configuration file, which may cause system startup failures when a non\-whole image is used. |Supported ||
|Blk\-None |Check whether Blk\-None is installed. This tool is used to prevent IO hang issues that occasionally occur when images with low kernel versions are used to create third\-generation instances. |Available: No risks are found. |\- |\- |\- |\- |
|||UnAvailable: Blk\-None is not installed. |High: Fixing is strongly recommended. |BlkNone.NotInstalled: The blk\-none tool is not installed. Instances of certain types may experience IO hang issues. If the kernel version of your image is higher than 4.19.x, you do not need to install the blk\-none tool. |Supported |Install the Blk_None tool according to the instructions in the [solution](https://docs.byteplus.com/en/docs/ecs/blk-none#.6Kej5Yaz5pa55qGI). |
|NetworkDhcpSetting |Check whether the Dynamic Host Configuration Protocol (DHCP) service is enabled on the eth0 network interface in the image. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The DHCP service is not enabled. |High: Fixing is strongly recommended. |NetworkDhcpSetting.NotCorrected: The network in the image is set to static mode, which causes a network configuration exception after the instance starts. |Not supported |Enable the DHCP service according to the instructions in the [solution](https://docs.byteplus.com/en/docs/ecs/Start-SHCP-Service-in-Linux-image). |
|SELinux |Check the SELinux service status of the image. We recommend that you do not enable the SELinux service on ECS instances because the service may cause system startup exceptions. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The SELinux service is enabled in the image. |High: Fixing is strongly recommended. |SELinuxConfig.NotCorrected: The SELinux service is enabled in the image. |Not supported |Disable the SELinux service according to the guidance in the [solution](https://docs.byteplus.com/en/docs/smc/Disable_SELinux). |
|DHCPClient |Check whether the image has DHCPClient correctly installed. |Available: No risks are found. |\- |\- |\- |\- |
|||Unavailable: DHCPClient is not installed properly. |High: Fixing is strongly recommended. |DHCPClient.NotInstalled: DHCPClient is not installed in the image. |Supported |Please install DHCPClient correctly. |
|Reset\-Authentication |Check whether the reset\-authentication plugin is installed correctly. |Available: No risks are found. |\- |\- |\- |\- |
|||UnAvailable: The reset\-authentication plugin is not installed correctly. |Medium: Optimization is recommended. |ResetAuthentication.NotInstalled: The reset\-authentication plugin is not installed. You cannot use the features for resetting the password, changing the hostname, or associating/disassociating a key. |Supported |Install the reset\-authentication plug\-in according to the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in). |
|o11yagent |Check whether the O11yAgent collection plugin is installed correctly. |Available: No risks are found. |\- |\- |\- |\- |
|||UnAvailable: The O11yAgent plugin is not installed correctly |Medium: Optimization is recommended. |o11yagent.NotInstalled: The O11yAgent plugin is not installed |Not supported |Based on the guidance in the [solution](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console), install the O11yAgent plugin. |
|Run\-Command\-Agent |Check whether the Cloud assistant plugin is installed in the image. |Available: No risks are found. |\- |\- |\- |\- |
|||UnAvailable: The Cloud assistant plugin is not installed correctly. |Medium: Optimization is recommended. |RunCommandAgent.NotInstalled: The Cloud assistant plugin is not installed. |Not supported |Install the Cloud assistant plugin according to the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client). |
|AutoResizeFS |Check whether the image supports automatic scaling up of the root partition. |Supported: No risks are found. |\- |\- |\- |\- |
|||UnSupported: The CloudMonitor plugin is not installed correctly. |Medium: Optimization is recommended. |AutoResizeFS.UnSupported: The image does not support automatic scaling up of the root partition. |Not supported |The Linux image uses Cloud\-init to automatically expand the root partition. Install the expansion tool and fix the Cloud\-init configuration according to the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/After_expanding_Volumes_partition_cannot_autom). |





</Tab>
<Tab zoneid="Q3c1w4KSZ8" title="Windows Server check items">
<TabTitle>Windows Server check items</TabTitle>


|**Check item** |**Description** |**Check result** |||Repair method ||
|---|---|---|---|---|---|---|
|||**Result** |**RiskLevel** |**RiskCode** |**One\-click repair** |**Manual repair** |
|Platform |Check the type of the image. |Example: Windows Server |\- |\- |\- |\- |
|||Unknown: The operating system type is unknown. |High: Fixing is strongly recommended. |Platform.Unknow: The operating system type is unknown. |Not supported |\- |
|PlatformVersion |Check the version of the image. |Example: Windows Server 2022 Datacenter |\- |\- |\- |\- |
|||UnKnown: The operating system version is unknown. |High: Fixing is strongly recommended. |PlatformVersion.Unknown: The operating system version is unknown. |Not supported |\- |
|Architecture |Check the image architecture information. |Example: AMD64 |\- |\- |\- |\- |
|||UnSupported: The check is not supported. |Medium: Optimization is recommended. |Architecture.NotSupported: Images in the ARM architecture cannot be checked. |Not supported |\- |
|||Unknown: Unknown image architecture |Medium: Optimization is recommended. |Architecture.UnKnown: Unknown architecture. |Not supported |\- |
|BootMode |Check the boot mode of the image. |Example: BIOS |\- |\- |\- |\- |
|||UnKnown |High: Fixing is strongly recommended. |BootMode.UnKnown: Unknown boot mode. |Not supported |This issue is usually caused by corruption of the image boot partition. We recommend that you recreate an image. |
|NetkvmVersion |Check the Netkvm driver version. |Example: 100.93.104.24000 |\- |\- |\- |\- |
|||UnCorrected: The Netkvm driver version is incorrect. |High: Fixing is strongly recommended. |NetkvmVersion.NotFound: The Netkvm driver is not found. |Supported |Install the Virtio driver according to the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5LqU5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFVmlydGlv6amx5Yqo). |
|ViostorVersion |Check the Viostor driver version. |Example: 100.93.104.24000 |\- |\- |\- |\- |
|||UnCorrected: The Viostor driver version is incorrect. |High: Fixing is strongly recommended. |ViostorVersion.NotFound: The Viostor driver is not found. |Supported |Install the Virtio driver according to the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5LqU5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFVmlydGlv6amx5Yqo). |
|BCD |Check whether the BCD (Boot Configuration Data) of the image is correct. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The BCD configuration is incorrect. |High: Fixing is strongly recommended. |BCD.NoBootEntry: No boot entry is found. |Supported |Please configure BCD correctly. |
||||High: Fixing is strongly recommended. |BCD.UnknownBootEntry: Unknown boot entries exist. |Supported ||
||||Medium: Optimization is recommended. |BCD.MultiBootEntry: Multiple boot entries exist. |Not supported ||
|Disk |Check whether the image can be mounted to the rescue machine and similar situations. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The image cannot be mounted to the rescue machine. |High: Fixing is strongly recommended. |Disk.SystemVolumeNumberNotFound: Image system partition is not found. |Not supported |There is a problem with the configuration of the image file. Please recreate an image. |
|||||Disk.DriveLetterAssignmentFailed: Disk mounting exception. |Not supported ||
|Registry |Check whether the registry file configuration of the image is correct. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The registry file is incorrect. |High: Fixing is strongly recommended. |Registry.NotCorrected: The registry configuration is incorrect. |Not supported |Use the correct registry file. |
|Cloudbase\-init |Check whether Cloudbase\-init is installed in the image. |Available: No risks are found. |\- |\- |\- |\- |
|||UnAvailable: Cloudbase\-init is not installed correctly. |High: Fixing is strongly recommended. |Cloudbase\-init.NotFound: The Cloudbase\-init service is not installed, which may cause system initialization failures. |Supported |Install Cloudbase\-init according to the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5LiJ5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFQ2xvdWRiYXNlLWluaXQ=). |
|Patch |Check whether the image has all required patches installed correctly. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The patches in the image are incomplete or incorrect. |High: Fixing is strongly recommended. |Patch.NotCorrected: The patch in the image is incomplete or incorrect, which may cause system startup exceptions. |Not supported |Please check the patch installation status in the image, refer to [the solution](https://docs.byteplus.com/en/docs/ecs/Install_uninstall_system_patches) guide, install missing patches, and uninstall erroneous patches.<br><br><br>* List of error patches: KB5009624, KB5009595, KB5009546, KB5009557, KB5009555, KB5014738, KB5014702, KB5014692, and KB5014678.<br><br>* Required patch: You need to install the KB3033929 patch for the Microsoft Windows Server 2008 R2 64\-bit operating system. |
|Reset\-Authentication |Check whether the reset\-authentication plugin is installed correctly. |Available: No risks are found. |\- |\- |\- |\- |
|||UnAvailable: The reset\-authentication plugin is not installed correctly. |High: Fixing is strongly recommended. |Reset\-Authentication.NotFound: The reset\-authentication plug\-in is not installed. |Supported |Install the reset\-authentication plug\-in according to the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in). |
|Sysprep |Check whether the Sysprep process has been completed during the image creation process. |Finished: No risks are found. |\- |\- |\- |\- |
|||Unfinished: The Sysprep process is not completed. |Medium: Optimization is recommended. |Sysprep.Unfinished: The Sysprep process is not completed during image creation, which may cause system startup exceptions. |Not supported |Recreate the image, and do not interrupt the Sysprep process during image creation. |
|Update |Check whether Windows updates are completed during the image creation process. |Finished: No risks are found. |\- |\- |\- |\- |
|||Unfinished: Windows updates are not completed. |Medium: Optimization is recommended. |Update.Unfinished: Windows updates are not completed during image creation, which may cause system startup exceptions. |Not supported |Recreate the image, and do not interrupt the system update process during image creation. |
|Xen |Check whether the Xen driver is installed in the image. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The Xen driver is installed. |Medium: Optimization is recommended. |Xen.NotCorrected: The Xen driver exists, which may cause system startup exceptions. |Not supported |Disable the Xen driver according to the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/Windows_Server_Operating_System#.56aB55SoWGVu6amx5Yqo). |
|O11yAgent |Check whether the O11yAgent collection plugin is installed correctly. |Available: No risks are found. |\- |\- |\- |\- |
|||UnAvailable: The O11yAgent plugin is not installed correctly |Medium: Optimization is recommended. |o11yagent.NotInstalled: The O11yAgent plugin is not installed |Not supported |Based on the guidance in the [solution](https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console), install the O11yAgent plugin. |
|Services |Check whether the service configuration in the image is correct. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The service configuration in the image is incorrect. |Medium: Optimization is recommended. |Services.NotCorrected: The service configuration in the image is incorrect, which may result in exceptions, such as driver update exceptions. |Not supported |Reconfigure the service and allow driver installation according to the instructions in the [solution](https://docs.byteplus.com/en/docs/ecs/Windows_Server_Operating_System#.5YWB6K645a6J6KOF6amx5Yqo). |
|DesktopConfig |Check whether the desktop.ini (desktop configuration) file in the image is correct. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: The desktop configuration file in the image is incorrect. |Medium: Optimization is recommended. |DesktopConfig.NotCorrected: The desktop configuration file is missing, which causes the desktop configuration to become invalid. |Not supported |Correctly configure the desktop.ini file. |
|Ntp |Check whether the NTP service of the image is correctly configured. |Corrected: No risks are found. |\- |\- |\- |\- |
|||UnCorrected: NTP service provided by BytePlus is not used. |Medium: Optimization is recommended. |Ntp.ServiceNotConfigured: NTP service configuration is not found. |Not supported |It is recommended to use BytePlus NTP service following the guidance in the [solution](https://docs.byteplus.com/en/docs/ecs/Configuring-the-NTP-service-for-Windows). |
||||Medium: Optimization is recommended. |Ntp.ServerNotSet: The NTP service has no upstream synchronization server configured. |Not supported ||
||||Medium: Optimization is recommended. |Ntp.Disabled: The NTP service is disabled. |Not supported ||
||||Medium: Optimization is recommended. |Ntp.NotVolcEngine: The upstream NTP synchronization server is not a BytePlus server. |Supported ||
|TimeZone |Check whether the time zone configuration in the image is correct. |Example: Asia/Shanghai |\- |\- |\- |\- |
|||UnKnown |Medium: Optimization is recommended. |TimeZone.NotConfigured: Time zone configuration is not found. |Not supported |Please configure the time zone correctly. |





</Tab>
</Tabs>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The detection item feature for the Cloud Monitor plugin (Cloud\-Monitor\-Agent) has been discontinued. We recommend that you install the next\-generation monitoring plugin (O11yAgent) provided by Cloud Monitor. O11yAgent operates from within the ECS instance to provide deeper and more accurate visibility into its runtime status. <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Overview-1">Learn more</a>.</div>
