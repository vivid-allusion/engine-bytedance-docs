---
title: "Installing GRID drivers manually"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-GRID-drivers"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

If you need OpenGL graphics and image processing capabilities for GPU Accelerated instances equipped with T4, A10, or L\-Series graphics cards, manually install the NVIDIA GRID driver and purchase the GRID license officially released by NVIDIA.

This topic describes how to apply for a license, configure the license server, and install the GRID driver.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">NVIDIA supports applying for a 90\-day license for trial.</div>


* <div data-tips="true" data-tips-type="tip">This topic is for reference only. If you have any issues when purchasing a license, please contact NVIDIA.</div>


* <div data-tips="true" data-tips-type="tip">You can also use <a href="https://docs.byteplus.com/en/docs/gpu/GPU_Rendering">GPU Rendering</a> instances with the NVIDIA GRID driver installed. In this case, you do not need to follow the installation steps described in this topic. This instance type is in Beta. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="tip">If provided driver versions can not meet your business requirements, you can <a href="https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-GRID-drivers">uninstall the GRID driver</a> and then <a href="https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-GRID-drivers?lang=zh&TagIDs=#.5q2l6aqk5LiJ77ya5a6J6KOFR1JJROmpseWKqA==">install a new one</a>.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A GPU Accelerated instance equipped with T4, A10, and L\-Series graphics cards is created and has internet access. For detailed operations, refer to [Creating GPU Accelerated instances](https://docs.byteplus.com/en/docs/gpu/Buying-GPU-Accelerated-instances).

<span id=".6L2v5Lu254mI5pys"></span>
## Software version


* GRID driver versions:

   * T4, A10: v13.1

   * L\-Series: v16.1

* License server version: v2.0.0

* Docker version: v20.10.17

* Docker\-compose version: v2.6.0Version


<span id=".5q2l6aqk5LiA77ya55Sz6K-3R1JJRCBMaWNlbnNl"></span>
## Step 1: Apply for GRID license


1. Go to [NVIDIA Enterprise Account](http://www.nvidia.com/object/nvidia-enterprise-account.html), register an account, and apply for a trial license.

2. After successfully submitting your application, you are prompted to check your email at the specified email address within 2 days. If the application is approved, you will receive the following two emails.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_920ed7dc3982173eda4c93a25568ea94.png) </span>

3. Open the email "NVIDIA Set Password", as shown in the picture below.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3afb83753c56787e1127627928a88c00.png) </span>

4. Click the "SET PASSWORD" button to set the initial password. Once the initial password is set, click the "LOGIN" button to log in to your NVIDIA enterprise account.

   You can also access the[ NVIDIA license Portal ](https://nvid.nvidia.com/)for login.


<span id=".5q2l6aqk5LqM77ya6YOo572yRExT55qE5pys5Zyw5pyN5Yqh"></span>
## Step 2: Deploy DLS local service

To set up a local DLS server for license authorization in the enterprise private network, follow these steps:

<span id=".Me-8ieS4i-i9vei9r-S7tg=="></span>
### 1) Download software

**Download the containerized DLS server package**


1. Access the [NVIDIA License Portal](https://nvid.nvidia.com/), select "SOFTWARE DOWNLOADS" in the left navigation pane to enter the "Software Downloads" page, and click the "ALL AVAILABLE" button.

2. Select the required software package for download.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b6beb50a1a18821839e15d0e96fab69c.png) </span>


**Download GRID driver**

On the "Software Downloads" page, click the "Download" button to the right of the software package for download.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3d39f919b573ffc38726ba16761767af.png) </span>

<span id=".Mu-8ieWuieijhURvY2tlcuWSjERvY2tlci1jb21wb3Nl"></span>
### 2) Install Docker and Docker\-compose


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following commands to prepare for installation. In this topic, Ubuntu 20.04 is used as an example, and commands are executed as the root user.

   ```Plain Text
   apt-get update                                                             # Update package list
   apt-get remove docker docker-engine docker.io containerd runc              # Uninstall installed packages (retain configuration files)
   apt-get install -y ca-certificates curl gnupg unzip lsb-release            # Install new packages
   ```
   

