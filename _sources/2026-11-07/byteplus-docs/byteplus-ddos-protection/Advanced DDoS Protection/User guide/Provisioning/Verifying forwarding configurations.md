---
title: "Verifying forwarding configurations"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-verifying-the-forwarding-configurations"
---

After adding domain names or ports to the instance of Advanced DDoS Protection, the incoming traffic will be redirected to the instance for filtration, and then be forwarded to your origin server. To ensure the stability of your service, it is recommended to verify whether the forwarding configurations take effect.

<span id="957cbdf8"></span>
## Background information


* You can verify website services accessed by domain name in two ways.

   * Modify the local hosts file and then access your website using the ping command.

   * Use the CNAME record to access the origin server.

* For non\-website services accessed via IP addresses (such as gaming services), you can directly access the IP address of Advanced DDoS Protection for verification.


<span id="69d259bd"></span>
## Prerequisites


* Add one or more forwarding rules.

* Add the CIDR blocks for the protection service to your origin server's allowlist.


<span id="ccbaf290"></span>
## Modify the local hosts file to access the origin server


1. Modify the local file `hosts` so that local requests to the origin server can be routed through the IP address of the Advanced DDoS Protection instance.

   1. Locate the hosts file. The paths to the file for different operating systems are as follows.

      * Linux:`/etc/hosts`.

      * Windows: `c:\Windows\System32\drivers\etc\hosts`.

      * Mac OS: `/etc/hosts`.

   2. Use a text editor to open the file.

   3. Add the IP address of the Advanced DDoS Protection instance and the domain name of the website to the last line of the file, with a space in between.

      For example, if the IP address of the Advanced DDoS Protection instance is `192.1.1.1`, and the protected domain name is `www.test.com`, you can add `192.1.1.1 www.test.com` to the last line of the file.

   4. Save the file.

2. Run the Command Prompt window, and execute `ping domain name` to access the origin server.

   For example, execute `ping www.test.com`.

   * If the output includes the IP address of the Advanced DDoS Protection instance (for example, `192.1.1.1`), the configuration is working. Proceed to **step 3** for further verification.

   * If the output does not contain `192.1.1.1`, refresh the local DNS cache by running `ipconfig/flushdns` and try again.

3. Access your origin server using the domain name.

   If the website is accessible, the configuration is successful.


<span id="e6920808"></span>
## Use the CNAME record to access the origin server

After you add a domain name, the system provides a CNAME record. This record is intended for redirecting network traffic to the Advanced DDoS Protection instance. To verify the effectiveness of the configuration, you can access your origin server using the provided CNAME record.

<span id="8949389b"></span>
## Use the instance IP address to access the origin server

For this example, assume the following: the instance IP is `192.1.1.1`, the origin server IP is `192.2.2.2`, and a forwarding rule is configured for port `1234` on both.


* You can verify the port forwarding configuration by executing the command telnet 192.1.1.1 1234 from your local system. A successful connection confirms that port forwarding is configured correctly.

* Additionally, if your client application can connect directly to an IP address, you can test the configuration by using the IP address of the Advanced DDoS Protection instance in your client.
