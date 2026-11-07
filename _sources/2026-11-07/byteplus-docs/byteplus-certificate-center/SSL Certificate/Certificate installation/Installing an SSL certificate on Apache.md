---
title: "Installing an SSL certificate on Apache"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-install-certificate-on-apache"
---

After the certificate is issued, you can download the certificate from the BytePlus Certificate Center console. After obtaining the certificate, you must install it on the server to enable HTTPS connections. This tutorial will guide you through the process of installing an SSL certificate on your Apache server.

<span id="prerequisites"></span>
## Prerequisites


* You have submitted an SSL certificate request through BytePlus Certificate Center and the SSL certificate has been issued.

   If you have not submitted an SSL certificate request, please refer to [Quick start](https://docs.byteplus.com/byteplus-certificate-center/docs/get-started-with-ssl-certificate-service).

* Port 443 of your server is open.

   The default port for HTTPS communication is 443, so the server can only handle client\-initiated HTTPS connection requests if port 443 is open.


<span id="environment"></span>
## Environment

This tutorial uses the following environment as an example to introduce the relevant steps:


* Server:

   * Operating system: Ubuntu 22.04 64\-bit

   * Web server software: Apache/2.4.41

   * Installation directory of the web server software: `/etc/apache2`

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The actual configuration may vary depending on the server environment. In this case, please refer to the actual environment, and this document is for reference only.   </div>
   

* Example domain: `ssl.example.com`


<span id="tutorial-overview"></span>
## Tutorial overview

This tutorial will guide you through modifying the `<VirtualHost>` configuration in the `apache2.conf` configuration file to enable port 443 listening for the domain and associate it with the corresponding certificate.

<span id="step-1-download-the-certificate-to-your-local-computer"></span>
## Step 1: Download the certificate to your local computer

For the issued SSL certificate, you can download the certificate package compatible with the Apache server to your local computer from the BytePlus Certificate Center console.

For specific operations on downloading the certificate package, please refer to [Downloading an SSL certificate](https://docs.byteplus.com/byteplus-certificate-center/docs/downloading-certificates).

After downloading the **Apache** certificate package, extract the certificate package to your local computer.

The certificate package is named `<CommonName>_apache`. Here, `<CommonName>` represents the domain name to which the certificate is issued.

After extraction, you will obtain the following certificate files:


* `<CommonName>_chain.crt`: Certificate chain file.

* `<CommonName>_public.crt`: Certificate file.

* `<CommonName>.key`: Private key file.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your SSL certificate request used a CSR uploaded manually by you and you did not provide the private key, the extracted files will not include the private key file. In this case, you need to prepare the private key file yourself to complete the subsequent configuration.</div>


<span id="step-2-upload-the-certificate-to-the-apache-server"></span>
## Step 2: Upload the certificate to the Apache server

There are many ways to upload local files to a remote server. This tutorial uses the `scp` command as an example to describe how to upload the certificate from a local Windows computer to an Apache server.


1. Log in to the Apache server remotely.

2. Create a folder named `cert` in the Apache installation directory to store the certificate.

   The Apache installation directory may vary depending on the Apache version. Please refer to your Apache version. In this tutorial, the Apache installation directory is `/etc/apache2`.

   ```Plain
   cd /etc/apache2
   mkdir cert
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can use the <code>find / -name apache2.conf</code> command to query the path of the <code>apache2.conf</code> configuration file. The path is the Apache installation directory.   </div>
   

3. Open the Shell tool on your local computer.

   For example, on the Windows 10 operating system, right\-click the Start icon in the lower\-left corner of the desktop, and then click **Windows PowerShell**.

4. Use the `scp` command to upload the certificate files to the server.

   ```Shell
   scp <path of the file on your local computer> root@<remote server IP>:/etc/apache2/cert
   ```
   

   After executing the `scp` command, enter the password of the root account of the remote server according to the command prompt.

   Examples:

   * Upload the certificate chain file:

      ```PowerShell
      scp C:\ssl.example.com_chain.crt root@<remote server IP>:/etc/apache2/cert
      ```
      

   * Upload the certificate file:

      ```PowerShell
      scp C:\ssl.example.com_public.crt root@<remote server IP>:/etc/apache2/cert
      ```
      

   * Upload the private key file:

      ```PowerShell
      scp C:\ssl.example.com.key root@<remote server IP>:/etc/apache2/cert
      ```
      

5. Confirm that the files are uploaded successfully.

   On the Apache server, execute the `ll /etc/apache2/cert` command to list the files in the `cert` directory.

   If the file list includes the certificate chain file, certificate file, and private key file, the certificate has been uploaded successfully.


<span id="step-3-configure-the-certificate-on-apache"></span>
## Step 3: Configure the certificate on Apache


1. Enable the `mod_ssl` module.

   In Apache, the `mod_ssl` module is used to enable HTTPS.

   ```Plain
   a2enmod ssl
   ```
   

2. Reload the Apache service.

   After enabling the `mod_ssl` module, you need to restart Apache for the configuration to take effect.

   ```Plain
   systemctl restart apache2
   ```
   

3. Add `<VirtualHost>` configuration.

   ```Plain
   vim /etc/apache2/sites-available/ssl.example.com.conf
   ```
   

   Add the following content to the configuration file:

   ```Plain
   <VirtualHost *:443>
      # Website domain
      ServerName ssl.example.com
      # Website root directory, same as the configuration for port 80
      DocumentRoot /var/www/ssl.example.com
      
      # Enable SSL
      SSLEngine on
      # Certificate chain file path
      SSLCertificateChainFile /etc/apache2/cert/ssl.example.com_chain.crt 
      # Certificate file path
      SSLCertificateFile /etc/apache2/cert/ssl.example.com_public.crt
      # Private key file path
      SSLCertificateKeyFile /etc/apache2/cert/ssl.example.com.key
   </VirtualHost>
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After entering the <code>vim</code> editing page, press the <code>i</code> key to enter the editing mode.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After editing, press the <code>Esc</code> key to exit the editing mode, then enter <code>:wq</code> to save changes and exit the <code>vim</code> editing page.   </div>
   

4. Enable the newly added `<VirtualHost>` configuration.

   ```Shell
   a2ensite ssl.example.com.conf
   ```
   

5. Check if there are any syntax errors in the configuration file.

   ```Plain
   apache2ctl configtest
   ```
   

   If `Syntax OK` is returned, there are no syntax errors. If there are syntax errors, you can modify the configuration according to the prompts.

6. Reload the Apache service.

   ```Shell
   systemctl reload apache2
   ```
   


<span id="step-4-verify-if-the-certificate-is-configured-successfully"></span>
## Step 4: Verify if the certificate is configured successfully

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before performing the verification, make sure that port 443 is open on the server. If your server does not allow access to port 443 due to security group, firewall, or other policies, please modify the corresponding policies first.</div>


Open a browser on your local computer and access the domain in HTTPS format: `https://ssl.example.com`.

If the connection is successfully established, a lock icon will appear in the browser address bar, indicating that the connection is secure.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_573e1740e2cb7bdca694077296380db8.png) </span>

You can click on the lock icon to view connection details, such as obtaining certificate information.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_07df7f59026b7095f76d0e1b0c82d423.png) </span>

