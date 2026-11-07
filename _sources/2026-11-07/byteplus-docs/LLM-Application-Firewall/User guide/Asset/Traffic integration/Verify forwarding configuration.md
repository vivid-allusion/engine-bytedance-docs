---
title: "Verify forwarding configuration"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Verify_forwarding_configuration"
---

To ensure your LLM Application Firewall forwarding configuration is effective before modifying your public DNS, you can perform a local verification. This guide shows you how to use your local computer's hosts file to direct traffic to the firewall, allowing you to confirm correct setup and prevent potential business disruptions.

<span id="7851e894"></span>
## Background information

The hosts file is a system file with no extension that maps domain names to IP addresses. When a user enters a website domain name in the browser, the system automatically searches for the corresponding IP address in the hosts file. Once found, the system immediately opens the corresponding webpage; if the domain is not found, the system queries a DNS server to resolve the IP address.

Add an entry to your local hosts file that maps your website's domain to the IP address of the LLM Application Firewall. This allows you to verify that the firewall's forwarding configuration is working correctly before you change your public DNS records. This helps prevent website access issues caused by an incorrect forwarding configuration.

<span id="7ad75cdb"></span>
## Prerequisites


* The website you want to protect has been added to an LLM Application Firewall instance. For detailed instructions, refer to [Configure traffic integration parameters ](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_traffic_integration_parameters).

* The source CIDR blocks of the LLM Application Firewall have been added to the allowlist on your origin server. For details, refer to [Allow back-to-origin CIDR blocks](https://docs.byteplus.com/docs/LLM-Application-Firewall/Allow_back-to-origin_CIDR_blocks).

* The IP address of the LLM Application Firewall has been obtained. For information on how to obtain, refer to [How to obtain the origin IP address ranges for the LLM Application Firewall?](https://docs.byteplus.com/docs/LLM-Application-Firewall/FAQ_about_LLM_Application_Firewall#d3e9ad90)


<span id="4560eef7"></span>
## Step 1: Modify the local hosts file

Modify your local `hosts` file to map the protected domain name directly to the LLM Application Firewall's IP address. This forces requests from your local machine to be routed through the firewall for testing.

<span id="e7a48f80"></span>
### Method 1: Modify using a text editor


1. Find the `hosts` file. The following describes the location of the `hosts` file for different operating systems.

   * Linux：`/etc/hosts`。

   * Windows：`c:\Windows\System32\drivers\etc\hosts`。

   * Mac OS：`/etc/hosts`。

2. Use a terminal command window or a text editor to open the `hosts` file.

3. Add the LLM Application Firewall IP address (see diagram ①) and the domain name to be protected (see diagram ②) in the last row.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d67f4ae71f76494ca17bedf025cd22c8) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A space is required between the IP address and the domain name in the hosts file entry.   </div>
   

4. Save the file.


<span id="fe140fc0"></span>
### Method 2: Use the terminal command tool to modify

This example uses macOS.


1. Open Terminal in the Dock.

2. Enter `sudo vi /etc/hosts`.

3. Enter your administrator password when prompted (this is usually your lock screen password).

4. Press `i` to enter edit mode.

5. Add the LLM Application Firewall IP address (see diagram ①) and the protected domain name (see diagram ②) in the last row.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d67f4ae71f76494ca17bedf025cd22c8) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">There must be a space between the IP address and the domain name in the hosts file entry.   </div>
   

6. After completing the modifications, press the `Esc` key to exit edit mode.

7. Enter `:wq` to save and exit.


<span id="c84c0e8c"></span>
## Step 2: Verify whether the hosts modification was successful

Run `ping website domain` in the terminal, and access the protected domain (see figure ① below).


* If the resolved IP address is the LLM Application Firewall IP address specified in the `hosts` file (see figure ②), the modification is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/709228b3265441fb80d028ffb456ecc0) </span>

* If the resolved IP address is the origin server address, please try refreshing the local DNS cache.


<span id="a9e102bd"></span>
## Step 3: Verify that the forwarding configuration has taken effect

Access the protected domain locally. If access is successful, the configuration is successful.


* If the domain name is accessible, it means your forwarding configuration has taken effect. After restoring the `hosts` file, update your domain's public DNS record to point to the LLM Application Firewall. This routes your production traffic through the firewall for protection.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c196b8c459bb4ba0afdc118e0b61916f) </span>

* If the website is not working properly, this may indicate an issue with the domain name settings added in the LLM Application Firewall. We recommend checking the domain's forwarding configuration in the LLM Application Firewall console, resolving any issues, and then running the local verification again. For more access information, refer to [Configure traffic integration parameters ](https://docs.byteplus.com/docs/LLM-Application-Firewall/Configure_traffic_integration_parameters).
