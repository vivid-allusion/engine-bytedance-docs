---
title: "Serverless OLAP WebUI best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Serverless_OLAP_WebUI_best_practices"
---

The WebUI of StarRocks/Doris provides a web\-based user interface for monitoring and managing clusters. This article introduces the best practices for connecting to fully managed StarRocks/Doris clusters via WebUI, covering connection methods, network recommendations, and proxy configuration suggestions.

<span id="84d51016"></span>
# Constructing the Web UI access URL

You can obtain the FE address and HTTP port (default is 8030) for the corresponding queue on the "Network Connection" page of the Serverless queue. By using the IP address and HTTP port of any FE node, you can construct the access URL for the corresponding Web UI.


1. Obtain the IP address and HTTP port of the FE node.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/786560ff88a148c9aabc49b3ce756e72~tplv-goo7wpa0wc-image.image) </span>

2. Construct the Web UI access URL in the format `http://<fe_ip>:<http_port>`.

3. After constructing the access URL, you can refer to the following instructions to access the WebUI based on your current network environment and requirements for service stability when accessing the web page.


<span id="6eecf1c4"></span>
# VPC intranet environment

If you can directly access the VPC intranet of BytePlus, you can directly open the Web UI access URL, or configure a proxy as needed to access the corresponding Web UI through a proxy connection.

<span id="6eecf1c4"></span>
## Direct access

You can directly open the Web UI access URL to access: `http://<fe_ip>:<http_port>`.

<span id="6eecf1c4"></span>
## Proxy access

To ensure high availability of the corresponding Web UI service, you can also set up a Nginx proxy, using the FE node IPs under the OLAP instance as the proxy targets. When configuring the proxy, ensure that the source IP routes to a fixed backend node. For guidance on setting up a custom proxy, refer to: [使用 Nginx 实现 web UI 负载均衡 - Apache Doris](https://doris.apache.org/zh-CN/docs/3.x/faq/install-faq?_highlight=web&_highlight=ui&_highlight=%E7%99%BB%E5%BD%95#q8-%E5%A4%9A%E4%B8%AA-fe%E5%9C%A8%E4%BD%BF%E7%94%A8-nginx-%E5%AE%9E%E7%8E%B0-web-ui-%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%E6%97%B6%E6%97%A0%E6%B3%95%E7%99%BB%E5%BD%95).

<span id="6eecf1c4"></span>
# Non\-VPC intranet environment

If you cannot directly access the VPC intranet of BytePlus, you need to use a Windows ECS instance in the same VPC environment as the Serverless OLAP instance to access the Web UI via proxy. The procedure is as follows.

<span id="327e4f27"></span>
## Proxy access


1. Create an ECS instance in the ECS console that meets the following conditions:

   1. The VPC and availability zone must be consistent with those of the OLAP instance to ensure network connectivity.

   2. The ECS instance must use the Windows operating system. You can select a public image, such as Windows Server 2022 Standard Edition 64\-bit Chinese.

2. Obtain the internal IP address and HTTP port of any FE node.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f291452c77c4cb4b21b47c7e3824132~tplv-goo7wpa0wc-image.image) </span>

3. Log in to the ECS instance through the ECS Console. Both ECS Terminal and VNC login methods are supported. After logging in, use the Microsoft Edge browser that comes with the operating system, and enter `http://<fe_ip>:8030` in the address bar to use the WebUI.


<span id="d38ebb69"></span>
# FAQs

<span id="de96d3fb"></span>
## Q1. How can I resolve frequent prompts to log in again during use?


* Possible cause: Confirm whether the FE IP being used is the IP provided directly on the Network Connection page of the OLAP Console. The IP provided here is a PLB address. To avoid uneven FE load caused by particularly high load from the same source IP, the load balancing algorithm does not use source address hashing. As a result, when the same source IP accesses the WebUI, switching FE may lead to authentication failures.

* Solution: On the OLAP Console \- Network Connection page \- View all nodes, select an FE IP. This avoids authentication issues caused by backend FE switching through the load balancing device.
