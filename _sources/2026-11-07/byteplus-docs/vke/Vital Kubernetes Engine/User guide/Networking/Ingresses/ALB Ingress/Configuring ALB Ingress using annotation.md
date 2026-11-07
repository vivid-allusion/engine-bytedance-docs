---
title: "Configuring ALB Ingress using annotation"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-an-ALB-Ingress-using-annotations"
---

An Application Load Balancer (ALB) Ingress allows you to configure powerful ALB capabilities through annotations. This topic introduces the typical scenarios of configuring an ALB Ingress through annotations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The annotations in YAML files are case\-sensitive.</div>



<span id=".6YCJ5oup5Y2V5Liq55uR5ZCs5Zmo"></span>
## Selecting a single listener

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before using an annotation to select a listener for an ALB instance, you must first create or associate the corresponding ALB instance and listener through an ALBInstance. For configuration details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl">Creating ALB Ingresses by using kubectl</a>.</div>


An ALB Ingress allows you to use an annotation to select a single listener created by an ALBInstance and configure forwarding rules and back\-end server groups in the listener. The following content in Yaml is an example with descriptions in it:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/loadbalancer-port: "80" # The listening port.
    ingress.vke.volcengine.com/loadbalancer-protocol: "http"  # The listener protocol. Values: http and https.
spec:
  ingressClassName: alb  # The name of the ALBInstance.
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


Here are the descriptions for the annotations included in the YAML file.


|Parameter |Type |Description |default value |
|---|---|---|---|
|ingress.vke.volcengine.com/loadbalancer\-port |String |Select the listening port for the listener. Ensure that the listener has been configured with the corresponding listening port. |80 |
|ingress.vke.volcengine.com/loadbalancer\-protocol |String |Select the protocol for the listener. Valid values:<br><br><br>* **http**: The HTTP protocol.<br><br>* **https**: The HTTPS protocol. |http |


<span id=".6YCJ5oup5aSa5Liq55uR5ZCs5Zmo"></span>
## Selecting multiple listeners

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before using an annotation to select a listener for an ALB instance, you must first create or associate the corresponding ALB instance and listener through an ALBInstance. For configuration details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl">Creating ALB Ingresses by using kubectl</a>.</div>


An ALB Ingress allows you to use annotations to select multiple listeners created by an ALBInstance and configure forwarding rules and back\-end server groups in the listeners. The following content in Yaml is an example with descriptions in it:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/listen-ports: '[{"HTTP": 80},{"HTTPS": 443}]' # Select multiple listeners. The configuration includes their listener protocol and port number.
spec:
  ingressClassName: alb  # The name of the ALBInstance.
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


Here are the descriptions for the annotations included in the YAML file.


|Parameter |Type |Description |default value |
|---|---|---|---|
|ingress.vke.volcengine.com/listen\-ports |Array of String |Select the protocol and port number for multiple listeners. Example: `{"HTTP": 80}`. You can specify a list of multiple values separated by commas (`,`).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you use the annotation to select multiple listeners, the <code>ingress.vke.volcengine.com/loadbalancer-port</code> and <code>ingress.vke.volcengine.com/loadbalancer-protocol</code> of individual listeners become invalid.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the annotation is deleted, the automatically created forwarding rules will also be deleted.</div><br> |No |


<span id=".6YWN572u6LCD5bqm566X5rOV"></span>
## Specifying scheduling algorithm

ALB Ingresses support annotations for configuring the scheduling algorithm of back\-end server groups. The following content provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/loadbalancer-scheduler: "wrr"  # The scheduling algorithm for back-end server groups. Valid values include wrr, wlc, and sh.
spec:
  ingressClassName: alb  # The name of the ALBInstance.
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


Here are the descriptions for the annotations included in the YAML file.


|Parameter |Type |Description |default value |
|---|---|---|---|
|ingress.vke.volcengine.com/loadbalancer\-scheduler |String |The scheduling algorithm used by the ALB back\-end server group. Valid values:<br><br><br>* **wrr**: Weighted Round Robin. Backend servers with higher weight values are polled ‌more frequently (with a higher probability)‌.<br><br>* **wlc**: Weighted Least Connections. ‌The algorithm extends the least connections algorithm‌ by assigning different weights to servers based on their ‌processing capacity‌, enabling each server to handle a number of service requests proportional to its weight.<br><br>* **sh**: Source IP Hash. ‌The algorithm uses consistent hashing‌ based on source IP addresses. Requests from the same source address ‌are directed to‌ the same backend server. |wrr |


<span id=".6YWN572u55u06YCaLXBvZC3mqKHlvI8="></span>
## Configuring LB\-to\-pod direct access mode

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The LB\-to\-pod direct access mode is only effective in clusters running with VPC\-CNI network model.</div>