<span id="optional-force-http-requests-to-redirect-to-https"></span>
## (Optional) Force HTTP requests to redirect to HTTPS

After enabling HTTPS communication for your website, you can also modify the `<VirtualHost>` configuration to force HTTP requests from end users to redirect to HTTPS requests, ensuring that end users always access your web service via the HTTPS protocol.


1. Edit the configuration file.

   ```Shell
   vim /etc/apache2/sites-available/ssl.example.com.conf
   ```
   

2. Add the following content to the end of the configuration file:

   ```Shell
   <VirtualHost *:80>
       ServerName ssl.example.com
       Redirect / https://ssl.example.com/
   </VirtualHost>
   ```
   

   The modified content is shown in the following image.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_acc17da35db22005a68bbecd56427594.png) </span>

3. Save changes and exit the configuration file.

4. Check if there are any syntax errors in the configuration file.

   ```Plain
   apache2ctl configtest
   ```
   

   If `Syntax OK` is returned, there are no syntax errors. If there are syntax errors, you can modify the configuration according to the prompts.

5. Reload the Apache service.

   ```Shell
   systemctl reload apache2
   ```
   

6. Open a browser on your local computer and access the domain in HTTP format: `http://ssl.example.com`.

   If the address is automatically converted to HTTPS format, it means that the HTTP request has been forced to redirect to HTTPS request.
