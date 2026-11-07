---
title: "IP Restriction"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_blocklist_and_allowlist_plugin"
---

IP Restriction are among the security protection capabilities provided by the API gateway. You can deny or allow access requests from specific IP addresses by configuring blocklists and allowlists. The API gateway supports configuring IP blocklists and allowlists at the instance, service, and route levels to meet the requirements for fine\-grained access control. This article describes how to set blocklist and allowlist for the API gateway.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* APIG instance has been created. For more information, refer to [Create an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* The service has been created. For specific operations, refer to [Create a service](https://docs.byteplus.com/en/docs/apig/Creating_a_service#.5Yib5bu65pyN5Yqh).

* The route has been added. For details, refer to [add route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limi


* Each resource dimension supports only one blacklist\-and\-allowlist Plugin.

* Both a blocklist and an allowlist can be defined simultaneously within the same Plugin.

* When both the blocklist and allowlist are active, the blocklist has higher priority.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the left navigation bar, select **Plugin Management \> IP ** **Restriction**.

3. On the IP Restriction page, click **Create Plugin** and configure the Plugin parameters.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Effective level |Select the effective level for the IP allowlist and blocklist Plugin, including:<br><br><br>* **Instance level**: The blacklist and allowlist take effect at the instance level, and you need to specify the target instance where they will be applied.<br><br>* **Service level**: The allowlist and denylist take effect within a Service, and you must specify the target instance and target Service to which they apply.<br><br>* **Routing level**: The allowlist and denylist take effect within the route. You need to specify the target instance, target service, and target route to which they apply. |
   |Notes/comments |Enter notes/comments about the current IP allowlist and blocklist Plugin. This field can be left blank. |
   |IP black/white list |Check the blacklist or whitelist you need to configure.<br><br><br>* **blacklist**: Prohibit access from specific IP addresses. Enforce source IP blocking for unfriendly access attempts in the gateway scenario.<br><br>* **whitelist**: Allows access from specific IP addresses. In the gateway scenario, only access from trusted source IPs is allowed. |
   |IP list |Enter a valid IPv4 CIDR IP address, then press Enter to confirm. Multiple entries are supported; separate them with a semicolon.`;`Or separate by pressing Enter. |
   |Custom Get IP |Enable custom method for obtaining the IP address?<br><br><br>* **IP acquisition method**: Currently, only **the X\-Forward\-For\-based method** is supported.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">There is a risk that the X\-Forward\-For header may be tampered with during the forwarding process, and the API gateway cannot verify the trustworthiness of the X\-Forward\-For header.</div><br><br><br><br>* **Intercept location**: The IP location selected for Identity and Access Management on multi\-layer forwarding chains, with IP information sourced from X\-Forward\-For. |
   

4. Click **OK** to complete the configuration.


<span id="PhDDGZOH"></span>
## Result validation

<span id="pUUFvdNf"></span>
### View configuration

After the configuration is complete, a new Plugin record will be generated in the  ** IP blacklist and allowlist Plugin** list. The Plugin status is **enabled**, which means the Plugin feature is active.

<span id="uMUuP0bF"></span>
### Certification test


1. To access the Service using the domain name configured in the APIG instance, this example uses a blocklist. This applies when the IP address of the access request is not on the blocklist.


```Bash
curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx
```


The expected result is as follows, indicating that backend services can be accessed through the API gateway.

```HTML
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```



2. When accessing the Service using the domain name configured in the APIG instance, if the IP address of the access request is on the blocklist...


```Bash
curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx
```


The expected result is as follows: requests that match the IP blocklist will be denied, and the message `ip restriction deny` will be displayed.

```Bash
ip restriction deny
```