An ALB Ingress supports LB\-to\-pod direct access configuration via annotations. The following content provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/loadbalancer-pass-through: "true" # Configure the LB-to-pod direct access mode.
spec:
  ingressClassName: alb  # The name of the ALBInstance.
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


Here are the descriptions for the annotations included in the YAML file.


|Parameter |Type |Description |default value |
|---|---|---|---|
|ingress.vke.volcengine.com/loadbalancer\-pass\-through |String |Select whether to enable the LB\-to\-pod direct access mode for the ALB instance. Valid values:<br><br><br>* **true**: Enable the LB\-to\-pod direct access mode.<br><br>* **false**: Disable the LB\-to\-pod direct access mode. |false |


<span id=".6YWN572u5YGl5bq35qOA5p-l"></span>
## Configuring health check

<span id=".6YWN572uLWh0dHAt5Y2P6K6u55qE5YGl5bq35qOA5p-l"></span>
### Configuring HTTP health checks

An ALB Ingress supports HTTP health checks for backend server groups based on annotations. The following is an example YAML with comments for annotations.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    ingress.vke.volcengine.com/loadbalancer-healthcheck-enabled: "true" # Whether to enable health checking. Values: true and false
    ingress.vke.volcengine.com/loadbalancer-healthcheck-protocol: "http" # The health check protocol. Valid values include http and tcp. In this example, http is used.
    ingress.vke.volcengine.com/loadbalancer-healthcheck-domain: "example.com"  # The domain name for health checks.
    ingress.vke.volcengine.com/loadbalancer-healthcheck-path: "/"  # Health check path (default: "/").
    ingress.vke.volcengine.com/loadbalancer-healthcheck-method: "GET"  # The health check method. Valid values include  GET and HEAD.
    ingress.vke.volcengine.com/loadbalancer-healthcheck-httpcode: "http_2xx,http_3xx"  # Status codes of health checks. Values: http_2xx (default), http_3xx (default), http_4xx, and http_5xx.
    ingress.vke.volcengine.com/loadbalancer-healthcheck-timeout: "2"  # The response timeout for a health check. Value range: 1-60
    ingress.vke.volcengine.com/loadbalancer-healthcheck-interval: "2"  # The time interval for performing health checks. The valid range is 1 to 300 seconds.
    ingress.vke.volcengine.com/loadbalancer-healthy-threshold: "3"  # The number of health checks required to determine that back-end servers are normal. Value range: 2 to 10
    ingress.vke.volcengine.com/loadbalancer-unhealthy-threshold: "3"  # The number of health checks required to determine that back-end servers are unhealthy. Value range: 2 to 10
  name: alb-ingress      # The custom Ingress name.
  namespace: default     # The namespace of the Ingress.
spec:
  ingressClassName: alb  # The name of the ALBInstance.
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


Here are the descriptions for the annotations included in the YAML file.


|Parameter |Type |Description |default value |
|---|---|---|---|
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-enabled |String |Whether to enable health check. Valid values:<br><br><br>* **true**: Enable health checking.<br><br>* **false**: Disable health checking. |true |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-protocol |String |The health check protocol. In this example, set the value to **http**. |http |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-domain |String |The domain name for health checks. ALB populates this domain name in the host field.<br><br>If no domain name is configured, the host field is left empty, and ALB does not include the host field in requests and the default domain name (internal IP address of the back\-end server group) will apply. |No |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-path |String |Health check path. The default path is `/`. |/ |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-method |String |The health check method. Available values: ** GET, HEAD**. |GET |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-httpcode |String |The status code for a normal health check.<br><br>Values: http_2xx, http_3xx, http_4xx, and http_5xx. |http_2xx,http_3xx |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-timeout |String |The response timeout for a health check.<br><br><br>* Value range: 1–60<br><br>* Unit: seconds |2 |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-interval |String |The time interval for performing health checks.<br><br><br>* Value range: 1–300<br><br>* Unit: seconds |2 |
|ingress.vke.volcengine.com/loadbalancer\-healthy\-threshold |String |The number of consecutive health check requests required to determine that the backend server is running properly.<br><br><br>* Value range: 2–10<br><br>* Unit: times |3 |
|ingress.vke.volcengine.com/loadbalancer\-unhealthy\-threshold |String |The number of consecutive health check requests required to determine that the backend server is not running properly.<br><br><br>* Value range: 2–10<br><br>* Unit: times |3 |


<span id=".6YWN572uLXRjcC3ljY_orq7nmoTlgaXlurfmo4Dmn6U="></span>
### Configuring TCP health checks

