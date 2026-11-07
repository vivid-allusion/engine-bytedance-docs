---
title: "Setting up multiple websites (Windows)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Setting_up_multiple_web_sites_Windows"
---

You can host multiple websites on a single ECS instance, enabling unified management and resource sharing for small\-scale sites, such as multiple WordPress blogs and static web pages.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* **Web environment deployment**

   An instance is purchased and a web environment is set up..

* **Software versions**

   * Operating system: In the example provided in this topic, Windows 2022 is used.

   * IIS: Internet Information Services (IIS) is a type of server software developed by Microsoft for hosting and providing web services. In the example provided in this topic, IIS 10.0 is used.

   * MySQL/MariaDB: A database management system. In the example provided in this topic, MySQL 8.0 is used.

   * PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.4 is used.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

This topic describes how to set up two static web pages on an ECS instance running the Windows operating system.

<span id=".5q2l6aqk5LiA77ya5Yib5bu66Z2Z5oCBV2Vi6aG16Z2i5paH5Lu2"></span>
### Step 1: Create a static Web page file


1. Log in to the Windows instance where a web environment is set up. [Learn more](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Enter the `C:\wwwroot` folder.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you install the IIS web server, this folder is created by default as the root directory of the server.   </div>
   

3. Create the `windows-page-1` and `windows-page-2` folders.

4. Click the "View" button in the top menu bar, and check "File name extensions".

5. Create site page files.

   * Site page 1:

      1. In the `windows-page-1` folder, create a text file named `page1.php`.

      2. Click the "Yes" button in the pop\-up window to complete the creation process.

      3. Open the `page1.php` file with Notepad, and enter the following content.

         ```Plain Text
         <?php
           echo "Welcome to Test Page 1";
         ?>
         ```
         

      4. Save and exit the file.

   * Site page 2:

      1. In the `windows-page-2` folder, create a text file named `page2.php`.

      2. Click the "Yes" button in the pop\-up window to complete the creation process.

      3. Open the `page2.php` file with Notepad, and enter the following content into it.

         ```Plain Text
         <?php
           echo "Welcome to Test Page 2";
         ?>
         ```
         

      4. Save and exit the file.


<span id=".5q2l6aqk5LqM77ya5Yib5bu6V2Vi56uZ54K5"></span>
### Step 2: Create a website


1. Log in to the Windows instance where the web environment is set up. For more information, see [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Click the "Start" icon, and then click the "Server Manager" button.

3. In the server manager window, click "Tools \> Internet Information Services (IIS) Manager".

4. In the left pane of the "Internet Information Services (IIS) Manager" window, select "<Host Name\> (e.g., `IV-BXJDxxxxx`) \> Sites". Then, create and configure the site information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example provided in this topic, two test sites and their web content are created for reference only. In actual site deployment scenarios, you need to configure real domain names, hostnames, physical paths, and other related information.   </div>
   

   * Test site 1

      1. Click the "Add Website" button.

      2. In the "Add Website" window, configure information described in the following table.

         Parameter descriptions:

         
         |Parameter |Description |Sample value |
         |---|---|---|
         |Site name (S) |The name used to identify and recognize a website. |windows\-page\-1 |
         |Application pool (L) |Each website can be associated with a specific application pool, which determines the runtime environment of the website application and isolates its resources from those of other applications. |windows\-page\-1 |
         |Physical path (P) |The root directory or content storage location for the website. |C:\wwwroot\windows\-page\-1 |
         |Host name |You can configure different hostnames (domain names) for multiple websites on the same IP address. This allows different websites to be accessed based on different domain names. |winpage1.com |
         

      3. Click "OK" to complete the creation.

   * Test site 2

      1. Click the "Add Website" button.

      2. In the "Add Website" window, configure information described in the following table.

         Parameter descriptions:

         
         |Parameter |Description |Sample value |
         |---|---|---|
         |Site name (S) |The name used to identify and recognize a website. |windows\-page\-2 |
         |Application pool (L) |Each website can be associated with a specific application pool, which determines the runtime environment of the website application and isolates its resources from those of other applications. |windows\-page\-2 |
         |Physical path (P) |The root directory or content storage location for the website. |C:\wwwroot\windows\-page\-2 |
         |Host name |You can configure different hostnames (domain names) for multiple websites on the same IP address. This allows different websites to be accessed based on different domain names. |winpage2.com |
         

      3. Click "OK" to complete the creation.


<span id=".5q2l6aqk5LiJ77ya6YWN572u5pys5ZywaG9zdHPvvIjlj6_pgInvvIk="></span>
### Step 3: Configure the local hosts file (optional)

The domain name of the test site created in this topic is not a valid domain name. Other PCs that need to access the test site must configure the IP mapping in their respective hosts file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the "Host Name" value you specified when you create a site in the IIS web server is a valid domain name, skip this step.</div>



1. Log in to the local PC that needs to access the test site.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example provided in this topic, another Windows instance that can access the Internet (not used for hosting a website) is used.   </div>
   

2. Go to the `C:\Windows\System32\drivers\etc` directory.

3. Back up the `hosts` file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you copy and save the <code>hosts</code> file as a backup. After the test is complete, you can use the backup to restore the <code>hosts</code> file to its original state.   </div>
   

4. Open the hosts file with Notepad, and add the following content at the end of the file.

   ```Plain Text
   <ECS instance Elastic IP (EIP)> winpage1.com
   <ECS instance Elastic IP (EIP)> winpage2.com
   ```
   

5. Save and close the file.

6. Click the "Start" icon, and select "Windows Administrative Tools \> Command Prompt".

7. Execute the following command in the command line to make the hosts configuration take effect immediately.

   ```Plain Text
   ipconfig /flushdns
   ```
   


<span id=".5q2l6aqk5Zub77ya6K6_6ZeuV2Vi6aG16Z2i"></span>
### Step 4: Access the web page


1. Log in to the local PC that has the local hosts file configured.

2. Access the test web page in the browser and verify whether it can be accessed.

   * Web page 1

      ```Plain Text
      winpage1.com/page1.php
      ```
      

   * Web page 2

      ```Plain Text
      winpage2.com/page2.php
      ```
      

3. At this point, multiple websites are set up.


<span id=".5q2l6aqk5LqU77ya5Li6572R56uZ5ZCv55SoIEhUVFBT77yI5Y-v6YCJ77yJ"></span>
### Step 5: Enable HTTPS for the website (optional)

When a user accesses your website over the HTTP protocol, the browser warns the user that the connection is not secure. We recommend that you enable HTTPS secure communication for your website. This ensures encrypted data transmission between users and your website, effectively defending against network hijacking, information leakage, and other threats.

To enable HTTPS, you need to deploy an SSL certificate on your website.
