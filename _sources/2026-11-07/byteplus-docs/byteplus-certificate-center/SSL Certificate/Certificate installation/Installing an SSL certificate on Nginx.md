---
title: "Installing an SSL certificate on Nginx"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-install-certificate-on-nginx"
---

After the SSL certificate is issued, you can download the certificate from the BytePlus Certificate Center console. After obtaining the certificate, you must install it on the server to enable HTTPS connections. This tutorial will guide you through the process of installing an SSL certificate on your Nginx server.

<span id="prerequisites"></span>
## Prerequisites


* You have submitted an SSL certificate request through BytePlus Certificate Center and the SSL certificate has been issued.

   If you haven't submitted an SSL certificate request yet, please refer to [Quick start](https://docs.byteplus.com/byteplus-certificate-center/docs/get-started-with-ssl-certificate-service).

* Port 443 of your server is open.

   The default port for HTTPS communication is 443, so the server can only handle client\-initiated HTTPS connection requests if port 443 is open.


<span id="environment"></span>
## Environment

This tutorial uses the following environment as an example to introduce the relevant operations:


* Server:

   * Operating system: Ubuntu 22.04 64\-bit

   * Web server: Nginx version 1.18.0

   * Installation directory of the web server: `/etc/nginx`

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Different server types may result in different configuration paths compared to the description in this article. In this case, please refer to the actual environment, and this tutorial is for reference only.   </div>
   

* Example domain: `ssl.example.com`

* Path of the virtual host configuration file corresponding to the domain: `/etc/nginx/conf.d/ssl.example.com.conf`


<span id="tutorial-overview"></span>
## Tutorial overview

This tutorial will guide you through modifying the `nginx.conf` configuration file's `server{}` configuration to enable port 443 listening for the domain and associate the corresponding certificate.

<span id="step-1-download-the-certificate-to-your-local-computer"></span>
## Step 1: Download the certificate to your local computer

