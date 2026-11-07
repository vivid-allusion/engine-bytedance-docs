---
title: "Manually setting up a web environment"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Manually_build_a_Web_Environment"
---

This topic describes how to quickly deploy a web environment on an ECS instance running the Windows operating system.

<span id=".6L2v5Lu254mI5pys"></span>
### Software versions


* Operating system: In the example provided in this topic, Windows Server 2022 is used.

* Web server: In the example provided in this topic, Apache HTTP Server 2.4.58 is used.

* Database: In the example provided in this topic, MySQL 8.0.36 is used.

* Programming language: In the example provided in this topic, PHP 8.3.1 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A Windows instance is purchased. For more information, see [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* An EIP is associated with the Windows instance, enabling the instance to connect to the Internet. For information about how to associate an EIP with an ECS instance, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5a6J6KOF5bm26YWN572uQXBhY2hl"></span>
### Step 1: Install and configure Apache


1. Log in to the target Windows instance. For more information, see [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. In the example provided in this topic, Apache is installed by using the Apache HTTP Server 2.4.58 binary package compiled by Apache Lounge with VS17 (Windows® Visual Studio C++ 2022).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The official Apache HTTP Server does not provide binary packages for Windows. You can use one of the following methods to obtain a binary package:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Refer to this practice to obtain a third\-party precompiled binary package. For more information, see <a href="https://www.apachelounge.com/download/#google_vignette">Apache Lounge</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Download and compile the source code. For more information, see <a href="https://httpd.apache.org/docs/current/platform/windows.html#down">Using Apache HTTP Server on Microsoft Windows</a>.   </div>
   

   1. Access the [Apache Lounge official website](https://www.apachelounge.com/download/#google_vignette) by using the instance browser.

   2. Select the required installation package, and click the package to download it.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_72df992aa1acbd1cfa2ff782750e8cd1.png) </span>

   3. After the download is complete, right\-click the package and select "Extract All(T)...".

   4. In the pop\-up window, select the storage path and click the "Extract" button.

3. Configure the server.

   1. Go to the folder you extracted. In the "Apache24 \> conf" folder, right\-click the httpd.conf file, select "Open with", and open this configuration file by using Notepad.

   2. Locate the `Define SRVROOT` configuration item in the configuration file.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0c7817dc6c64f0b8daf05f1e09025407.png) </span>

   3. Change the default value c:Apache24 to the path where you extracted the Apache24 files.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Replace <code>C:/Users/Administrator/Downloads/httpd-2.4.58-win64-VS17/Apache24</code> with the actual path, and replace backslashes (<code>\</code>) in the original Windows path with forward slashes (<code>/</code>).      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e5999dafa46b43e019e443834cb89b1.png) </span>

   4. Change the value of the `Listen` parameter to the following content, and press `Ctrl`+`S` to save the change.

      ```Plain Text
      0.0.0.0:80
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_542fd9dbfb5523b1a37bee1e4e87df28.png) </span>

4. Click the Windows icon in the lower\-left corner, then select "Windows Security".

   1. In the directory tree on the left, select "Firewall & network protection".

   2. Click the "Allow an app through firewall" button.

   3. In the "Allow apps to communicate through Windows Defender Firewall" dialog box, click the "Allow another app..." button.

   4. In the "Add an app" dialog box, click the "Browse" button.

   5. Go to the bin folder in the Apache installation directory, select the httpd.exe file, and click the "Open" button.

   6. In the "Add an app" dialog box, click the "Add" button.

   7. In the "Allow apps to communicate through Windows Defender Firewall" dialog box, select the checkbox in the "Public" column to the right of "Apache HTTP Server".

   8. Click "OK" to complete the operation.

5. Start the server and check whether the server is running.

   1. Click the Windows icon in the lower\-left corner, select "Windows System," right\-click "Command Prompt", and then click "More \> Run as administrator."

   2. In the Command Prompt dialog box, execute the following command to enter the directory where the Apache HTTP Server files are located.

      > Replace `httpd-2.4.58-win64-VS17\Apache24\bin` with the actual path to the Apache HTTP Server bin folder after extraction.      
      

      ```Plain Text
      cd httpd-2.4.58-win64-VS17\Apache24\bin
      ```
      

   3. Execute the following command to start the server.

      ```Plain Text
      httpd.exe
      ```
      

   4. In the address bar of the instance browser, enter the following address and press the Enter key.

      ```Plain Text
      http://localhost
      ```
      

      If the following output is displayed, Apache HTTP Server is installed and started.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cec88394a78b661487a089b9eb4a014b.png) </span>

6. In the Command Prompt window where you start the server, press `Ctrl` to +`C`shut down the server.


<span id=".5q2l6aqk5LqM77ya5a6J6KOF5bm26YWN572uTXlTUUw="></span>
### Step 2: Install and configure MySQL


1. Log in to the target Windows instance. For more information, see [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Access the [MySQL Installer for Windows](https://www.apachelounge.com/download/#google_vignette) page by using the instance browser.

3. Select the MySQL version and instance operating system for which you want to download the tool, and then click the "Download" button to download the MySQL installer.

   > This practice is used to deploy a web environment. We recommend that you use mysql\-installer\-web\-community\-8.0.36.0.msi. Select the version based on your business requirements.   
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a9e5374c9545ed86e320be09ef2db44e.png) </span>

4. Double\-click the downloaded installer to start the installation process.

   1. On the "Choosing a Setup Type" page:

      1. Select the content you want to install. In this practice, keep the default settings.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_945e10fc3205b6e151a616aa40db8a7e.png) </span>

      2. Click the "Next" button to proceed to the next step.

   2. On the "Check Requirements" page, click the "Execute" button to check whether the conditions required to run MySQL are installed.

      1. If there are any toolkits or other components that are installed, follow the instructions to complete the installation.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59ec1497b02554c1a508e9c29d20416f.png) </span>

      2. After the check is passed, click the "Next" button to proceed to the next step.

   3. On the "Download" page:

      1. Click the "Execute" button to download MySQL Server.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a36eedea3d948d7bbd5dfa3b87d0c7ba.png) </span>

      2. After the download is complete, click the "Next" button to proceed to the next step.

   4. On the "Installation" page:

      1. Click the "Execute" button to install MySQL.

      2. After installation is complete, click the "Next" button to proceed to the next step.

5. On the "Product Configuration" page, click the "Next" button to enter the configuration process.

   1. On the "Type and Networking" page:

      1. Configure the current instance type, the port used by MySQL, and other information.

         > In this practice, the default settings are used. Modify the settings based on your business requirements.         
         

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b74423544be7162773333f555963c53d.png) </span>

      2. Click the "Next" button to proceed to the next step.

   2. On the "Named Pipe" page, retain the default settings, and click the "Next" button to proceed to the next step.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_826c0640af28a2ae63d903748512ef17.png) </span>

   3. On the "Authentication Method" page, retain the default settings, and click the "Next" button to proceed to the next step.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ce3b528201d82ec8bbed5c8198490b9.png) </span>

   4. On the "Accounts and Roles" page:

      1. Configure the login password for the `root` user, and add users based on your business requirements.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e2ef7e18e129d676ca0ed456cb13af0b.png) </span>

      2. Click the "Next" button to proceed to the next step.

   5. On the "Windows Service" page, retain the default settings, and click the "Next" button to proceed to the next step.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dcfe9ebaccf28798efdae911f4952311.png) </span>

   6. On the "Server File Permission" page, retain the default settings, and click the "Next" button to proceed to the next step.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5760d91a500927b431dd422709574ee0.png) </span>

   7. On the "Apply Configuration" page, click the "Execute" button to make the configuration take effect.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_340991eeb0ed98d9314efee73f6f7053.png) </span>

   8. Click the "Finish" button to complete the configuration process.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de2b75048bf3a8c0c9940bea6618c1d1.png) </span>

6. After you return to the installation process, click the "Next" button to proceed to the next step.

7. On the "Installation Complete" page, click the "Finish" button to complete the installation process.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_97c11b33e8a568fb9333ac3270cbb221.png) </span>

8. Start the server and check whether the server is running.

   1. Click the Windows icon in the lower\-left corner, and click "MySQL \> MySQL 8.0 Command line Client".

   2. In the MySQL command line tool, enter the login password of the `root` account.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_29a3894a8ee2da2b7320669b8a8b57ef.png) </span>

   3. You can use this command line tool to create and modify database tables and other related information.


<span id=".5q2l6aqk5LiJ77ya5a6J6KOFUEhQ"></span>
### Step 3: Install PHP


1. Log in to the target Windows instance. For more information, see [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Access the [PHP For Windows](https://windows.php.net/download#php-8.3) page by using the instance browser and select the required installation package.

   > Select a thread\-safe PHP version. In this practice, version 8.3.1 is used.   
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5cbda3f11d02ec720156a929541c16d3.png) </span>

3. After the download is complete, right\-click the package and select "Extract All(T)...".

4. In the pop\-up window, select the storage path and click the "Extract" button.

5. After extraction is complete, right\-click the php.ini\-production file in the folder obtained from the extraction and click the "Copy" button. Then, right\-click any blank area in the current folder window and click the "Paste" button to create a copy of the file.

6. Right\-click the copied file, click the "Rename" button, and change the file name to php.ini.

7. Right\-click the php.ini file, select "Open with", and open the configuration file by using Notepad.

   1. In the configuration file, locate the extension_dir parameter and delete the `;` symbol at the beginning of the line where the parameter resides, and change the value of the parameter to the actual path of the PHP ext folder.

      > Replace the backslash (`\`) in the path with the forward slash`/`.      
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f6954d1ac51fcc8f1bc63079f88a28d7.png) </span>

   2. In the configuration file, locate the `extension=curl`, `extension=mbstring`, `extension=mysqli`, and `extension=pdo_mysql` parameters, and delete the `;` symbol at the beginning of the lines where the parameters reside.

   3. Press `Ctrl` +`S`to save the change.

8. Add the PHP module to the Apache HTTP Server configuration file.

   1. Enter the Apache HTTP Server folder, right\-click the httpd.conf file in the "Apache24 \> conf" folder, select "Open with", and then select Notepad to open this configuration file.

   2. Add the following content to the configuration file.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When you add a path value to the Apache configuration file on the Windows operating system, all backslashes (such as c:\php) should be converted to forward slashes (such as c:/php).      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Replace the sample path with the actual path for each PHP file.      </div>
      

      1. Add the following content to the LoadModule module.

         ```Plain Text
         LoadModule php_module "C:/Users/Administrator/Downloads/php-8.3.1-Win32-vs16-x64/php8apache2_4.dll"
         <FilesMatch "\.(php|phtml|html|htm)$">
         SetHandler application/x-httpd-php
         </FilesMatch>
         PHPIniDir "C:/Users/Administrator/Downloads/php-8.3.1-Win32-vs16-x64"
         ```
         

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_102491810dd6051fe7f787565ade58f7.png) </span>

      2. In the `IfModule dir_module` module, change the value of the `DirectoryIndex` parameter to the following content.

         ```Plain Text
         index.php
         ```
         

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0705fdae67206f1229550d722394568f.png) </span>

      3. Press `Ctrl` +`S`to save the change and exit the file.


<span id=".6aqM6K-B546v5aKD"></span>
## Verify the environment


1. Log in to the target Windows instance. For more information, see [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Enter the htdocs folder of Apache HTTP Server and create a new file named test.php.

3. Right\-click the test.php file, click "Open with \> Notepad" to open the file, and enter the following content.

   ```Plain Text
   <?php
   phpinfo();
   ?>
   ```
   

4. Click the Windows icon in the lower\-left corner, select "Windows System," right\-click "Command Prompt", and then click "More \> Run as administrator."

5. In the Command Prompt dialog box, execute the following command to enter the directory where the Apache HTTP Server files are located.

   > Replace `httpd-2.4.58-win64-VS17\Apache24\bin` with the actual path to the Apache HTTP Server bin folder after extraction.   
   

   ```Plain Text
   cd httpd-2.4.58-win64-VS17\Apache24\bin
   ```
   

6. Execute the following command to start the server.

   ```Plain Text
   httpd.exe
   ```
   

7. In the address bar of the instance browser, enter the following address and press the Enter key.

   ```Plain Text
   http://localhost/test.php
   ```
   

   If the following output is displayed, the environment is set up successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb65e4f1ca0454e4d2fb43938aea7aa4.png) </span>