3. Execute the following commands to add the official GPG key of Docker and the software source.

   ```Plain Text
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -                                         #Import GPG Key
   add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"             #add Docker APT repository
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fcb4c64d76c88671d2ccbe7fac02c5e5.png) </span>

4. Execute the following command to install Docker.

   `apt install -y docker-ce docker-ce-cli containerd.io`

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6bce13a78d92ce0ca78bd1402d31f44c.png) </span>

5. Execute the following commands to download Docker\-compose and grant the execute permission.

   * Download Docker\-compose:

      `curl -L https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose`

   * Add the executable permission to the binary file:

      `sudo chmod +x /usr/local/bin/docker-compose`

      If the following output is displayed, the installation is successful.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_671b824831ef2e07fda354c306193878.png) </span>


<span id=".M--8iemDqOe9smxpY2Vuc2UgMi4wIGltYWdl"></span>
### 3) Deploy license 2.0 image


1. Execute the following commands to decompress the package `nls-2.0.0-bios.zip` into the DLS folder.

   ```Plain Text
   ls -l                             
   mkdir DLS                         
   cd DLS/                           
   unzip ../nls-2.0.0-bios.zip       
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_936bf367aff0878eb3cf4cf566ba057e.png) </span>

2. Execute the following commands to load the container images.

   `docker load --input dls_pgsql_2.0.0.tar.gz`

   `docker load --input dls_appliance_2.0.0.tar.gz`

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_69fa341836f2112119993ea119c12cb0.png) </span>

3. Modify the host address of Docker container service and start the license service.

   `DLS_PUBLIC_IP='192.168.xx.xx' docker-compose up`

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_080e7958aa5bb6c873a2051119a92f08.png) </span>

   > You can also use the `-d` parameter to run the container service in the background by executing the command: `DLS_PUBLIC_IP='192.168.xx.xx' docker-compose up -d`.   
   

   During the first run, the database is initialized. The output displayed for the subsequent run is as follows.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df29dfb83fdf8e61ad9b39b096863035.png) </span>


<span id=".NO-8iemFjee9rkRMU-acjeWKoQ=="></span>
### 4) Configure DLS service


1. Access the DLS console via the modified Docker host address `https://192.168.xx.xx`, and select "New Installation".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5751e4c0f6173b7d9dc70b5fb177987e.png) </span>

2. Set the login name and password. The login name is dls_admin.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e0cc118914c202244b9cc92859c06db0.png) </span>

3. After successful login, you can view the created DLS instance. You can modify the IP address and name of the instance based on your needs. After the modification, you need to log in again using the new IP address.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bc59393236c985694b41ef277636aeab.png) </span>

4. After you confirm that the information is correct, click the "Download DLS Instance Token" button to download the token authorization file. Then, prepare to submit this file to the NVIDIA Portal.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89710b9f5dde719e4c9dfacaf6bef3a7.png) </span>

5. Return to the [NVIDIA Portal](https://nvid.nvidia.com/), select "SOFTWARE INSTANCES" from the left navigation pane, and enter the "Software Instances" page.

6. Click the "ACTIONS" button in the upper right corner. Then, select "Upload DLS instances token" to upload the token file obtained in the previous step and register the DLS instance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_97948f3883e7221259910adae2350589.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6c570486357f8dab087118d1cb202594.png) </span>

7. After the token file is uploaded successfully, you can see the registered DLS instance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c07cfff286c52da7c89de27a3901bb93.png) </span>


<span id=".Ne-8ieWIm-W7ukxpY2Vuc2UgU2VydmVy"></span>
### 5) Create license server


1. Select "CREATE SERVERS" in the left navigation pane to enter the "Create License Server" page, specify the service name, add the required license type and quantity, and then click the "CREATE SERVER" button to create the server.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d59131bdf908dd80832b1a89cb154ef9.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_460350842b5fdcf70b651cfcf3ea71d6.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_454a46a7cb946676de29487e4b533ee7.png) </span>

2. Select "SERVER DETAILS" in the left navigation pane to enter the "License Server Details" page. Click the "BIND SERVICE INSTANCE" button to associate the license server with the registered DLS instance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b27e6f2ad377e82b679bc2fea909cb30.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_47caf7f36a8a0d10a4c5947a653f966d.png) </span>

3. After successful association, select "ACTIONS \> Download" in the upper right corner to download the bin file for transferring license configurations.

4. Return to the local DLS console and upload the bin file to DLS to complete the license transfer.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_11f30cd275196cdc56b38976ab62b966.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1dd5f844e1b4e0ef9bc1e0ef3ab1d564.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de0d5b616b6c8e5f7740c732e72de4af.png) </span>

5. After the bin file is uploaded successfully, the local DLS is granted license authorization permission (token file\-based). You need to download the .tok token file generated by the local DLS and upload it to the GPU instance.


<span id=".Nu-8ieS4i-i9veaOiOadg1Rva2Vu5paH5Lu2"></span>
### 6) Download token file for authorization


1. On the home page of the DLS console, select "ACTIONS \> Generate client config token" to generate the token file.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b45eedcab37379ceaafd1cc7d9cc094f.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dde6ffe116039b201a0e44048cf06601.png) </span>

