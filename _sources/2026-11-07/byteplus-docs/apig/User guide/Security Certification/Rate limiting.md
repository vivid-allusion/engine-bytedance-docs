---
title: "Rate limiting"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_a_rate_limit_plugin"
---

The rate limiting plugin supports controlling access request thresholds at both the APIG instance level and the route level to ensure the stability of backend services. This article introduces how to configure the rate limiting feature.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information


* Route\-level rate limiting: Within a statistical period, the total number of requests across all request methods, matching paths, and domain names within a specified route is calculated.

* Instance\-level rate limiting: During a statistical period, the total number of requests across all routes within the specified instance is calculated.


The gateway counts instance\-level rate limiting policies and route\-level rate limiting policies separately. The enforcement priority of route\-level rate limiting policies is higher than that of gateway\-level policies. For example, suppose there are four routes—a, b, c, and d—under APIG instance A. In example A, routes a, b, and c are all configured with a rate limiting policy, while route d is not. Then, within a statistical period:


* If a request hits the a, b, or c routes under instance A, each of the a, b, and c routes will be counted separately, and instance A will not be counted.

* If a request hits route d under instance A where no rate limiting policy is configured, only instance A is counted.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An APIG instance has been created. For details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* Routes have been created. For details, refer to [add route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* After the rate limiting plugin is enabled, it takes effect independently on each gateway replica, and the rate limiting counters are isolated between different replicas.

   For example, if your APIG instance has 2 replicas and you configure an instance\-level rate limit of 100 requests per minute, each replica will be limited to 100 requests per minute, so the theoretical maximum throughput of the APIG instance is 200 requests per minute.

* Rate limiting policy priority: route level takes precedence over instance level.

* Routing\-level rate limiting only supports HTTP(S) routes and does not support TCP routes.

* Only one rate limiting plugin is permitted per APIG instance.

* Only one rate limiting plugin can be configured per route.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Instance\-level rate limiting plugins and route\-level rate limiting plugins both support dual entry configuration, as follows:</div>



* <div data-tips="true" data-tips-type="tip">The instance\-level rate limiting plugin can be enabled and configured in two ways: You can go to <strong>Instance Management</strong>, select the target instance, and open the <strong>plugin List</strong> tab to enable and configure the rate limiting plugin. Alternatively, you can configure it by accessing <strong>plugin Management \> Rate Limiting plugin</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The route\-level rate limiting plugin can be enabled and configured by navigating to <strong>Route management \> Service list (Domain name)</strong> and accessing the <strong>plugin list</strong> tab for the target route. Alternatively, you can configure it via <strong>plugin management \> Rate limiting plugin</strong>.</div>



Below, the **plugin Management \> Rate Limiting plugin** entry is used as an example to introduce the relevant process.


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the left navigation bar, select **Plugin management \> Rate limiting**.

3. On the rate limiting plugin page, click **Create plugin**, and configure the parameters for the rate limiting plugin.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Effective level |Select the effective level for the rate\-limiting plugin, including:<br><br><br>* **Instance level**: The rate limiting threshold is effective within an instance, and you need to specify the target instance to which it applies.<br><br>* **Routing level**: The rate limiting threshold takes effect within the Service, and you must specify the target instance, target Service, and target route. |
   |Notes/comments |Enter notes/comments about the current rate\-limiting plugin. This field can be left empty. |
   |Threshold of limited viewership |Configure the number of times the current instance/route can be accessed within one interval period. After exceeding the target number of requests, access requests will be denied, and the system will return error code `429 Too Many Requests` and display `rate_limited`. |
   |Interval period |Define the duration of the interval period, including: 1s (1 second), 1m (1 minute), 1h (1 hour), and 1d (1 day). |
   

4. Click **OK** to complete the configuration.


<span id=".5pON5L2c57uT5p6c"></span>
## Result validation

<span id="GkGK2OFX"></span>
### View configuration

After the configuration is completed, a new rate limiting plugin record will be generated in the **Rate limiting** list. The plugin status is **enabled**, indicating that the plugin feature is active.

<span id="I0CnWMU9"></span>
### Certification tests


1. Use the domain name configured in the APIG instance to access the service, as long as access requests do not exceed the rate limiting threshold.


```Bash
curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx
```


The expected result is as follows, which means that the backend Service can be accessed through the API gateway.

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



2. If you access the service using the domain name configured in the APIG instance and the number of access requests exceeds the rate limit threshold, access will be restricted.


```Bash
curl -H "Host: apig-example.com" http://14.xxx.xxx.xxx
```


The expected result is as follows: requests within the target quota can be accessed successfully, while requests that exceed the target quota are rejected, and a `rate_limited` message is displayed.

```Bash
rate_limited
```
