---
title: "Adding domain name"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Adding_domain_name"
---

The service, serving as the external interface for business operations, can bind your custom domain name to the service through the add domain name feature. This article guides you on how to add a custom domain name.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A service has been created. For details please refer to [Creating a service](https://docs.byteplus.com/en/docs/apig/Creating_a_service).

* The domain name to be added has been obtained from the domain registrar.

* (Optional) If the domain name uses the HTTPS protocol, a trusted digital certificate needs to be obtained.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* A domain name can only be uniquely bound to one service, and domain name conflicts prevent successful configuration.

* While binding custom domain names, it is not possible to add, delete, or modify any custom domain names and routes under the current service.

* There is a limit to the number of custom domain names that each service can associate with, for more details, please refer to [Limits](https://docs.byteplus.com/en/docs/apig/Limits).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. Select **Route management \> Service list (Domain name)**  from the left navigation bar.

4. Click on the target service name in the service list to enter the Overview page of the service.

5. Select the **domain management** tab, **click** add domain name, and bind a custom domain in the Service.

   
   |**Parameter** |**Description** |
   |---|---|
   |Service name |Displays the name of the current service. |
   |Add domain name |Please enter the Domain name to be added.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Public Domain names must complete ICP filing or access filing with the Ministry of Industry and Information Technology, otherwise, the configuration cannot be successful.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">A domain name can only be uniquely bound to one service, and domain name conflicts prevent successful configuration.</div><br> |
   |Protocol type |Select the communication protocol type supported by the custom Domain name.<br><br><br>* **HTTP**: Supports requests of HTTP protocol only.<br><br>* **HTTPS**: Supports requests of HTTPS protocol only.<br><br>* **HTTP & HTTPS**: Supports requests of both HTTP and HTTPS protocols. |
   |Enforce HTTPS |Whether to enable forced HTTP request redirection, including:<br><br><br>* Enable: All HTTP requests for this Domain name will be redirected to HTTPS.<br><br>* Do not enable: HTTP requests for this Domain name will not be redirected to HTTPS. |
   |Certificate selection |When **protocol type** includes HTTPS, select the HTTPS certificate saved by the Certificate Center from the dropdown menu.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The domain name in the certificate needs to match the domain name to be bound.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Wild card certificates only support same\-level matching. e.g., <code>*.example.com</code> can match <code>a.example.com</code>, but can not match <code>a.b.example.com</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you need to reuse the same multi/wildcard certificate, ensure that the certificate ID selected under the same gateway is consistent (uploading the same certificate content repeatedly to the Certificate Center will result in different certificate IDs). Otherwise, accessing these domain names under the same browser may result in access failure.</div><br> |
   

6. Click **confirm** to complete the binding of the Domain name.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After configuration, you need to go to DNS provider to complete the DNS resolution and point the custom domain to the API gateway's default domain name or IP address.


* Add a DNS resolution record. Point the custom domain to the IP address of the API gateway. To obtain the IP address of the API gateway, please refer to [Obtaining gateway address](https://docs.byteplus.com/en/docs/apig/Adding_access_entrance).

* Add a CNAME record. Point the custom domain to the default domain name of the current service of API gateway. If a CNAME record is not added, client requests sent through the custom domain will not be correctly resolved to the API gateway.