2. Transfer the downloaded token file to the GPU instance. To upload data, refer to [Overview of local data upload](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview).


<span id=".5q2l6aqk5LiJ77ya5a6J6KOFR1JJROmpseWKqA=="></span>
## Step 3: Install GRID driver

<span id="Windows"></span>
### Windows

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This operation applies to Windows instances with the GPU driver not installed.</div>


* <div data-tips="true" data-tips-type="tip">The following public images with preinstalled GPU drivers do not currently support installing the GRID driver.</div>


   * <div data-tips="true" data-tips-type="tip">Windows Server 2019 Datacenter Edition 64\-bit Chinese (GPU)</div>


   * <div data-tips="true" data-tips-type="tip">Windows Server 2016 Datacenter Edition 64\-bit Chinese (GPU)</div>


1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Install the obtained GRID driver.

   1. Double\-click the installation program, and in the prompted dialog box, click the "OK" button. During installation, the program is automatically decompressed.

   2. After extraction is complete, in the pop\-up "NVIDIA Installer" dialog box, click the "Agree and Continue (A)" button.

   3. Keep the default installation options, and click the "Next (N)" button.

   4. After installation is complete, click the "Close" button.

3. Check whether the GRID driver is successfully installed.

   1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   2. Click the "Start" button. In the "Recently Added" section, if "NVIDIA RTX Desktop Manager" and "NVIDIA Corporation" are displayed, the installation succeeds.

4. Configure and activate the license service.

   1. Copy the obtained .tok file into the following directory.

      `C:\Program Files\NVIDIA Corporation\vGPU Licensing\ClientConfigToken`

   2. Set the value of `FeatureType` to 2.

      1. Right\-click "Start \> Run", enter "regedit", and click the "OK" button to open the Registry Editor.

      2. Locate `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\NVIDIA Corporation\Global\GridLicensing` or `Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\nvlddmkm\Global\GridLicensing`.

      3. Create a value item.

         Select `GridLicensing`, and then choose "Edit \> New \> DWORD (32\-bit) Value (D)" in the upper left corner.

      4. Select the value item, click the "Edit \> Modify" button in the upper left corner, and modify the value name to `FeatureType` and the value data to `2`.

   3. Restart the NvDisplayContainer service.

      Right\-click "Start \> Search" and enter "Services". In the pop\-up "Services" dialog box, right\-click "NvDisplayContainer" and select "Restart (E)".

   4. View license status.

      `C:\Program Files\NVIDIA Corporation\NVSMI\nvidia-smi.exe -q`

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7e44e29ab40ecb8cb8e2b858fe9ac1be.png) </span>

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_28e59b493059cbe398db6fe8c743fcd5.png) </span>


<span id="Linux"></span>
### Linux


1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Install the obtained GRID driver.

   1. Execute the following commands to install the GRID driver.

      ```Plain Text
      chmod +x NVIDIA-Linux-x86_64-470.82.01-grid.run
      ./NVIDIA-Linux-x86_64-470.82.01-grid.run         
      ```
      

   2. Execute the `nvidia-smi` command to check whether the GRID driver is successfully installed.

      If the following output is returned, the installation succeeds.

      `Driver Version` indicates the current GRID driver version, and `CUDA Version` indicates the maximum supported version of the GRID driver.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9cd175626a253490e7c62c7c6ca08eea.png) </span>

3. Configure and activate the license service.

   1. Execute the `cd /etc/nvidia` command to switch to the /etc/nvidia directory.

   2. Execute the following command to create the gridd.conf file.

      `cp gridd.conf.template gridd.conf`

   3. Execute the `vim gridd.conf` command to open the gridd.conf file, and press `i` to enter edit mode.

   4. Set the value of `FeatureType` to 2, and keep other configurations as default.

   5. Press the `Esc` key to exit edit mode, enter `:wq`, and then press `Enter` to save and exit the file.

   6. Execute the following command to copy the obtained .tok file to the /etc/nvidia/ClientConfigToken directory.

      `cp <.tok file path> /etc/nvidia/ClientConfigToken/`

   7. Execute the following command to restart the nvidia\-gridd service.

      `systemctl restart nvidia-gridd.service`

   8. View license status.

      * Method 1: Execute the `nvidia-smi -q` command. If the following output is displayed, license activation is successful.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_62aec7f2eadc08637cafe1ddb9d22fe5.png) </span>

      * Method 2: Execute the `systemctl status nvidia-gridd.service` command. If the following output is displayed, license activation is successful.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f38190fd5a017a1fb87846ee10f0feb8.png) </span>