An ALB Ingress supports TCP health checks for backend server groups based on annotations. The following is an example YAML with comments for annotations.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    ingress.vke.volcengine.com/loadbalancer-healthcheck-enabled: "true" # Whether to enable health checking. Values: true and false
    ingress.vke.volcengine.com/loadbalancer-healthcheck-protocol: "tcp" # The health check protocol. Valid values: http and tcp In this example, set the value to tcp.
    ingress.vke.volcengine.com/loadbalancer-healthcheck-timeout: "2"  # The response timeout for a health check. Value range: 1-60
    ingress.vke.volcengine.com/loadbalancer-healthcheck-interval: "2"  # The time interval for performing health checks. The valid range is 1 to 300 seconds.
    ingress.vke.volcengine.com/loadbalancer-healthy-threshold: "3"  # The number of health checks required to determine that back-end servers are normal. Value range: 2 to 10
    ingress.vke.volcengine.com/loadbalancer-unhealthy-threshold: "3"  # The number of health checks required to determine that back-end servers are unhealthy. Value range: 2 to 10
  name: alb-ingress      # The custom Ingress name.
  namespace: default     # The namespace of the Ingress.
spec:
  ingressClassName: alb  # The name of the ALBInstance.
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


Here are the descriptions for the annotations included in the YAML file.


|Parameter |Type |Description |default value |
|---|---|---|---|
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-enabled |String |Whether to enable health check. Valid values:<br><br><br>* **true**: Enable health checking.<br><br>* **false**: Disable health checking. |true |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-protocol |String |The health check protocol. In this example, set the value to **tcp**. |http |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-timeout |String |The response timeout for a health check.<br><br><br>* Value range: 1–60<br><br>* unit: seconds |2 |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-interval |String |The time interval for performing health checks.<br><br><br>* Value range: 1–300<br><br>* Unit: seconds |2 |
|ingress.vke.volcengine.com/loadbalancer\-healthy\-threshold |String |The number of consecutive health check requests required to determine that the backend server is running properly.<br><br><br>* Value range: 2–10<br><br>* Unit: times |3 |
|ingress.vke.volcengine.com/loadbalancer\-unhealthy\-threshold |String |The number of consecutive health check requests required to determine that the backend server is not running properly.<br><br><br>* Value range: 2–10<br><br>* Unit: times |3 |


<span id=".5Li65oyH5a6a5ZCO56uv5pyN5Yqh57uE6YWN572u5YGl5bq35qOA5p-l"></span>
### Configuring health checks for the specified backend service group

The aforementioned health check configurations based on HTTP and TCP apply to all back\-end server groups created by an ALB Ingress. To configure a different health check policy for a specified backend server group (in this example, `second.example.com`), use the annotation in the following example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress
  annotations:
    ingress.vke.volcengine.com/loadbalancer-rules-configs: |
        [
            {
                "host": "second.example.com",
                "path": "/",
                "healthCheck":
                 {
                   "enabled": true,
                   "protocol": "http",
                   "method": "GET",
                   "httpcode": "http_2xx,http_3xx",
                   "timeout": 2,
                   "interval": 2,
                   "healthyThreshold": 3,
                   "unhealthyThreshold": 3
                }
            }
        ]
spec:
  ingressClassName: alb # The name of the ALBInstance.
  rules:
  - host: first.example.com
    http:
      paths:
      - pathType: Prefix
        path: /
        backend:
          service:
            name: service-demo-a
            port:
              number: 80
  - host: second.example.com
    http:
      paths:
      - pathType: Prefix
        path: /
        backend:
          service:
            name: service-demo-b
            port:
              number: 80
