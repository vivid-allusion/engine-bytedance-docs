---
title: "Manually deploying MySQL databases on Windows instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Manually_deploying_MySQL_databases_on_Windows_instances"
---

This topic describes how to manually deploy MySQL on Windows instances using the "mysql\-installer\-community" installation tool.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic involves third\-party product information, which is for reference only. BytePlus does not make any implied guarantees or other forms of commitments for the performance, reliability, or potential impacts of operations that involve any third\-party product.</div>


<span id="k7flEfoo"></span>
## Prerequisite

You have purchased a Windows\-based instance. For more information, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

   > In the example provided in this topic, Windows Server 2019 is used. The operating system may differ slightly depending on the version.   
   

2. Go to the [MySQL official website](https://downloads.mysql.com/archives/installer/).

3. Select the target version, click the "Download" button to download the mysql\-installer\-community installation package.

   > This practice uses the "mysql\-installer\-community\-8.0.42.0.msi" version as an example. Different versions may vary slightly.   
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_417375d6681928dcfa1956b0c83a2d3b.png) </span>

4. Install the installation package downloaded.

   1. Double\-click the installation package "mysql\-installer\-community".

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the installation package opens automatically after being downloaded, skip this step.      </div>
      

   2. Select "Custom", and click the "Next" button.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_576fd64f8941d83a6db27f91faf8223d.png) </span>

   3. In the product directory on the left, select the version "MySQL Server 8.0.42\-X64" to be installed, and the corresponding "MySQL Documentation" and "Samples and Examples". Then, click "Next" to proceed to the next step.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">As needed, you can select the MySQL version of the product to be installed from the product directory on the left and add it to the installation list on the right. To ensure compatibility, we recommend that you keep selected items such as "MySQL Documentation", "Samples and Examples", and other items in the same version as the MySQL version.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">MySQL Documentation: provides MySQL documentation covering information such as detailed descriptions and user guides. You can install it based on your needs.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Samples and Examples: provides example codes and example databases, which help you quickly understand and get started with MySQL features. You can install it based on your needs.      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc3761f85d937b570b371226c8bc4a05.png) </span>

   4. Check dependencies

      1. If any uninstalled dependency package is detected, please click the "Execute" button to download it.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f9cd3bead743ffcc3e0d20a885fbcc64.png) </span>

      2. After the download is complete, you will automatically enter the dependency package installation interface. Select "I agree to the license terms and conditions", and click the "Install" button.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb210ff1f44353850cd13d28c8a00408.png) </span>

      3. After the dependency package is installed, click the "Close" button.

   5. Click the "Next" button. Verify that the list of products about to be installed is correct, and then click the "Execute" button.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8d223861f5b62fd338766e83a64b9aff.png) </span>

   6. Wait until the installation succeeds, then click "Next".

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6792f52de5293583255d1f9c58e3ebfc.png) </span>

5. Configure MySQL Server

   1. On the "Product Configuration" page, click the "Next" button.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5e87ccdff4b4e138bc7164b8c0b1f9a2.png) </span>

   2. Click the "Config Type" drop\-down list and select "Server Computer". Then, click "Next".

      > For other configurations, we recommend that you use the default settings, or you can configure them as needed.      
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a7e5333a93bd9f8b6af98d368116959.png) </span>

   3. Keep the default values, and click the "Next" button.

   4. Set the MySQL root account password, and then click the "Next" button.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The root account in MySQL is a super administrator account. It has all database permissions, such as creating databases, modifying user permissions, and reading/writing any data.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Please keep your root account password safe for future use, such as logging in to MySQL.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can also click "Add User" to create a new account as needed.      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fbe3f4ded2e3fc40768df5b85ee0e125.png) </span>

   5. Keep the default settings on the "Windows Server" page, and click "Next".

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff9f1826af4b94c073918be6ff0444cd.png) </span>

   6. Keep the default settings on the "Server File Permissions" page, and click "Next".

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2fff3132e97902e932723fee20cfd70d.png) </span>

   7. Click the "Execute" button to configure the application. Wait until the application is configured, and then click "Finish" to complete the configuration of MySQL Server.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_98eac5eab2c0fc613bf971c714a7821e.png) </span>

6. Click the "Next" button to configure "Samples and Examples".

   1. Enter the root account password configured in the previous steps, and then click the "Check" button to verify the connectivity of the MySQL database.

   2. When a check mark (✔) and the message "Connection successful" are displayed, the installer has confirmed that the root password is correct and the local MySQL service has been started. Click "Next" to proceed.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1c5a6e20b050227875a8ebced5c2c224.png) </span>

   3. Click the "Execute" button to configure the application.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_430870d45216fe3414f105ffbef2201f.png) </span>

   4. Wait until the application is configured, click "Finish" to complete the configuration.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_25833d600b0345b54ad19fb131f94652.png) </span>

   5. On the "Product Configuration" page, click the "Next" button.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_18802e3e14b0cb8a15e5a192ad4fb1b0.png) </span>

   6. Click the "Finish" button to complete the installation.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_022c26dd2217137aa769dc8f729b6930.png) </span>

7. Verify deployment results

   1. In the Windows menu, select "MySQL \> MySQL 8.0 Command Line Client" to open the MySQL command line page.

   2. Enter the root account password configured in the previous steps, and press the "Enter" key to log in to MySQL.

      If the following information is displayed, the MySQL database has been deployed.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_75b31ddb12ea16908267fe3f66f46699.png) </span>
