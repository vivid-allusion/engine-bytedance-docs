---
title: "Installing FSX"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Installing_FSX"
---

This topic provides notes and steps for installing FSX.

<span id="4037108c"></span>
## Notes


* For a list of operating systems supported by FSX, see [FSX Operating environment](https://docs.byteplus.com/en/docs/nas/FSX_overview#75ccf9d1).

* The FSX client will be installed in the `/opt/fsx` directory. Ensure that the disk space of this directory exceeds 1GB to avoid installation failure or malfunction.

* During the installation of FSX, configuration files are stored in `/opt/tmp/fsx` and logs in `/var/log/fsx`. Make sure there are no directories with the same names in your system to prevent installation failure or malfunction.


<span id="79969740"></span>
## Installing FSX

FSX supports multiple operating systems. Select the appropriate installation method based on your operating system.


<Tabs>
<Tab zoneid="XvAktQdAhh" title="Deb-based distributions (veLinux/Ubuntu/Debian)">
<TabTitle>Deb-based distributions (veLinux/Ubuntu/Debian)</TabTitle>

1. For operating system\-specific installation packages, contact the technical team for the latest builds.

2. Run this command to install the client.

   ```Bash
   dpkg -i fsx_amd64.deb 
   ```
   

3. Run this command to check the client version.

   ```Bash
   fsx -v
   ```
   

   The following version information indicates a successful installation.

   ```Bash
   Version: 1.1.0.400
   ```
   





</Tab>
<Tab zoneid="W85CwVrdE7" title="RPM-based distributions (veLinux CentOS Compatible/CentOS)">
<TabTitle>RPM-based distributions (veLinux CentOS Compatible/CentOS)</TabTitle>

1. For operating system\-specific installation packages, contact the technical team for the latest builds.

2. Run this command to install the client.

   ```Bash
   rpm -ivh fsx_x86_64.rpm
   ```
   

3. Run this command to check the client version.

   ```Bash
   fsx -v
   ```
   

   The following version information indicates a successful installation.

   ```Bash
   Version: 1.1.0.400
   ```
   





</Tab>
<Tab zoneid="hSWPhnErJx" title="Other operating systems">
<TabTitle>Other operating systems</TabTitle>

1. For operating system\-specific installation packages, contact the technical team for the latest builds.

2. Run this command to extract the FSX installation package.

   ```Bash
   sudo tar -C /root -xzf ./storage.fsx.bin_1.1.0.69.tar.gz
   ```
   

3. Run this command to create the `/opt/fsx` directory.

   ```Bash
   sudo mkdir -p /opt/fsx
   ```
   

4. Run this command to extract `fsx.tar.gz` to the `/opt/fsx` directory.

   ```Bash
   sudo tar -C /opt/fsx -xzf ./fsx.tar.gz
   ```
   

5. Go to the `/opt/fsx` directory and run this command to install FSX.

   ```Bash
   sudo ./fsx -m install
   ```
   

6. Run this command to check the client version.

   ```Bash
   sudo fsx -v
   ```
   

   The following version information indicates a successful installation.

   ```Bash
   Version: 1.1.0.400
   ```
   





</Tab>
</Tabs>


<span id="5a3cde77"></span>
## Upgrading FSX

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Upgrading FSX may cause a brief disruption to the service. We recommend performing the upgrade during off\-peak hours.</div>



<Tabs>
<Tab zoneid="1v89T2ZC" title="Deb-based distributions (veLinux/Ubuntu/Debian)">
<TabTitle>Deb-based distributions (veLinux/Ubuntu/Debian)</TabTitle>

1. For operating system\-specific installation packages, contact the technical team for the latest builds.

2. Run this command to upgrade the client.

   ```Bash
   dpkg -i fsx_amd64.deb
   ```
   

3. To confirm whether the client has been successfully upgraded, check the running binary version and the dpkg version.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If both version numbers match, the upgrade is successful.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the two version numbers do not match, please contact the technical team for support.   </div>
   

   1. Run this command to view the running binary version.

      ```Bash
      fsx -v
      ```
      

      The following version information is returned.

      ```Bash
      Version: 1.1.0.400
      ```
      

   2. Run this command to check the dpkg ** ** version.

      ```Bash
      dpkg -l fsx
      ```
      

      The following version information is returned.

      ```Bash
      ||/ Name           Version      Architecture Description
      +++-==============-============-============-================================================================================
      ii  fsx        1.1.0.400     amd64        fsx branch: fsx/xxx_09b1043bb962e8bb10****a71cb41477b9ce****
      ```
      


</Tab>
<Tab zoneid="4Tx0MACq" title="RPM-based distributions (veLinux CentOS Compatible/CentOS)">
<TabTitle>RPM-based distributions (veLinux CentOS Compatible/CentOS)</TabTitle>

1. For operating system\-specific installation packages, contact the technical team for the latest builds.

2. Run this command to upgrade the client.

   ```Bash
   rpm -Uvh fsx_x86_64.rpm
   ```
   

3. To confirm whether the client has been successfully upgraded, check the running binary version and the dpkg version.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If both version numbers match, the upgrade is successful.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the two version numbers do not match, please contact the technical team for support.   </div>
   

   1. Run this command to view the running binary version.

      ```Bash
      fsx -v
      ```
      

      The following version information is returned.

      ```Bash
      Version: 1.1.0.400
      ```
      

   2. Run this command to check the dpkg version.

      ```Bash
      rpm -qi fsx
      ```
      

      The following version information is returned.

      ```Bash
      Name        : fsx
      Version     : 1.1.0.400
      Release     : 1
      Architecture: x86_64
      Install Date: Mon 18 Nov 2024 04:30:00 PM CST
      ...
      ```
      





</Tab>
<Tab zoneid="jF0pcDQx" title="Other operating systems">
<TabTitle>Other operating systems</TabTitle>

1. For operating system\-specific installation packages, contact the technical team for the latest builds.

2. Run this command to extract the FSX installation package.

   ```Bash
   sudo tar -C /root -xzf ./storage.fsx.bin_1.1.0.69.tar.gz
   ```
   

3. Run this command to create the `/opt/fsx_temp` directory.

   ```Bash
   sudo mkdir -p /opt/fsx_temp
   ```
   

4. Run this command to extract `fsx.tar.gz` to the `/opt/fsx_temp` directory.

   In the following commands, the client extraction directory is set to `/opt/fsx_temp`. You can choose a different directory that suits your specific needs.

   ```Bash
   sudo tar -C /opt/fsx_temp -xzf ./fsx.tar.gz
   ```
   

5. After navigating to the `/opt/fsx_temp` directory, run this command to upgrade the client.

   ```Bash
   sudo ./fsx -m update
   ```
   

6. After the upgrade, run this command to delete the directory where the installation package is stored.

   ```Bash
   sudo rm -rf /opt/fsx_temp
   ```
   





</Tab>
</Tabs>


<span id="7b03a504"></span>
## Uninstalling FSX

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before uninstalling FSX, make sure that you have unmounted all mounted directories in Linux. Otherwise, the uninstallation will fail.</div>



<Tabs>
<Tab zoneid="CevpFiiH" title="Deb-based distributions (veLinux/Ubuntu/Debian)">
<TabTitle>Deb-based distributions (veLinux/Ubuntu/Debian)</TabTitle>

Run this command to uninstall the client.

```Bash
dpkg -P fsx
```



</Tab>
<Tab zoneid="5DC51xRK" title="RPM-based distributions (veLinux CentOS Compatible/CentOS)">
<TabTitle>RPM-based distributions (veLinux CentOS Compatible/CentOS)</TabTitle>

Run this command to uninstall the client.

```Bash
rpm -e fsx
```



</Tab>
<Tab zoneid="glfkk4lK" title="Other operating systems">
<TabTitle>Other operating systems</TabTitle>

1. Run this command to enter the `/opt/fsx` directory.

   ```Bash
   sudo cd /opt/fsx 
   ```
   

2. Run this command to uninstall the client.

   ```Bash
   sudo ./fsx -m uninstall
   ```
   


</Tab>
</Tabs>


<span id="nSIBRhjd"></span>
##
