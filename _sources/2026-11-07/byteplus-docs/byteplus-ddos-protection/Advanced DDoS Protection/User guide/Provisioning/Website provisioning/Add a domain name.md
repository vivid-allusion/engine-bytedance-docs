---
title: "Add a domain name"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-adding-a-domain-name-to-the-instance"
---

To safeguard your website services from DDoS attacks, you can add your domain name to the Advanced DDoS Protection service. This guide provides step\-by\-step instructions for provisioning your website, which involves configuring your domain, protocol type, and origin server settings. This setup ensures that traffic is filtered through our scrubbing centers, allowing only legitimate requests to reach your service.

<span id="7f3a9c76"></span>
## Before you begin

Create an instance of BytePlus Advanced DDoS Protection.

<span id="78799e02"></span>
## Precautions

Both WebSocket and WebSockets protocols are supported and enabled by default.

<span id="4d42da8f"></span>
## Procedure


1. Log in to the [BytePlus Advanced DDoS Protection Console](https://console.byteplus.com/ddos-protection/advance/instances).

2. In the left\-side navigation pane, choose **Advanced DDoS Protection** \> **Provisioning**.

3. Choose **Website config** tab, and click **Add domain name**.

4. Configure the parameters.

   
   |**Configuration** |**Description** |
   |---|---|
   |**Provisioning** ||
   |**Associated instance** |Select the associated instance to protect your website services.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">Up to 10 instances can be selected at a time.</div><br> |
   |**Domain name** |Enter the domain name of your website. Both wildcard domain names and exact\-match domain names are supported.<br><br><br>* To include both a wildcard domain name and its primary domain name, you must enter them individually. For instance, if you want to secure the domain names `*.a.com` and `a.com`, it is necessary to enter each domain name separately during the provisioning.<br><br>* If a wildcard domain name and its corresponding exact\-match domain name are concurrently configured, the Advanced DDoS Protection instance will prioritize the matching of forwarding rules and protection policies for the exact\-match domain. To illustrate, if both `*.a.com` and `www.a.com` are provisioned, the forwarding rules and protection policies for `www.a.com` will take precedence. |
   |**Protocol type** |Select the communication protocol used by your websites, and enter available ports ranging from 1 to 65534. Currently, both HTTP and HTTPS protocols are supported.<br><br><br>* **HTTP**: When HTTP is selected, port 80 will be used by default, but this can be modified. The WebSocket protocol will also be automatically enabled.<br><br>* **HTTPS**: When HTTPS is selected, port 443 will be used by default, but this can be modified. The WebSocket protocol will also be automatically enabled.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To ensure proper forwarding, you must add an SSL certificate if you select <strong>HTTPS</strong> as the protocol type. For more details, see <a href="https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-setting-an-SSL-certificate-for-domain-name">Setting an SSL certificate for domain name</a>.   </div><br>   <br><br>   * **HTTPS redirection**: When HTTPS is enabled and HTTP is disabled, the system automatically activates HTTPS redirection. This function redirects all HTTP requests to HTTPS requests on the standard port 443. If this feature is turned off, the system will discard all HTTP requests.<br><br>   * **Advanced settings**: If HTTPS is selected, you can click **Expand advanced settings** to configure **Protocol following** and **HTTP 2.0**.<br><br>      * **Protocol following**: When you select both HTTP and HTTPS, you can enable **Protocol following**. This ensures that back\-to\-origin requests are forwarded using the same protocol as the access protocol. To ensure smooth transmission, verify that the origin server supports both HTTP and HTTPS protocols.<br><br>      * **HTTP 2.0**: HTTP 2.0 is enabled by default and cannot be deactivated when HTTPS is selected. Once enabled, it provides access protection under the HTTP 2.0 protocol and requests will be forwarded to the origin server using either the HTTP 1.0 or HTTP 1.1 protocol.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">It is required to upload a certificate if <strong>HTTPS</strong> is enabled when setting the protocol type.</div><br> |
   |**Back\-to\-origin configuration** ||
   |**Load balancing algorithm** |The Source Address Hash (SH) is selected by default and cannot be modified. This algorithm operates based on the consistent hashing of the source IP address. Consequently, requests originating from the same source IP address are consistently directed to the same backend server. |
   |**Origin server type** |Set the type of your origin server.<br><br><br>* Source IP: Use IP addresses to identify different origin servers.<br><br>* Source domain name: Use domain names to identify different origin servers. |
   |**Origin server configuration** |Click **Add origin server address**, and configure the related parameters.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">Up to 20 origin servers can be added.</div><br><br><br><br>* **Back\-to\-origin protocol**: The protocol from the Advanced DDoS Protection instance to the origin server. HTTP and HTTPS are supported. If you have enabled **Protocol following** for the current domain name, it is required to select both HTTP protocol and HTTPS as back\-to\-origin protocol to make the protocol following feature operate normally.<br><br>* **Origin server address**: Specify the IP address or domain name of the origin server. This must align with the type of origin server you have selected. In other words, if the **Origin server type** is set to **Source IP**, enter the IP address of your origin server. Conversely, if the **Origin server type** is set to **Source domain name**, enter the domain name of your origin server.<br><br>* **Origin server port**: The port of your origin server.<br><br>* **Weight**: It represents the likelihood that the origin server will receive a request. This likelihood is calculated by dividing the weight of the origin server by the total weight of all servers in the group. The value can be configured within a range of 1 to 99. The default setting is 99.<br><br>* **Action**: To remove an unnecessary item, click the **Delete** icon. |
   

5. Click **Next step**, and view and copy the value of CIDR blocks.

6. Click **Next step**, and confirm your forwarding configuration.

7. Click **Save**.


<span id="2df697ad"></span>
## What to do next

After configuration, you need to proceed with the following steps to ensure your service functions normally.


1. Add the back\-to\-origin CIDR blocks to the allowlist of the firewall, access control list (ACL), or any other security software installed on your origin server.

2. If HTTPS is selected as the protocol type, it is required to upload an SSL certificate and add it to your domain name.

3. Configure a DNS record for your domain name.
