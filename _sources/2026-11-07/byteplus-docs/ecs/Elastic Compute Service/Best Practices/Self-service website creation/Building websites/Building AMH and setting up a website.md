---
title: "Building AMH and setting up a website"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Building-an-AMH-website"
---

AMH is a Linux server and virtual host management system that enables web\-based server control and management. This topic describes how to set up an AMH website for a production environment on the Linux operating system.

<span id=".6L2v5Lu254mI5pys"></span>
## Software versions


* Operating system: In the example provided in this topic, CentOS 7.6 is used.

* PHP: A server\-side scripting language embedded in HTML documents. In the example provided in this topic, PHP 7.0.33 is used.

* AMH: In the example provided in this topic, AMH 6.2 is used.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Linux instance is purchased, and the associated security group has an inbound rule configured with the TCP protocol and port 8888, as shown in the following table.


|Direction |Protocol/Application |Port/Range |Source address |
|---|---|---|---|
|Inbound |TCP |8888 |0.0.0.0/0 |


<span id=".56ys5LiA5q2l77ya5LiL6L295bm25a6J6KOFQU1I"></span>
## Step 1: Download and install AMH


1. Execute the following command to download AMH.

   ```Plain Text
   wget http://amh.sh/amh.sh && bash amh.sh
   ```
   

   The following output is displayed:

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_89762b1b56293217a359c419fffbbe43.png) </span>

2. Enter `1` and press Enter to complete the installation.

3. After the installation is successful, the following output is displayed. Record the AMH address and the usernames and passwords for the AMH administrator and the database.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4a1a26e64e9a8ae76dc9ddd12fc38f0f.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you forget your password, you can execute the <code>amh amh-6.2 admin change_amh_password new_pass</code> command (replace new_pass with your desired password) to specify a new password.   </div>
   

<span id=".56ys5LqM5q2l77ya6K6_6Zeu5bm26YWN572uQU1I"></span>
## Step 2: Access and configure AMH


1. Enter `http://<ECS instance EIP>:8888` in the local browser to access AMH.

   If the following output is displayed, AMH is set up successfully.

2. Enter the account and password of the AMH administrator as prompted.

   If the following output is displayed, the login is successful.

3. Configure the virtual host.

   1. Click lnmp01 in the "LNMP Environment List".

   2. The virtual host configuration page is displayed. Specify a value for the "Host identifier domain" and "Associated domain" parameters and retain the default settings for other parameters. As shown in the following figure, click the "Save" button.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you use an IP address to access the virtual host, you can enter the IP address in both the "Host identifier domain" and "Associated domain" fields.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you use a domain name to access the virtual host, make sure that an ICP filing is complete for the domain name and the domain name is resolved to your ECS instance.      </div>
      

4. Configure a database.

   1. Follow the path below and click the "Download and install" button.

   2. After the installation is complete, click "Database \> phpAdmin management", and then click the "phpAdmin" button.

   3. Go to the database homepage and click the "Account" button in the right navigation bar.

   4. Click the "Add user account" button. Configure the parameters as shown in the following figure, select "Create a database with the same name as the user and grant all database permissions to the user", and then click the "Execute" button at the bottom to create the database and account.

5. Configure FTP.

   1. Follow the path below and click the "Manage" button.

   2. Select all options and click the "OK" button

   3. After the installation is complete, click "FTP Management \> Account Management" and add a new FTP account.

   4. Enter the account information and click the "Save" button.

   5. Click the "File Management" button corresponding to the account.

   6. Enter the FTP username and password, and then click the "Log in" button.

   7. Select the default homepage files `ErrorPages` and `index.html` in AMFTP, and then click the "Delete" button, as shown in the following figure.

   8. Upload website files. In the example provided in this topic, [DEDECMS files](https://www.dedecms.com/download) are uploaded. You can upload system files based on your business requirements.

   9. Select the DEDECMS files, and click the "Intelligent Extraction" button.


<span id=".56ys5LiJ5q2l77ya5a6J6KOF572R56uZ"></span>
## Step 3: Install the website


1. Use a local browser to access the domain name specified in [Step 2: Access and configure AMH](https://docs.byteplus.com/en/docs/ecs/Building-an-AMH-website#.56ys5LqM5q2l77ya6K6_6Zeu5bm26YWN572uQU1I), and install the DEDECMS content management system.

2. Select "I have read and agree to this agreement", and then click the "Continue" button.

3. Perform an environment check, and then click the "Continue" button.

4. Use the database created in [Step 2: Access and configure AMH](https://docs.byteplus.com/en/docs/ecs/Building-an-AMH-website#.56ys5LqM5q2l77ya6K6_6Zeu5bm26YWN572uQU1I), and configure the database information.

5. Configure the administrator username and password, and then click the "Continue" button.

6. After the installation is complete, the following output is displayed, indicating that the installation is successful.

7. Click the "Visit website homepage" button to access the website homepage.

8. Click the "Log in to website backend" button to access the backend management page of the website.


<span id=".56ys5Zub5q2l77yI5Y-v6YCJ77yJ77ya5Li6572R56uZ5ZCv55SoIEhUVFBT"></span>
## Step 4 (Optional): Enable HTTPS for the website.

When a user accesses your website over the HTTP protocol, the browser warns the user that the connection is not secure. We recommend that you enable HTTPS secure communication for your website. This ensures encrypted data transmission between users and your website, effectively defending against network hijacking, information leakage, and other threats.

To enable HTTPS, you need to deploy an SSL certificate on your website.
