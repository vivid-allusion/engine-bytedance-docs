---
title: "Configure HTTP Proxy"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Configure-http-proxy"
---

When the server is in an internal network environment and external network access must pass through a unified egress point, you need to use an HTTP proxy to access TOS object storage. This article describes the steps for configuring an HTTP proxy in tosutil.

<span id="7a2b2203"></span>
## Background Information

tosutil supports configuring the HTTP proxy using either environment variables or a configuration file. If both methods are configured, the system will prioritize the proxy specified in the configuration file. After configuration is complete, you can use the tosutil tool to access TOS object storage via a proxy.

<span id="8d9b26c4"></span>
## Configure HTTP Proxy via Configuration File


1. Execute the following command to open the tosutil configuration file.

   ```Bash
   vim ~/.tosutilconfig
   ```
   

2. In the tosutilconfig file, set the value of the `proxyUrl` parameter to the proxy address.

   The example is as follows:

   ```Bash
   proxyUrl=http://10.0.0.1:1234
   ```
   

3. Save and exit the tosutilconfig file.


<span id="51bd01fa"></span>
## Configuring HTTP Proxy via Environment Variables

This article outlines the steps for configuring an HTTP proxy in environment variables across different operating systems.


<Tabs>
<Tab zoneid="KLDE2e99IC" title="macOS/Linux">
<TabTitle>macOS/Linux</TabTitle>

When configuring the HTTP proxy in environment variables, different commands are required depending on the proxy server.


* If your proxy service does not require additional authentication, you do not need to include a username and password in the command.

   Open the terminal and enter the following command:

   ```Bash
   # HTTP Proxy
   export HTTP_PROXY=http://<Proxy Server IP>:<Port>
   export HTTP_PROXY=http://<Proxy Server Domain Name>:<Port>
   # HTTPS Proxy
   export HTTPS_PROXY=http://<Proxy Server IP>:<Port>
   export HTTPS_PROXY=http://<Proxy Server Domain Name>:<Port>
   ```
   

   The example is as follows:

   ```Bash
   # HTTP Proxy
   export HTTP_PROXY=http://10.0.0.1:1234
   export HTTP_PROXY=http://proxy.example.com:5678
   # HTTPS Proxy
   export HTTPS_PROXY=http://10.0.0.1:1234
   export HTTPS_PROXY=http://proxy.example.com:5678
   ```
   

* If authentication is enabled on your proxy server, you need to add your username and password to the command.

   Open the terminal and enter the following command:

   ```Bash
   # HTTP Proxy
   export HTTP_PROXY=http://<username>:<password>@<proxy server IP>:<port>
   export HTTP_PROXY=http://<username>:<password>@<proxy server domain>:<port>
   # HTTPS Proxy
   export HTTPS_PROXY=http://<username>:<password>@<proxy server IP>:<port>
   export HTTPS_PROXY=http://<username>:<password>@<proxy server domain>:<port>
   ```
   

   The example is as follows:

   ```Bash
   # HTTP Proxy
   export HTTP_PROXY=http://aaa:pass123@10.0.0.1:1234
   export HTTP_PROXY=http://aaa:pass123@proxy.example.com:1234
   # HTTPS Proxy
   export HTTPS_PROXY=http://aaa:pass123@10.0.0.1:5678
   export HTTPS_PROXY=http://aaa:pass123@proxy.example.com:5678
   ```
   


</Tab>
<Tab zoneid="No5YelTDu0" title="Windows">
<TabTitle>Windows</TabTitle>

When configuring the HTTP proxy in environment variables, different commands must be used depending on the proxy server.


* If your proxy service does not require additional authentication, you do not need to include a username and password in the command.

   Open the Command Prompt and enter the following command:

   ```Bash
   # HTTP Proxy
   setx HTTP_PROXY=http://<Proxy Server IP>:<Port>
   setx HTTP_PROXY=http://<Proxy Server Domain>:<Port>
   # HTTPS Proxy
   setx HTTPS_PROXY=http://<Proxy Server IP>:<Port>
   setx HTTPS_PROXY=http://<Proxy Server Domain>:<Port>
   ```
   

   The example is as follows:

   ```Bash
   # HTTP Proxy
   setx HTTP_PROXY=http://10.0.0.1:1234
   setx HTTP_PROXY=http://proxy.example.com:1234
   # HTTPS Proxy
   setx HTTPS_PROXY=http://10.0.0.1:1234
   setx HTTPS_PROXY=http://proxy.example.com:5678
   ```
   

* If authentication is enabled on your proxy server, you need to include the username and password in the command.

   Open the command prompt and enter the following command:

   ```Bash
   # HTTP Proxy
   setx HTTP_PROXY=http://<username>:<password>@<proxy server IP>:<port>
   setx HTTP_PROXY=http://<username>:<password>@<proxy server domain>:<port>
   # HTTPS Proxy
   setx HTTPS_PROXY=http://<username>:<password>@<proxy server IP>:<port>
   setx HTTPS_PROXY=http://<username>:<password>@<proxy server domain>:<port>
   ```
   

   The example is as follows:

   ```Bash
   # HTTP Proxy
   setx HTTP_PROXY=http://aaa:pass123@10.0.0.1:1234
   setx HTTP_PROXY=http://aaa:pass123@proxy.example.com:1234
   # HTTPS Proxy
   setx HTTPS_PROXY=http://aaa:pass123@10.0.0.1:1234
   setx HTTPS_PROXY=http://aaa:pass123@proxy.example.com:5678
   ```
   


</Tab>
</Tabs>
