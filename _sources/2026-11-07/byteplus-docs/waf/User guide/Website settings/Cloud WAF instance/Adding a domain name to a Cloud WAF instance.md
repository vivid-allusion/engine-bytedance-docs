---
title: "Adding a domain name to a Cloud WAF instance"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Allowing_back-to-origin_CIDR_blocks"
---

The cloud WAF instance can be integrated with websites deployed either on BytePlus or elsewhere without limiting the deployment location of your business. Websites protected by the cloud WAF instance route their requests back to the origin servers through BytePlus servers located in the Johor region. After setting up the website parameters and back\-to\-origin parameters, you need to add the back\-to\-source CIDR blocks to the allowlist and update the DNS resolution records for the protected domain name. This article introduces the steps to making your domain name under WAF protection using the CNAME method.

<span id="3164365d"></span>
## Background information

BytePlus WAF supports two types of instances, suitable for different business scenarios.


* WAF instance for CDN domains: Protects domains added to BytePlus CDN. Integrating WAF with CDN not only enhances website security but also improves business performance. which offers your users a faster and more secure experience.

* Cloud WAF Instance: Regardless of where your business is located, whether on BytePlus or elsewhere, you can easily configure website parameters and back\-to\-origin parameters to finalize the setup. You can add your domains to a Cloud WAF instance using CNAME records. Simply configure the parameters, allow the WAF's back\-to\-source IP addresses, and modify the DNS resolution records of the domain to complete the setup.


<span id="a1901915"></span>
## Prerequisites