```


The following table describes fields in the `ingress.vke.volcengine.com/loadbalancer-rules-configs` annotation.


|Parameter |Type |Description |default value |
|---|---|---|---|
|host |String |The domain name that the rule applies to. |No |
|path |String |The path that the rule applies to. |No |
|healthCheck |Array of healthCheck |The health check rules for back\-end server groups. |No |


<span id="healthcheck"></span>
#### healthCheck


|Parameter |Type |Description |default value |
|---|---|---|---|
|enabled |Boolean |Whether to enable health checking for the backend service group. Valid values:<br><br><br>* **true**: Enable health checking for the specified backend service group.<br><br>* **false**: Disable health checking for the specified backend service group. |No |
|protocol |String |The protocol for health checks. In this case, use http. |No |
|method |String |The health check method. Available values: GET, HEAD. |HEAD |
|httpcode |String |The HTTP status code for a normal health check. Values: http_2xx, http_3xx, http_4xx, and http_5xx. |http_2xx,http_3xx |
|timeout |Integer |The response timeout for the health check. It will be determined to be an anomaly if the backend server does not respond correctly within the specified time. The value range is 1 to 60 seconds.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The response timeout must be less than or equal to the check interval.</div><br> |2 |
|interval |Integer |health check interval. The valid range is 1 to 300 seconds. |2 |
|healthyThreshold |Integer |The health threshold for health checking. The threshold is the number of consecutive health checks: if that many consecutive checks on a back\-end server pass, the server is considered healthy. The value range is 2 to 10. |3 |
|unhealthyThreshold |Integer |The threshold for an unhealthy result of health checking. The threshold is the number of consecutive health checks: if all consecutive checks on a back\-end server fail, the server is considered unhealthy. The value range is 2 to 10. |3 |


<span id=".6YWN572u6L2s5Y-R5rWB6YeP6ZmQ6YCf"></span>
## Configuring speed limits for forwarded traffic

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta · Apply for trial</strong></a>] This feature is currently in the <strong>beta</strong> stage. To use this feature, submit an application.</div>


An ALB Ingress supports speed limit configurations for forwarded traffic via annotations. The following content provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    ingress.vke.volcengine.com/loadbalancer-rules-configs: |   # Configure traffic speed limiting.
      [
          {
              "host": "example.com", 
              "path": "/", 
              "trafficLimitQps": 2000 
          }
      ]
  name: alb-ingress # The custom Ingress name.
  namespace: default # Namespace of the Ingress
spec:
  ingressClassName: alb  # The name of the ALBInstance.
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


The following table describes fields in the `ingress.vke.volcengine.com/loadbalancer-rules-configs` annotation.


|Parameter |Type |Description |default value |
|---|---|---|---|
|host |String |The domain name that the rule applies to. |No |
|path |String |The path the rule applies to. |No |
|trafficLimitQps |Integer |The requests per second for the forwarding rule. The value range is 100 to 100,000.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not specify a value, no traffic limit is applied.</div><br> |No |


<span id=".6YWN572u6L2s5Y-R6KeE5YiZ6YeN5a6a5ZCR"></span>
## Configuring redirection

An ALB Ingress supports redirection through annotation. The following content provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: alb-ingress
  annotations:
    ingress.vke.volcengine.com/loadbalancer-rules-configs: |
      [
            {
                "host": "first.example.com",
                "path": "/",
                "ruleAction": "Redirect",
                "redirectConfig": 
                     {
                       "domain": "test.com",
                       "uri": "/docs",
                       "port": 8080,
                       "httpCode": "302",
                       "protocol": "HTTPS"
                    }
            }
      ]
spec:
  ingressClassName: alb # The name of the ALBInstance.
  rules:
  - host: first.example.com
    http:
      paths:
      - pathType: Prefix
        path: /
        backend:
          service:
            name: redirect # The fixed value 'redirect' indicate redirecting.
            port:
              name: use-annotation # The fixed value 'redirect' indicate redirecting.
  - host: second.example.com
    http:
      paths:
      - pathType: Prefix
        path: /
        backend:
          service:
            name: service
            port:
              number: 80
```


The following table describes fields in the `ingress.vke.volcengine.com/loadbalancer-rules-configs` annotation.


|Parameter |Type |Description |default value |
|---|---|---|---|
|host |String |The domain name that incoming requests must match. |No |
|path |String |The  path pattern to match. |No |
|ruleAction |String |The action to take when rule conditions are met. Valid values:<br><br><br>* null: By default, requests are forwarded to the back\-end server group.<br><br>* **Redirect**: Redirect is enabled. |Redirect |
|redirectConfig |Array of redirectConfig |The redirection rules. |No |


<span id="redirectconfig"></span>
#### redirectConfig


|Parameter |Type |Description |default value |
|---|---|---|---|
|domain |String |The target domain name for redirection. Exact domain matching is supported.<br><br>If this parameter is not specified, it will be assigned the default value (null), which means it will match the requested domain. |No |
|uri |String |The target URI for redirection. The value must start with a forward slash (`/`). The value can contain only letters, digits, and special characters `-`, `_`, `/`, `.`, `%`, `?`, `#`, `&`, `=`. The length is limited to 1 to 128 characters.<br><br>If this parameter is not specified, it will be assigned the default value (null), which means it will match the requested URI. |null |
|port |Integer |The port for redirection. The value can range from 1 to 65535.<br><br>If this parameter is not specified, it will be assigned the default value (null), which means it will match the request port. |null |
|httpCode |String |The redirection status code. Supports redirection status codes: 301, 302, 307, and 308.<br><br>The default value is 301. |301 |
|protocol |String |The protocol for redirection. Supported protocols include HTTP and HTTPS.<br><br>The default protocol is HTTPS. |HTTPS |
