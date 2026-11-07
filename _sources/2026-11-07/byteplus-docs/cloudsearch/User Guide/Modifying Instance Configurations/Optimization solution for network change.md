---
title: "Optimization solution for network change "
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Network-change-optimization"
---

<span id="ae82b378"></span>
## Background Information

Replanning the network for Cloud Search instance requires modifying the private network or subnet configurations, which will result in changes of network connection accessing the instance from visualization tools (Kibana, Cerebro, etc.), SDK, or HTTP/HTTPS using public or private network domain name.

Public and private domain names need to be resolved to the new IP address in accordance with the modified network setting. Since browsers, applications, operating systems, and DNS servers may cache the results of DNS resolution, the new IP address cannot be detected in time. Therefore, network change of Cloud Search instance will lead to minutes or even hours of disruption to instance access from visualization tools (Kibana, Cerebro, etc.) as well as the online read/write of applications.

This topic describes optimization solutions for different cloud service scenarios and clients to reduce service interruption time due to network change.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The optimization solutions proposed in this topic only reduce service interruption time but <strong>cannot guarantee zero impact on the service</strong>.</div>


<span id="40a21937"></span>
## Optimization settings for the cloud

<span id="1b8e56bd"></span>
### Public cloud scenario

For public cloud scenario (i.e. all your service resources are inside BytePlus), a private domain name is recommended to access the Cloud Search instance which ensures efficient domain name resolution provided by DNS server inside BytePlus, namely the BytePlus PrivateZone service. Meanwhile, the internal DNS server can control its cache time to make the clients detect the new IP address faster, and thus reduce service interruption time.

<span id="73669d99"></span>
### Hybrid cloud scenario

For hybrid cloud scenario (i.e. BytePlus resources are connected to your own IDC or third\-party cloud services via a private line, VPN, cloud enterprise network, or transit router), a private domain name is recommended to access the Cloud Search instance. In addition, DNS resolution requests of private domain name are recommended to forwarded to DNS server inside BytePlus VPC which can also be enabled by BytePlus PrivateZone service. BytePlus PrivateZone service ensures efficient domain name resolution and reduces service interruption time.

<span id="6391f90c"></span>
### Private cloud scenario

If your applications and services are deployed in your own IDC or third\-party cloud service, or local debugging is required, the public domain name is used to access BytePlus services. For this scenario, BytePlus PublicDNS service is recommended to speed up your Internet access and help you avoid issues including DNS spoofing, DNS hijacking, and so on. It can also effectively control the cache expiration time of the DNS server to make your clients detect the new IP address for the domain name faster, and thus reduce service interruption time.

<span id="1b02d89b"></span>
## Optimization settings for the client

The configurations of visualization tools (Kibana, Cerebro, etc.) and online applications can also be optimized to reduce service interruption time.

<span id="2b9b8fe2"></span>
### Visualization tools

Browsers may cache DNS, and the cache policies may vary from different browsers.

When access failure or time\-out occurs in using visualization tools, try to refresh the page multiple times. If it doesn't work, please try the following workaround.

Here we take Chrome browser as an example to illustrate how to clear browser's DNS cache.


1. Type `chrome://net-internals/#dns` into the address bar of Chrome browser.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5a7b6dc06d245deb16cadb659d6fed5~tplv-goo7wpa0wc-image.image) </span>


2. On the DNS lookup page, click **Clear host cache**.

3. Switch to the Socket page, and click **Flush socket pools**.


<span id="fa5c2ed2"></span>
### Application clients

Your application will be developed in multiple languages, and some languages will cache DNS internally.

Taking Java as an example, the JVM will cache DNS by default in the following two cases:


* In most cases, the `JavaSecurity` mechanism is disabled, and the JVM defaults to DNS caching for 30 seconds.


You can use the system parameter `sun.net .inetaddr.ttl` to customize the cache time in seconds. There are two ways to specify the cache time as listed below:


* Add `-Dsun.net.inetaddr.ttl=10` to the application startup parameters.

* Set properties in your application code as follows: `System.setProperty("sun.net.inetaddr.ttl", "10")`

* If the `JavaSecurity` mechanism is enabled, the JVM will permanently cache DNS records by default, which will cause the program to be unable to detect the new IP address corresponding to the modified domain name.


In this case, the Security property needs to be configured in your application code to specify the cache time in seconds by setting the value of `networkaddress.cache.ttl`.

```Java
java.security.Security.setProperty("networkaddress.cache.ttl", "10");
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For Java clients, both of the above settings require an application restart to take effect. The recommended DNS cache time of the JVM is 5 to 10 seconds, which will not have a significant impact on the access efficiency of the application.</div>


* <div data-tips="true" data-tips-type="tip">For clients of other languages like Go and Python, DNS is not cached by default. If a specific function library is used to implement DNS caching, the caching time in the corresponding code needs to adjusted.</div>