* You have already created a Cloud WAF instance. For more details about creating an instance, see [Creating a Cloud WAF instance to protect your domain names](https://docs.byteplus.com/docs/waf/Creating_a_Cloud_WAF_instance).

* The domain has not been added to the WAF instance yet.


<span id="11485d31"></span>
## Precautions

When you add domains using CNAME records, WebSocket protocols are automatically supported and currently, there is no option to disable this feature.

<span id="74e5cd53"></span>
## Procedure


1. Log in to the [BytePlus Web Application Firewall Console](https://console.byteplus.com/waf).

2. In the top menu bar, select **Asia Pacific (Johor)** , \*\*\*\* the region where your cloud WAF instance is located.

3. On the left\-side navigation pane, select **Website settings**, and then click **Create New Site**.

4. Choose the access method as **CNAME**.

5. Fill in the basic information of the website.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0adaefa63f848658c347731c5364721~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Description |Example |
   |---|---|---|
   |**Website configurations** |||
   |Protected domain |Enter the domain name you want to protect. You can enter the domain name directly, or use a `*` wildcard at the start to cover all subdomains without listing them individually.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you need to configure both wildcard domains and the main domain itself, please configure them separately. For example: if you need to configure <code>*.b.a.com</code> and <code>b.a.com</code>, you must connect to each domain separately and configure policies accordingly.</div><br> |www.test.com |
   |Project |Add the domain name to the project which the current account can access. |Default project |
   |Protocol type |Select a protocol:<br><br>An SSL certificate should be linked if the HTTPS protocol is selected. If only the HTTPS protocol is chosen, any HTTP requests will be redirected to HTTPS. |* HTTP: 80, 81<br><br>* HTTPS: 443, 4443<br><br>* Force non\-standard port redirection: Disabled<br><br>* Protocol follow: Disabled<br><br>* HTTP 2.0: Disabled<br><br>* IPv6 protection: Disabled |
   ||Port configuration:<br><br><br>* By default, the HTTP protocol uses port 80, while HTTPS uses port 443.<br><br>* The number of ports supported by the protocol configuration varies by instance edition.<br><br>* After entering a port number, hit Enter to proceed with adding more port numbers.<br><br>* Port numbers can be edited or deleted.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The port number entered must fall within the range of addable ports and must not be a duplicate. Click <strong>View available ports</strong> to explore and identify the available ports for the specific protocol.</div><br> ||
   ||More settings:<br><br><br>* Force non\-standard port redirection: If only the HTTPS protocol is enabled, HTTP port 80 will automatically be redirected to HTTPS port 443. You can enable **Force non\-standard port redirection** to redirect requests from non\-standard HTTP ports to the same port number on HTTPS.<br><br>* When enabled, the "back\-to\-origin protocol" of requests will match the "access protocol." To ensure that requests are properly forwarded to the origin server, please enable both HTTP and HTTPS, and verify that the origin servers support the specified protocols.<br><br>* HTTP 2.0: Before activating HTTP 2.0, ensure that the HTTPS protocol is selected. Once activated, HTTP 2.0 provides protected access and forwards to the origin servers using the HTTP 1.0/1.1 protocol.<br><br>* IPv6 protection: Once activated, this feature safeguards IPv6 client requests. Additionally, both IPv4 and IPv6 origin addresses can be configured in the origin settings. Once Protocol following is enabled, IPv4 requests will be directed to IPv4 origin servers, and IPv6 requests to IPv6 origin servers. ||
   |Certificate selection |After setting the HTTPS protocol, you should select the appropriate certificate. You have the option to choose either a previously uploaded certificate or to add a new one. |Because the HTTPS protocol is enabled, it is necessary to select the relevant certificate. |
   |**Log configuration** |||
   |Log collection |Enable or disable the log service for the current domain.<br><br><br>* **Enabled**: WAF starts collecting log data generated by the domain.<br><br>* **Disabled**: WAF does not collect log data generated by the domain.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To enable the log service, you must first authorize cross\-service access for the WAF, granting WAF permissions for log collection and storage.</div><br> |Keep it enabled |
   |Log all headers |* If disabled, only common header fields will be logged.<br><br>* If enabled, all header fields in the traffic will be logged, which may significantly increase the usage of log storage. |Keep it disabled |
   |**Access capability** |||
   |Proxy configuration |Check whether the website that needs to be configured was using Advanced DDoS Protection, CDN, or other layer 7 proxies before integrating with WAF.<br><br><br>* **No**: There was no proxy configured, WAF takes the IP making requests to WAF (X\-Real\-Ip) as the client IP.<br><br>* **Yes**: A proxy has been configured in front of the WAF. This means that the requests the WAF receives are forwarded through other Layer 7 proxy services, not coming directly from the requesting client. Further configuration is needed to determine the client IP method.<br><br>   * Getting client IP from the X\-Forwarded\-For field: Identify the first public IP address listed in the X\-Forwarded\-For (XFF) field, as the actual IP address of the client.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">This method poses a risk of attackers manipulating the X\-Forwarded\-For field.      </div><br>      <br><br>   * Custom header: Identify and utilize the client IP by matching fields in sequence to represent the actual client IP. If the field matching fails to retrieve the client IP, it will be obtained through the X\-Forwarded\-For field. However, if the X\-Forwarded\-For field is compromised by fake and illegal IP addresses, then the X\-Real\-Ip field will be used to determine the client IP.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can configure up to five custom header fields per domain in a single instance.      </div><br>       |No |
   |Keep\-alive connection |Configure the persistent connection limits between the client and WAF.<br><br><br>* Keep\-alive time: The persistent time for the connection between the client and WAF. 75 seconds is set by default, with available values ranging from 0 to 900 seconds.<br><br>* Reuse count: The number of multiple requests that can be sent over a single established TCP connection. The default value is set at 100, with options ranging from 60 to 1,000. |Maintain the default setting:<br><br><br>* Keep\-alive time: 75 seconds<br><br>* Reuse count: 100 |
   |Max request body size |The maximum value for request body sizes that can be received. The default value is set at 60 MB, with options ranging from 1 to 10,240 MB. |Maintain the default setting: 60 MB |
   |**Origin server configuration** |||
   |Back to origin method |* Back to origin over public networks: The origin servers apply public IP addresses.<br><br>* Private IP addresses within a VPC: The origin address is a private IP, and you should select a BytePlus VPC. |Back to origin over public networks |
   |Load balancing |* Weighted Round Robin (WRR): Backend servers assigned higher weight values are queried more frequently.<br><br>* Weighted Least Connection (WLC): Allocates requests to the backend server that has the lowest ratio of "current connections to weight."<br><br>* Source IP Hashing (SH): This method employs consistent hashing based on the source IP address, ensuring that requests from the same source are consistently routed to the same backend server. |Weighted Round Robin |
   |Origin server configuration |* Group:<br><br>   * Default group: This group consists of all access ports that have not been assigned custom back\-to\-origin configuration rules. If the custom grouping rules do not apply, the default grouping rules will automatically take effect.<br><br>   * Custom group:<br><br>      * Click **add** to create a custom group, and configure the effective port range.<br><br>      * You can edit the custom group name, which supports a maximum of 15 characters including letters, digits, and underscores.<br><br>      * You can edit the custom group. However, removing a group will delete the back\-to\-origin configuration within it and apply the default group configuration to perform back\-to\-origin on the ports inside the group.<br><br>* Access port configuration:<br><br>   * The default group consists of all access ports that have not been assigned custom back\-to\-origin configuration rules.<br><br>   * The custom groups allow the selection of multiple target interfaces within the specified port range. A port can be selected only once across different custom groups.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For example, if you have selected ports <code>80</code>, <code>81</code>, <code>82</code>, <code>83</code> under HTTP protocol and ports <code>443</code>, <code>4443</code> under HTTPS protocol in your website configuration, and have chosen ports <code>80</code> and <code>81</code> under the HTTP protocol in custom group 1 of the origin server configuration, the remaining ports <code>82</code>, <code>83</code>, <code>443</code>, and <code>4443</code> will be applied to the back\-to\-origin rules configuration in the default group.   </div><br>   <br><br>* Origin server address configuration:<br><br>   * Origin server protocol: The protocol applied for rerouting requests from WAF to the origin server, both HTTP and HTTPS are supported.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">When the protocol following function is disabled, the origin server will maintain consistent protocols across different groups within the same region. For example, if you configure the protocol of a custom group's origin server to HTTP, then the protocol for the origin sites in all groups, including the default group, will also be set to HTTP.      </div><br>      <br><br>   * Origin server address: The origin server IP address of the website.<br><br>   * Origin server port: The exact port of the origin server.<br><br>   * Weight: It refers to the probability that a backend server receives a request. Integers from 1 to 100 are supported.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Weights do not necessarily indicate proportionality.      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">To ensure equal rotation probability among multiple origin servers, assign them the same weight value.      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The total weight of the origin servers can exceed 100.      </div><br>      <br><br>      * In a weighted round\-robin load balancing algorithm, each origin server's chance of being selected is determined by its weight divided by the total weight of all servers in the group. Therefore, the larger the weight, the greater the probability of receiving requests.<br><br>      * When the load balancing algorithm uses weighted least connections, the calculation is based on the ratio of current connections to the weight of each origin server. The origin server with the lowest ratio is most likely to receive new requests.<br><br>      * When the listener scheduling algorithm uses source IP hashing, configuring weights is unnecessary.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add up to 20 origin servers to each IP address group.   </div><br>    |<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Because HTTP and HTTPS protocols are selected and Protocol following is enabled when setting website, you should configure the origin server information to support both HTTP and HTTPS protocols.</div><br><br><br>For example:<br><br>In the default group, add the following two origin servers:<br><br><br>* Origin server 1:<br><br>   * Origin server protocol: HTTP<br><br>   * Origin server address: 192.1. **.** <br><br>   * Origin server port: 80<br><br>   * Weight: 100<br><br>* Origin server 2:<br><br>   * Origin server protocol: HTTPS<br><br>   * Origin server address: 192.2. **.** <br><br>   * Origin server port: 443<br><br>   * Weight: 40<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Because the load balancing algorithm is <code>WRR</code>, origin server 1, which has a weight of 100, has a higher probability of receiving requests.</div><br> |
   |**Back\-to\-origin capability** |||
   |Connection timeout |The timeout for establishing a connection between the WAF and the backend server. It should be set longer than the health check timeout. The default value is set at 4 seconds, with options ranging from 4 to 120 seconds. |Maintain the default setting: 4 seconds |
   |Write connection timeout |The timeout for WAF to transfer requests to the backend server. The default value is set at 60 seconds, with options ranging from 30 to 36,000 seconds. |Maintain the default setting: 60 seconds |
   |Read connection timeout |Timeout for WAF to read response from the backend server. The default value is set at 60 seconds, with options ranging from 30 to 36,000 seconds. |Maintain the default setting: 60 seconds |
   |Back\-to\-origin keep\-alive connection |The number of reuse counts from WAF to the origin server. The default value is set at 100, with options ranging from 60 to 1,000. |Maintain the default setting: 100 |
   |Origin retry |The maximum number of retries permitted when the WAF can not connect to the origin server. The default value is set at 3 times, with options ranging from 1 to 10. |Maintain the default setting: 3 times |
   |Idle connection timeout |Idle time for the persistent connection established between WAF and the backend server. The default value is set at 15 seconds, with options ranging from 1 to 60 seconds. |Maintain the default setting: 15 seconds |
   |SNI configuration |* If your origin server IP is associated with multiple domain names and WAF connects to your origin server using the HTTPS protocol, you need to set up the sourcing SNI (Server Name Indication) to identify the specific domain name being requested. The origin server delivers the SSL certificate for the configured SNI domain name to ensure proper functionality.<br><br>* If no domain name is configured, requests will be routed based on the actual host specified in the traffic. |Disabled |
   

6. Click **Submit**.

   Once the domain name is successfully added, WAF will display the CNAME value of the protection domain and the back\-to\-origin CIDR blocks on the page.


<span id="5aa13778"></span>
## What to do next


1. Allow access from the back\-to\-origin CIDR blocks. For more details, see [Adding the back-to-origin CIDR blocks to your allowlist](https://docs.byteplus.com/docs/waf/Modifying_the_DNS_record).

2. Check whether the forwarding takes effect. For more details, see [Verifying the configurations of your domain name](https://docs.byteplus.com/docs/waf/Verifying_website_settings).

3. Modify DNS resolution record, see [Modifying the DNS record of your domain name](https://docs.byteplus.com/docs/waf/Adding_a_domain_to_a_cloud_WAF_instance).