For issued SSL certificates, you can download the Nginx\-compatible certificate package to your local computer from BytePlus Certificate Center. For detailed steps on downloading the certificate package, please refer to [Downloading an SSL certificates](https://docs.byteplus.com/byteplus-certificate-center/docs/downloading-certificates).

After downloading the Nginx certificate package, extract the certificate package to your local computer.

The certificate package is named `<CommonName>_nginx`. `<CommonName>` represents the domain name to which the certificate is issued.

After extraction, you will obtain the following files:


* `<CommonName>.pem`: Certificate file.

* `<CommonName>.key`: Private key file.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If your SSL certificate request used a CSR uploaded manually by you and you did not provide the private key, the extracted files will not include the private key file. In this case, you need to prepare the private key file yourself to complete the subsequent configuration.</div>


<span id="step-2-upload-the-certificate-to-the-nginx-server"></span>
## Step 2: Upload the certificate to the Nginx server

There are many ways to upload local files to a remote server. This tutorial uses the `scp` command as an example to demonstrate how to upload the certificate to the Nginx server.


1. Log in to the Nginx server remotely.

2. Create a folder named `cert` in the Nginx installation directory to store the certificate.

   The Nginx installation directory may vary depending on the version of Nginx you are using. In this tutorial, the default installation directory for Nginx is `/etc/nginx`.

   ```Shell
   cd /etc/nginx
   mkdir cert
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can use the <code>find / -name nginx.conf</code> command to find the path of the <code>nginx.conf</code> configuration file. This path is the Nginx installation directory.   </div>
   

3. Open the Shell tool on your local computer.

   For example, on Windows 10, right\-click the Start icon in the lower\-left corner of the desktop, and then click **Windows PowerShell**.

4. Use the `scp` command to upload the certificate files to the server.

   ```Shell
   scp <path of the file on your local computer> root@<remote server IP>:/etc/nginx/cert
   ```
   

   After executing the `scp` command, enter the password for the root account of the remote server as prompted.

   Examples:

   * Upload the certificate file:

      ```Shell
      scp C:\ssl.example.com_cert\ssl.example.com.pem root@<remote server IP>:/etc/nginx/cert
      ```
      

   * Upload the private key file:

      ```Shell
      scp C:\ssl.example.com_cert\ssl.example.com.key root@<remote server IP>:/etc/nginx/cert
      ```
      

5. Verify if the files are uploaded successfully.

   On the Nginx server, execute the `ll cert` command to list the files in the `cert` directory.

   If the file list includes the certificate file and the private key file, it means that the certificate has been uploaded successfully.


<span id="step-3-configure-the-certificate-on-nginx"></span>
## Step 3: Configure the certificate on Nginx

You need to modify the virtual host configuration `server{}` of Nginx. The location of `server{}` may vary depending on your actual environment.

In this tutorial, `server{}` is located in the `ssl.example.com.conf` configuration file in the `/etc/nginx/conf.d` directory.


1. Edit the configuration file.

   ```Shell
   vim /etc/nginx/conf.d/ssl.example.com.conf
   ```
   

2. Add the following SSL configuration to the configuration file.

   ```Shell
   server {
       ## Required SSL configuration
       listen 443 ssl; # Enable port 443 listening
       server_name ssl.example.com; # The domain being listened to
       ssl_certificate /etc/nginx/cert/ssl.example.com.pem; # Certificate file path
       ssl_certificate_key /etc/nginx/cert/ssl.example.com.key; # Private key file path
       
       ## Optional SSL configuration
       # ssl_session_timeout 5m; # Time for which the client can reuse session parameters
       # ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4; # Allowed encryption suite types
       # ssl_protocols TLSv1.1 TLSv1.2 TLSv1.3; # Allowed TLS protocol types
       # ssl_prefer_server_ciphers on; # Whether to prefer the server's encryption suite when negotiating encryption algorithms, rather than the client's browser's encryption suite
       
       ## Website configuration, consistent with the configuration related to port 80
       root html; 
       index index.html index.htm;
       location / {
           root html;
           index index.html index.htm;
       }
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After entering the <strong>vim</strong> editing page, press the <strong>I</strong> key to enter the editing mode.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After editing, press the <strong>Esc</strong> key to exit the editing mode, and then enter <code>:wq</code> to save and exit the <strong>vim</strong> editing page.   </div>
   

3. Check if there are any syntax errors in `nginx.conf`.

   ```Shell
   nginx -t
   ```
   

   If the message `syntax is ok` is returned, it means there are no syntax errors. If there are syntax errors, you can modify the configuration again based on the prompts.

4. Reload the Nginx service.

   ```Shell
   /etc/init.d/nginx reload
   ```
   


<span id="step-4-verify-if-the-certificate-is-configured-successfully"></span>
## Step 4: Verify if the certificate is configured successfully

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before performing the verification, make sure that port 443 is open on the server. If your server does not allow access to port 443 due to security group or firewall policies, please modify the corresponding policies first.</div>


Open a browser on your local computer and access the domain in HTTPS format: `https://ssl.example.com`.

If the connection is successfully established and the browser's address bar displays a lock icon, it means that the connection is secure. You can click on the lock icon to view the connection details, which include the certificate information.

<span id="optional-force-http-requests-to-redirect-to-https"></span>
## (Optional) Force HTTP requests to redirect to HTTPS

After enabling HTTPS communication on your website, you can modify the `server{}` configuration to force HTTP requests from end users to redirect to HTTPS, ensuring that end users always access the web service via the HTTPS protocol.


1. Edit the configuration file.

   ```Shell
   vim /etc/nginx/conf.d/ssl.example.com.conf
   ```
   

2. Locate the configuration for port 80 in the configuration file and add the following line of code:

   `rewrite ^(.*)$ https://$host$1;`

   This line of code uses the `rewrite` directive to redirect HTTP requests to HTTPS.

   ```Shell
   server {
       listen 80;
       server_name ssl.example.com; # The domain being listened to
       rewrite ^(.*)$ https://$host$1; # Add this line of code
       location / {
           index index.html index.htm;
       }
   }
   ```
   

3. Save changes and exit the configuration file.

4. Check if there are any syntax errors in `nginx.conf`.

   ```Shell
   nginx -t
   ```
   

   If the message `syntax is ok` is returned, it means there are no syntax errors. If there are syntax errors, you can modify the configuration again based on the prompts.

5. Reload the Nginx service.

   ```Shell
   sudo /etc/init.d/nginx reload
   ```
   

6. Open a browser on your local computer and access the domain in HTTP format: `http://ssl.example.com`.

   If the address is automatically converted to HTTPS format, it means that HTTP requests have been forced to redirect to HTTPS.
