---
title: "WAF protection"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/WAF-protection"
---

Application Load Balancer (ALB) can integrate with BytePlus Web Application Firewall (WAF). You can connect an ALB instance to WAF in the WAF console. After the ALB instance is connected to WAF, the system monitors and analyzes the traffic passing through the ALB instance to cleanse malicious traffic, separating business forwarding from security protection.

<span id="Connecting to WAF"></span>
## Connecting to WAF

<span id="Before you begin"></span>
### Before you begin


* Activate [BytePlus WAF](https://console.volcengine.com/waf) and buy a WAF instance.

* Ensure that the domain name you want to protect is filed but not added to WAF.

* Ensure that your business relies on BytePlus to offer website services, an ALB instance is created to balance traffic loads, and website services are running normally.

* For more information on BytePlus WAF, refer to [official documentation](https://www.volcengine.com/docs/6511/75945).


<span id="Procedure"></span>
### Procedure

Log on to the [BytePlus WAF console](https://console.volcengine.com/waf).

In the left\-side navigation pane, click **网站设置** to go to the corresponding page.

On the **网站设置** page, click **负载均衡接入**.

On the **负载均衡接入** tab, add the domain name you want to protect and complete proxy configurations. For more information, refer to [Configuration](https://docs.byteplus.com/en/docs/42/5230#Configuration) instructions. Confirm the settings and click **下一步**.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cef38273a56b99a690258dc1f8763ce3.png) </span>

Select the ALB instance, forwarding protocol, and port number that you want to connect to WAF. If you want to forward traffic from multiple ports, select the corresponding ports. Confirm the settings and click **确定**. The ALB instance is connected to WAF.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93b17bdb6e7f5fa5107b77d059a65897.png) </span>

<span id="Configuration instructions"></span>
### Configuration instructions


|Parameter |Description |
|---|---|
|防护域名 |Type the website domain name that you want to connect. The domain name must be the same as that for the listener. |
|代理配置 |Verify whether Layer 7 proxies such as Advanced DDoS Protection and content delivery network (CDN) are used for the website before connecting to WAF. |
| | |
| |* **否**: No proxy is configured before the website is connected to WAF. The IP address connected to WAF, namely X\-Real\-Ip, serves as the client IP address. |
| | |
| | |
| |* **是**: Proxies are configured before the website is connected to WAF. Therefore, the business requests received by WAF are forwarded by other Layer 7 proxy services, not directly from the clients initiating the requests. Configure a method to determine the client IP address. Details are as follows: |
| |* **X\-Forwarded\-For 字段获取客户端真实 IP**: uses the first elastic IP address (EIP) in the X\-Forwarded\-For field as the real IP address of a client. |
| | |
| |* **自定义 Header 字段获取客户端真实 IP**: gets the IP address of a client based on the sequence of adding matching fields and uses it as the real IP address of the client. |


If you select the **X\-Forwarded\-For 字段获取客户端真实 IP** option, a risk that attackers forge the X\-Forwarded\-For field is imposed.

If you select the **自定义 Header 字段获取客户端真实 IP** option, you can configure five custom Header fields at most for each domain name of a single instance.

If the IP address of a client cannot be got by matching fields, get the real IP address of the client from the X\-Forwarded\-For field.

If the real IP address of a client cannot be got from the X\-Forwarded\-For field due to IP address forgery, the X\-Real\-Ip field is used as the IP address of the client.

<span id="Website list"></span>
## Website list

The **网站列表** page of **网站设置** displays the basic information of websites that are connected to WAF, including the origin server IP address, access mode, protocol type, access status, protection status, and attack information. These fields are described as follows:


|Field |Description |
|---|---|
|防护网站 |The website that is connected to WAF. Click the name of a website to view its basic information, including the protected domain name, listener protocol type, WAF back\-to\-origin IP address, load balancing algorithm, back\-to\-origin protocol, virtual private cloud (VPC), origin server configuration, access mode, and CNAME value. |
|源服务器 IP |The IP address of the origin server that offers external services for a website connected to WAF. |
|接入方式 |The mode in which a website is connected to a WAF cluster. Options are: |
| | |
| |* **CNAME 接入**: includes SaaS and Advanced DDoS Protection. For more information, refer to [Web Application Firewall—Website settings](https://www.volcengine.com/docs/6511/75945). |
| | |
| | |
| |* **负载均衡接入**: An ALB instance is connected to WAF. |
|协议类型 |The protocol type for the website connected to WAF. Options are: |
| | |
| |* HTTP |
| | |
| | |
| |* HTTPS |
|接入状态 |The status of connecting the website to the WAF cluster. |
|防护状态 |The enabled status of different protection policies. Click a specific protection policy to go to its configuration page. Available protection policies include vulnerability protection, CC protection, access denylist, access allowlist, geographical access control, custom response blocking, prevention of sensitive information leakage, API protection, request allowlisting, field allowlisting, entrusted bot attack classification, custom bot attack classification. |
|3天攻击监控 |The situation of attacks to a website in the last 3 days. |
|操作 |You can edit, modify protection rules for, and delete a website connected to WAF. |
| | |
| |* **编辑**: You can edit the settings of a website connected to WAF. |
| | |
| | |
| |* **防护设置**: You can modify protection rules for different protection policies of the website. |
| | |
| | |
| |* **删除**: You can delete the domain name of the website connected in **负载均衡型接入** mode. |
