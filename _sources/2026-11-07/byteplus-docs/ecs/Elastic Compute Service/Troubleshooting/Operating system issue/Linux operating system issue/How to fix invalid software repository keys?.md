---
title: "How to fix invalid software repository keys?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/How_to_fix_expired_software_repository_keys"
---

<span id="jwNHfzP9"></span>
## Issue description

When you install or update packages on a Linux system using a package manager (such as `apt`, `yum`, or `dnf`), the following signature verification errors occur.


* **veLinux/Debian/Ubuntu**

   ```Plain Text
   The following signatures were invalid: KEYEXPIRED <fingerprint>
   ```
   

* **CentOS/Rocky Linux/AlmaLinux**

   ```Plain Text
   NOKEY: Public key for package is not installed
   ```
   


<span id="9r3Fbnhs"></span>
## **Causes**

Software repository key is a GPG public key used to verify the legitimacy of software package sources. In Linux systems, package managers (for example, `apt`, `yum`, and `dnf`) use software repository keys to verify the digital signature of each package during installation or update to ensure that the package is signed by a trusted publisher and not tampered with in transit. If a software repository key is missing, expired, or mismatched, the package manager refuses to install or update the package and returns a signature verification error.

<span id="48FgYeel"></span>
## Solutions

This section describes common solutions for software repository key expiration. You can first update the software repository key within the affected **instance**. If the instance was created from a **custom image**, you can fix the issue within the image as needed to prevent new instances created from it from encountering the same key issue.

<span id="EqwxqOOd"></span>
### Step 1: Fix the affected instance

<span id="8Sh7bBjG"></span>
#### Solution 1: Update software repository key via cloud assistant


* **Prerequisites**

   [Cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client?lang=en) has been installed on the target instance.

