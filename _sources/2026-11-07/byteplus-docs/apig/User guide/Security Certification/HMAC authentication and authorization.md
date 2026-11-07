---
title: "HMAC authentication and authorization"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_an_HMAC_plugin"
---

The HMAC plugin generates a non\-forgeable AK/SK signature for HTTP requests based on the HmacSHA256 algorithm. After it is enabled, you must include the required request headers, signature, and other related information to access the current resource. This article explains how to create an HMAC plugin.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* If you select service level as the effective level, please create a service first. For specific operations, refer to [Create Service](https://docs.byteplus.com/en/docs/apig/Creating_a_service).

* If the effective level is set to the route level, please add a route first. For specific operations, refer to [add route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

* The consumer has been created, and the credential has been generated. For specific operations, refer to [Create a consumer](https://docs.byteplus.com/en/docs/apig/Creating_a_consumer) and [Generate a credential](https://docs.byteplus.com/en/docs/apig/Generating_credentials).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limi


* The same plugin can only be bound once on the same resource.

* When the same plugin is bound to resources at different levels, only the resource with the highest effective priority is matched. The effective priority is ranked from highest to lowest as follows: route \> service.

   For example, Service I has two routes: Route A and Route B. When the plugin is configured on both Service I and Route A, Route A uses its own plugin configuration, while Route B uses the plugin configuration set at the Service I level.

* You can only select APIG instances created after 00:00 on January 19, 2024 as the instance for an instance\-level plugin. If your console cannot enable plugins, please [submit a ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000170&FlowKey=DhvSFwiOSXyEVSlGZJXx).


<span id=".5Yib5bu65o-S5Lu2"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, select **Plugin Management \> HMAC Auth**.

4. On the HMAC page, click **Create Plugin**.

5. On the Create HMAC plugin page, configure the following settings, then click **OK**.

   
   |**Parameter** |Description |
   |---|---|
   |Effective level |Select the activation level for the HMAC plugin. Including: service level, routing level.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the same plugin is bound to resources at different levels, only the resource with the highest effective priority will take effect. The effective priority, from highest to lowest: Route \> Service.</div><br> |
   |Service |For the effective level, select **Service level**, then select the instance and service. |
   |owning route |Select **Routing level** as the effectiveness level, and then select the instance, service, and route. |
   |Notes/comments |Optional. You can choose whether to edit the content of the notes/comments according to your business needs. For example, you may include the purpose of the HMAC plugin to facilitate future identification. |
   |Consumer |Select a consumer.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The consumer must have generated a credential.</div><br> |
   


<span id="15agjef9"></span>
## Result validation

<span id="15agjef9"></span>
### View configurations

After the configuration is complete, a new plugin record will be generated in the HMAC list. The plugin status is **Enabled**, indicating that the plugin feature is in effect.

<span id="vgzFmCvN"></span>
### Certification testing


1. Access the Service using the domain name configured in the APIG instance when the access request carries HMAC credential information. The signature method for an HMAC credential. Refer to [Signature method](https://docs.byteplus.com/en/docs/6369/67269).


```Bash
curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx -H "Authorization: HMAC-SHA256 Credential=API***, SignedHeaders=host;x-content-sha256;x-date, Signature=***"
```


The expected result is as follows, indicating that the backend service can be accessed through the API gateway.

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



2. Access the service using the domain name configured in the APIG instance when the access request does not carry HMAC credentials.


```Bash
curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx
```


The expected result is as follows: authentication fails, and the backend Service cannot be accessed through the API gateway.

```Bash
Consumer authentication failed.
```
