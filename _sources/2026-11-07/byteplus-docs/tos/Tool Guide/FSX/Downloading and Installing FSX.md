---
title: "Downloading and Installing FSX"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install-fsx"
---

This article provides information on precautions, installation steps, and other related information for installing FSX.

<span id="10ba65d2"></span>
## Precautions


* For the operating systems supported by the FSX client, please refer to [Operating environment](https://docs.byteplus.com/docs/tos/Overview#e82382a8). If your operating system is not included in the supported list, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245) to contact the technical team.

* The FSX client will be installed in the `/opt/fsx` directory. Please ensure that the available disk space in this installation directory exceeds 1GB; otherwise, installation may fail or the client may not function properly.

* When installing the FSX client, the client configuration files will be stored in the `/opt/tmp/fsx` directory. It is recommended to reserve at least 2 GiB of disk space. Log files will be stored in the `/var/log/fsx` directory, and it is also recommended to reserve at least 2 GiB of disk space. Please ensure that there are no directories with the same name in your system; otherwise, installation may fail or the system may not function properly.

* When mounting a bucket, it is recommended that you implement appropriate isolation measures for the bucket directory to prevent other services from deleting or writing to the mounted directory; otherwise, data inconsistency and other unexpected problems may occur.


<span id="27b24466"></span>
## Download FSX Client

Download the FSX client for Linux. The download address is as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The FSX client currently supports only the x86_64 and ARM64 architectures (with ARM64 currently supported only on ecs.c3bl series instances), and is currently not supported for use in Windows or macOS environments.</div>



|**System Architecture** |**Operating System** |**Tool Download Link** |**Tool Verification Address** |
|---|---|---|---|
|x86_64 |DEB\-based distribution (veLinux) |[fsx_amd64.deb](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx_amd64.deb) |[fsx_amd64.deb.sha256sum](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx_amd64.deb.sha256sum) |
||RPM\-based distribution (veLinux CentOS Compatible) |[fsx_x86_64.rpm](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx_x86_64.rpm) |[fsx_x86_64.rpm.sha256sum](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx_x86_64.rpm.sha256sum) |
||Other Operating Systems |[fsx.tar.gz](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx.tar.gz) |[fsx.tar.gz.sha256sum](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx.tar.gz.sha256sum) |
|ARM64 |DEB\-based distribution (veLinux) |[fsx_arm64.deb](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx_arm64.deb) |[fsx_arm64.deb.sha256sum](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx_arm64.deb.sha256sum) |
||RPM\-based Distribution (veLinux CentOS Compatible) |[fsx_aarch64.rpm](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx_aarch64.rpm) |[fsx_aarch64.rpm.sha256sum](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx_aarch64.rpm.sha256sum) |
||Other Operating Systems |[fsx.tar.gz](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx.tar.gz) |[fsx.tar.gz.sha256sum](https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx.tar.gz.sha256sum) |


You can also execute the wget command to download the FSX client.


<Tabs>
<Tab zoneid="xRLvKvGgrr" title="x86_64 architecture">
<TabTitle>x86_64 architecture</TabTitle>

* DEB\-based distribution (veLinux)

   * Tools

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx_amd64.deb
      ```
      

   * Tool Verification File

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx_amd64.deb.sha256sum
      ```
      

* RPM\-based distribution (veLinux CentOS Compatible)

   * Tools

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx_x86_64.rpm
      ```
      

   * Tool Verification Address

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx_x86_64.rpm.sha256sum
      ```
      

* Other Operating Systems

   * Tools

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx.tar.gz
      ```
      

   * Tool Verification Address

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/amd64/fsx/latest/fsx.tar.gz.sha256sum
      ```
      


</Tab>
<Tab zoneid="hGd7YF0Ymi" title="ARM64 Architecture">
<TabTitle>ARM64 Architecture</TabTitle>

* DEB\-based distribution (veLinux)

   * Tools

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx_arm64.deb
      ```
      

   * Tool Verification File

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx_arm64.deb.sha256sum
      ```
      

* RPM\-based distribution (veLinux CentOS Compatible)

   * Tools

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx_aarch64.rpm
      ```
      

   * Tool Verification File

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx_aarch64.rpm.sha256sum
      ```
      

* Other Operating Systems

   * Tools

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx.tar.gz
      ```
      

   * Tool Verification File

      ```Bash
      wget https://m645b3e1bb36e-mrap.mrap.accesspoint.tos-global.volces.com/linux/arm64/fsx/latest/fsx.tar.gz.sha256sum
      ```
      


</Tab>
</Tabs>


<span id="18f7d510"></span>
## Installing the FSX Client

The FSX client supports multiple operating systems. Please select the appropriate installation method according to your operating system type. The following uses the x86_64 system architecture as an example:


<Tabs>
<Tab zoneid="gG7vZ3m8Ga" title="Deb-based distribution (veLinux)">
<TabTitle>Deb-based distribution (veLinux)</TabTitle>

1. Run the following command to install the client.

   ```Bash
   dpkg -i fsx_amd64.deb 
   ```
   

2. Run the following command to check the client version.

   ```Bash
   fsx -v
   ```
   

   The following version information indicates that the installation was successful.

   ```Bash
   Version: 1.2.3.592
   ```
   


</Tab>
<Tab zoneid="KRQofHYQZl" title="RPM-based Distribution (veLinux CentOS Compatible)">
<TabTitle>RPM-based Distribution (veLinux CentOS Compatible)</TabTitle>

1. Execute the following command to install the client.

   ```Bash
   rpm -ivh fsx_x86_64.rpm
   ```
   

2. Run the following command to check the client version.

   ```Bash
   fsx -v
   ```
   

   The following version information indicates that the installation was successful.

   ```Bash
   Version: 1.2.3.592
   ```
   


</Tab>
<Tab zoneid="yyJnXY5USA" title="Other Operating Systems">
<TabTitle>Other Operating Systems</TabTitle>

1. Execute the following command to create the installation directory for fsx.

   ```Bash
   mkdir -p /opt/fsx
   ```
   

2. Execute the following command to extract fsx.tar.gz to the `/opt/fsx` directory.

   ```Bash
   sudo tar -C /opt/fsx -xzf ./fsx.tar.gz
   ```
   

3. Execute the following command to enter the `/opt/fsx` directory, then install FSX.

   ```Bash
   cd /opt/fsx
   ```
   

   ```Bash
   sudo ./fsx -m install
   ```
   

4. Execute the following command to check the client version.

   ```Bash
   sudo fsx -v
   ```
   

   If the following version information is returned, it means the installation was successful.

   ```Bash
   Version: 1.2.3.592
   ```
   


</Tab>
</Tabs>


<span id="27a42498"></span>
## Upgrade FSX Client

Below, we use the x86_64 system architecture as an example to describe the steps for upgrading the FSX client.


<Tabs>
<Tab zoneid="PGmpIo8la7" title="Deb-based distribution (veLinux)">
<TabTitle>Deb-based distribution (veLinux)</TabTitle>

1. Execute the following command to upgrade the client.

   ```Bash
   dpkg -i fsx_amd64.deb
   ```
   

2. Confirm the upgrade status.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Compare the version of the running binary with the dpkg version. If the two version numbers are identical, the upgrade is successful. If the two version numbers do not match, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245">submit a ticket</a> to contact technical support.   </div>
   

   1. Execute the following command to check the version of the running binary.

      ```Bash
      fsx -v
      ```
      

      The following version information is returned.

      ```Bash
      Version: 1.2.3.592
      ```
      

   2. Execute the following command to check the dpkg \*\*\*\* version.

      ```Bash
      dpkg -l fsx
      ```
      

      The following version information is returned.

      ```Bash
      ||/ Name           Version      Architecture Description
      +++-==============-============-============-================================================================================
      ii  fsx        1.2.3.592    amd64        fsx branch: fsx/xxx_09b1043bb962e8bb10****a71cb41477b9ce****
      ```
      


</Tab>
<Tab zoneid="ttGN0r2Unp" title="RPM-based distribution (veLinux CentOS Compatible)">
<TabTitle>RPM-based distribution (veLinux CentOS Compatible)</TabTitle>

1. Execute the following command to upgrade the client.

   ```Bash
   rpm -Uvh fsx_x86_64.rpm
   ```
   

2. Confirm the upgrade status.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Check the running binary version and the dpkg version; if both version numbers are identical, the upgrade has been successful. If the two version numbers do not match, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245">submit a ticket</a> to contact technical support.   </div>
   

   1. Run the following command to check the version of the running binary.

      ```Bash
      fsx -v
      ```
      

      The following version information will be returned.

      ```Bash
      Version: 1.2.3.592
      ```
      

   2. Run the following command to check the version of dpkg \*\*\*\*.

      ```Bash
      rpm -qi fsx
      ```
      

      The following version information will be returned.

      ```Bash
      Name        : fsx
      Version     : 1.2.3.592
      Release     : 1
      Architecture: x86_64
      Install Date: Mon 18 Nov 2024 04:30:00 PM CST
      ...
      ```
      


</Tab>
<Tab zoneid="Z4Bz7gsFLV" title="Other Operating Systems">
<TabTitle>Other Operating Systems</TabTitle>

1. Execute the following command to extract fsx.tar.gz to the `/opt/fsx_temp` directory.

   In the following commands, the client extraction directory is `/opt/fsx_temp`; you may use a different directory as needed.

   ```Bash
   mkdir -p /opt/fsx_temp
   ```
   

   ```Bash
   sudo tar -C /opt/fsx_temp -xzf ./fsx.tar.gz
   ```
   

2. Execute the following commands, enter `/opt/fsx_temp`, and upgrade the client.

   ```JSON
   cd /opt/fsx_temp
   ```
   

   ```Bash
   sudo ./fsx -m update
   ```
   

3. After the upgrade is complete, you can execute the following command to delete the temporary directory of the installation package.

   ```Bash
   sudo rm -rf /opt/fsx_temp
   ```
   


</Tab>
</Tabs>


<span id="sMiBcryZ"></span>
## Uninstall FSX Client

The following uses the x86_64 system architecture as an example to describe the steps for uninstalling the FSX client.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before uninstalling FSX, please ensure that all mount points have been unmounted in the Linux system; otherwise, the client uninstallation will fail. For detailed instructions on unmounting a mount point, please refer to <a href="https://docs.byteplus.com/docs/tos/FSX-configuration-and-mounting#570d17e6">Unmounting a Mount Point</a>.</div>



<Tabs>
<Tab zoneid="oHU5AFyOUI" title="Deb-based distribution (veLinux)">
<TabTitle>Deb-based distribution (veLinux)</TabTitle>

Execute the following command to uninstall the FSX client.

```Bash
dpkg -P fsx
```



</Tab>
<Tab zoneid="cM52uiOuu6" title="RPM-based distributions (veLinux CentOS Compatible)">
<TabTitle>RPM-based distributions (veLinux CentOS Compatible)</TabTitle>

Run the following command to uninstall the FSX client.

```Bash
rpm -e fsx
```



</Tab>
<Tab zoneid="zLp6Uvbo7F" title="Other Operating Systems">
<TabTitle>Other Operating Systems</TabTitle>

1. Execute the following command, and enter `/opt/fsx`.

   ```Bash
   sudo cd /opt/fsx 
   ```
   

2. Run the following command to uninstall the FSX client.

   ```Bash
   sudo ./fsx -m uninstall
   ```
   


</Tab>
</Tabs>