* **Procedure**

   1. Log in to the [cloud assistant console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/invocations).

   2. In the top menu bar, select the region where the target instance resides.

   3. Click the "Create a job" button and enter the following information.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">This section describes only the parameters required for issue solution. Keep other parameters with default values. For the complete parameter description, see <a href="https://docs.byteplus.com/en/docs/ecs/Creating-a-job">Creating jobs</a>.      </div>
      

      
      |Parameter​ |Description |
      |---|---|
      |**Execute command** ||
      |Command source |Select ****[Public commands](https://docs.byteplus.com/en/docs/ecs/Managing-public-command?lang=en#.5YWs5YWx5ZG95Luk5rGH5oC7). |
      |Command |Select **Update software repository key**. |
      |Executing user |Select the **root** user. |
      |**Object** ||
      |Object |Select the ECS instances for which you want to update the software repository key.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can select up to 200 ECS instances.</div><br> |
      

   4. Click the "Confirm" button. After the job is created, the system automatically redirects you to the Job management page and starts job execution.

   5. Verify whether the software repository key update succeeds.

      1. When the job status changes to **Succeeded**, click the "Execution result" button in the "Actions" column on the right.

      2. Click the "Runtime log" button in the "Actions" column on the right of the target instances in sequence. If the log contains `keyring installed successfully`, the software repository key of the corresponding instance is updated.


<span id="d44g9Z8w"></span>
#### Solution 2: Manually update software repository key


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the corresponding commands according to the instance operating system to update the key information.

   
   <Tabs>
   <Tab zoneid="0nXGD6yz" title="veLinux">
   <TabTitle>veLinux</TabTitle>
   
   1. Execute the following commands to update the software repository key.
   
      * **veLinux 2.0**
   
         ```Bash
         wget https://mirrors.ivolces.com/velinux/pool/main/v/velinux-archive-keyring/velinux-archive-keyring_2.0.0%2Bbase2_all.deb
         dpkg -i velinux-archive-keyring_2.0.0+base2_all.deb
         ```
         
   
      * **veLinux 1.0**
   
         ```Bash
         wget https://mirrors.ivolces.com/velinux/pool/main/v/velinux-archive-keyring/velinux-archive-keyring_1.2%2Bvelinux1_all.deb
         dpkg -i velinux-archive-keyring_1.2+velinux1_all.deb
         ```
         
   
   2. Execute the following command to ensure that the key update succeeds and to refresh the `apt` software repository information.
   
      ```Bash
      sudo apt-get update
      ```
      
   
      If the output does not contain `The following signatures were invalid: EXPKEYSIG`, the software repository key is updated.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f2ad7e23b878bb5c0c96924f18e09d7c.png) </span>
   
   
   </Tab>
   <Tab zoneid="Pw44jmPI" title="Ubuntu">
   <TabTitle>Ubuntu</TabTitle>
   
   1. Execute the following commands to update the software repository key.
   
      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
      
   
      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Replace <code><fingerprint></code> with the actual value contained in the error message when you execute the <code>apt-get update</code> command. For example, if the error message is <code>The following signatures were invalid: EXPKEYSIG 3B4FE6ACC0B21F32</code>, replace the value with <code>3B4FE6ACC0B21F32</code>.   </div>
      
   
      ```Bash
      sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys <fingerprint>
      ```
      
   
   2. Execute the following command to ensure that the key update succeeds and to refresh the `apt` software repository information.
   
      ```Bash
      sudo apt-get update
      ```
      
   
      If the output does not contain `The following signatures were invalid: EXPKEYSIG`, the software repository key is updated.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2265f1eaa9ee0273cc81bddb2ba57282.png) </span>
   
   
   </Tab>
   <Tab zoneid="5q5GGHfn" title="Debian">
   <TabTitle>Debian</TabTitle>
   
   1. Obtain the repository key download URL for the update.
   
      1. From any device with internet access and a browser, visit the[ Debian official key release information page](https://ftp-master.debian.org/keys.html).
   
      2. Based on the OS release version number (for example, 12) or codename (for example, bookworm) of the target instance, find and obtain the download URLs for the corresponding **Archive Signing Key** and ** Security Archive Signing Key**.
   
   2. On the target instance, execute the following commands to download the new keys.
   
      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
      
   
      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The Debian 12/bookworm commands are used as an example. Replace <code>https://ftp-master.debian.org/keys/archive-key-12.asc</code> and <code>https://ftp-master.debian.org/keys/archive-key-12-security.asc</code> with the actual key download URLs you obtain.   </div>
      
   
      ```Bash
      cd /etc/apt/trusted.gpg.d/
      sudo wget https://ftp-master.debian.org/keys/archive-key-12.asc
      sudo wget https://ftp-master.debian.org/keys/archive-key-12-security.asc
      ```
      
   
   3. Execute the following command to verify that the key update succeeds and to refresh the `apt` software repository information.
   
      ```Bash
      sudo apt-get update
      ```
      
   
      If the output does not contain `The following signatures were invalid: EXPKEYSIG`, the software repository key is updated.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8906baa8b1cc7ccd7e763cabb476867.png) </span>
   
   
   </Tab>
   <Tab zoneid="MlLECOPl" title="CentOS/Rocky Linux/AlmaLinux">
   <TabTitle>CentOS/Rocky Linux/AlmaLinux</TabTitle>
   
   1. Execute the following command to import the official software repository key.
   
      ```Bash
      rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-*
      ```
      
   
   2. Execute the following command to import the EPEL software repository key.
   
      * **CentOS Stream 10.x/Rocky Linux 10.x/AlmaLinux 10.x**
   
         ```Bash
         rpm --import https://mirrors.ivolces.com/epel/RPM-GPG-KEY-EPEL-10
         ```
         
   
      * **CentOS Stream 9.x/Rocky Linux 9.x/AlmaLinux 9.x**
   
         ```Bash
         rpm --import https://mirrors.ivolces.com/epel/RPM-GPG-KEY-EPEL-9
         ```
         
   
      * **CentOS 8.x/Rocky Linux 8.x/AlmaLinux 8.x**
   
         ```Bash
         rpm --import https://mirrors.ivolces.com/epel/RPM-GPG-KEY-EPEL-8
         ```
         
   
      * **CentOS 7.x**
   
         ```Bash
         rpm --import https://mirrors.ivolces.com/epel/RPM-GPG-KEY-EPEL-7
         ```
         
   
   3. Execute the following command to check whether the repository key is imported and updated.
   
      ```Bash
      yum install --assumeno curl
      ```
      
   
      * If the output does not contain `NOKEY: Public key for package is not installed`, the software repository key is updated.
   
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8c449c51571f5e0159945335c93c88a9.png) </span>
   
      * If the output displays` Import of key(s) didn't help, wrong key(s)?`, this error indicates that the imported key does not match the signature/data being verified. You need to manually import the GPG key from the official software package repository. For example, to import the AlmaLinux official repository key:
   
         ```Bash
         rpm --import https://mirrors.ivolces.com/almalinux/RPM-GPG-KEY-AlmaLinux
         ```
         
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="8e2kCDll"></span>
### Step 2: (Optional) Fix the affected custom image

If your affected ECS instance was created from a **custom image**, updating the software repository key fixes only the current instance. The change is not automatically synchronized to the corresponding custom image. If you still need to use the custom image to create new instances, follow the instructions in this section to create a temporary instance first to complete the fix, and then recreate the custom image.


1. Create a temporary instance from the affected custom image.

   1. Log in to the [Custom Image console](https://console.byteplus.com/image/region:image+cn-beijing/images?tab=2&projectName=default).

   2. In the top menu bar, select the region and project of the target image.

   3. Click the "Create Instances" in the "Actions" column to the right of the target image.

   4. On the instance creation page, refer to [Purchasing an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to create an instance.

2. Follow the instructions in [Step 1](https://docs.byteplus.com/en/docs/ecs/How_to_fix_expired_software_repository_keys#EqwxqOOd) to update the software repository key in the temporary instance.

3. Recreate the custom image based on the fixed temporary instance.

   1. After the update succeeds, click "... \> Volumes & Image \> Create custom image" in the "Actions" column on the right side of the target instance.

   2. Enter the name, project, and other information of the new image as needed. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance#.5q2l6aqk5Zub77ya6YCa6L-H5a6e5L6L5Yib5bu66Ieq5a6a5LmJ6ZWc5YOP).

   3. Click the "Create" button and wait until the custom image is created.

4. If the status of the new image is **Available** in the "State" column, the custom image is created.

5. After the new image has been created, you can clear resources as needed, including the temporary instance used to repair the image and the custom images that still have software repository key issues. This helps avoid incurring additional charges or unnecessary resource usage.
