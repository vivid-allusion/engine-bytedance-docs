---
title: "Verifying the configurations of your domain name"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Verifying_website_settings"
---

After adding a domain name using CNAME method, the WAF instance will forward requests received on related ports to the corresponding ports on your origin server. To ensure service stability, it is recommended that you verify the forwarding effects after completing the access configuration. This document describes how to verify whether the forwarding configuration takes effect on a local computer.

<span id="fb976e74"></span>
## Background information

The `hosts` file is a system file without an extension. It stores the mappings between commonly used website domain names and their IP addresses. When a user enters a website domain name in a browser, the system automatically searches for the corresponding IP address in the `hosts` file. Once found, the system immediately opens the corresponding web page. If the IP address is not found, the system submits the domain name to the DNS server for IP address resolution.

By adding valid DNS resolution records to the hosts file on a local computer, you can direct the domain name resolution of the website to the WAF's IP address. This allows you to access the protected domain name from your local computer, verifying whether the domain name access settings added in WAF are correct and effective, and avoiding abnormal website access caused by incorrect domain name access configurations.

<span id="7955eea3"></span>
## Prerequisites


* You have added the domain names to the WAF instance. For more details, see [Adding a domain name to a Cloud WAF instance](https://docs.byteplus.com/docs/waf/Allowing_back-to-origin_CIDR_blocks).

* The back\-to\-origin IP addresses are in the allowlist of the origin server. For more details, see [Adding the back-to-origin CIDR blocks to your allowlist](https://docs.byteplus.com/docs/waf/Modifying_the_DNS_record).

* You have obtained the IP address of the WAF instance. For more details, see [How to obtain the IP address of WAF when verifying whether the forwarding is effective?](https://docs.byteplus.com/docs/waf/FAQ-about-web-application-firewall#b226e896)


<span id="194cec6c"></span>
## Step 1: Modifying your local hosts file

Modify the `hosts` file to allow local requests to the origin server to pass through the WAF instance.

<span id="dc1e2218"></span>
### Method 1: Modifying with a text editor


1. Locate the `hosts` file. The paths of the `hosts` file vary by operating systems:

   * Linux：`/etc/hosts`.

   * Windows：`c:\Windows\System32\drivers\etc\hosts`.

   * Mac OS：`/etc/hosts`.

2. Open the `hosts` file using a text editor.

3. Add the WAF IP address (① in the figure below) and the protected domain name (② in the figure below) to the last line.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d67f4ae71f76494ca17bedf025cd22c8~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">There must be a space between the WAF IP address and the website domain name.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To obtain the WAF IP address, you can refer to <a href="https://docs.byteplus.com/docs/waf/FAQ-about-web-application-firewall#b226e896">How to obtain the IP address of WAF when verifying whether the forwarding is effective?</a>   </div>
   

4. Save the file.


<span id="b63647f2"></span>
### Method 2: Using a terminal command tool

The following uses Mac OS as an example.


1. Open **Terminal** from the **Dock**.

2. Enter `sudo vi /etc/hosts`.

3. Enter the administrator password as prompted, which is the lock screen password.

4. Enter `i` to enter editing mode.

5. Add the WAF IP address (① in the figure below) and the protected domain name (② in the figure below) to the last line.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d67f4ae71f76494ca17bedf025cd22c8~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">There must be a space between the WAF IP address and the website domain name.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To obtain the WAF IP address, you can refer to <a href="https://docs.byteplus.com/docs/waf/FAQ-about-web-application-firewall#b226e896">How to obtain the IP address of WAF when verifying whether the forwarding is effective?</a>   </div>
   

6. After the modification is complete, press the `Esc` key to exit editing mode.

7. Enter `:wq` to save and exit.


<span id="2c7109b5"></span>
## Step 2: Verifying whether the modifications are successful

Run `ping website domain name` in the terminal to access the protected domain name (① in the figure below).


* If the parsed IP address is the WAF IP bound in the `hosts` file (② in the figure below), the modification is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/709228b3265441fb80d028ffb456ecc0~tplv-goo7wpa0wc-image.image) </span>

* If the parsed IP address is the origin server address, try refreshing the local DNS cache.


<span id="c3ddf445"></span>
## Step 3: Verifying whether the website configuration is effective

Directly access the protected domain name locally, and check whether your website can be accessed normally.


* If the domain name can be accessed normally, it indicates that the configuration takes effect. It is recommended that you restore the `hosts` file and modify the DNS resolution of the domain name to resolve the business traffic to WAF for protection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd8afd3d11e246608e3ae98c3732181b~tplv-goo7wpa0wc-image.image) </span>

* If the website cannot be accessed, it is likely that some parameters have been improperly configured. You should check the domain name settings in the WAF. After rectifying the issues, conduct the local verification again. For more details about configuring domain name parameters, see [Adding a domain name to a Cloud WAF instance](https://docs.byteplus.com/docs/waf/Allowing_back-to-origin_CIDR_blocks).
