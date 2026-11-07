---
title: "Configuring APIG Ingresses by using annotations"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configure_APIG_Ingress_Using_Annotation"
---

An APIG Ingress allows you to configure diverse routing capabilities based on annotations. This topic describes the scenarios and methods of using annotations to configure an APIG Ingress.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">The annotations in YAML files are case\-sensitive.</div>


<span id=".6YWN572u54Gw5bqm5Y-R5biD"></span>
## Configuring canary releases

APIG Ingresses support configuring canary releases through annotations and allow traffic splitting based on headers or service weights. The following content in Yaml is an example with descriptions in it:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
    nginx.ingress.kubernetes.io/canary: "true" # Whether to enable canary deployments. Values include true (enabling it)and false (disabling it).
    nginx.ingress.kubernetes.io/canary-by-header: "Region" # Header-based traffic splitting.
    nginx.ingress.kubernetes.io/canary-by-header-value: "beijing" # When a request contains the specified header with the header value of beijing, the request will be forwarded.
    nginx.ingress.kubernetes.io/canary-weight: "25" # Weight-based traffic splitting.
    nginx.ingress.kubernetes.io/canary-weight-total: "100" # The total service weight.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # Service port number to forward to
```


The following table describes the annotations.


|Paramete |Type |Description |default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/canary |String |Enable the canary release feature. Valid values:<br><br><br>* `true`: Enables canary deployments.<br><br>* `false`: Disables canary deployments. |No |
|nginx.ingress.kubernetes.io/canary\-by\-header |String |Implement canary release based on headers, and traffic is routed to the service specified in the canary Ingress. |No |
|nginx.ingress.kubernetes.io/canary\-by\-header\-value |String |When the header value in the request matches the configuration, the request will be routed to the service specified in the canary Ingress. |No |
|nginx.ingress.kubernetes.io/canary\-weight |String |Implement canary release based on weight, and traffic is randomly routed to the service specified in the canary Ingress based on the assigned weights. |No |
|nginx.ingress.kubernetes.io/canary\-weight\-total |String |Specify the total weight during traffic splitting based on weight. |100 |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For an example of configuring canary and blue\-green deployments, see <a href="https://docs.byteplus.com/en/docs/vke/Implement_canary_release_and_blue-green_deployment_using_APIG_Ingress">Implementing canary release and blue\-green deployments based on APIG Ingresses</a>.</div>


<span id=".6YWN572u6YeN5YaZ"></span>
## Configuring rewrites

APIG Ingresses support rewriting based on annotations. The following YAML file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
    nginx.ingress.kubernetes.io/rewrite-target: "/test/" # Configuration rewrite. The original path is rewritten to the specified path.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


The following table describes the annotations.


|Parameter |Type |Description |default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/rewrite\-target |String |The path rewrite for the APIG instance. This allows the original path in the Ingress to be rewritten to a specified target. Group capture is supported.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>rewrite-target</code> supports exact matching and prefix matching.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the original <code>path</code> ends with <code>/</code>, the path specified by <code>rewrite-target</code> must also end with <code>/</code>. If the original <code>path</code> does not end with <code>/</code>, the path specified by <code>rewrite-target</code> cannot end with <code>/</code>, either.</div><br> |No |


<span id=".6YWN572u6Leo5Z-f"></span>
## Configuring CORS

APIG Ingresses support configuring cross\-origin resource sharing (CORS) through annotations. The following file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
    nginx.ingress.kubernetes.io/enable-cors: "true" # Enable or disable CORS.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


The following table describes the annotations.


|Parameter |Type |Description |default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/enable\-cors |String |Specifies whether to enable CORS. Valid values:<br><br><br>* **true**<br><br>* **false** |No |


<span id=".6YWN572u6LSf6L295Z2H6KGh"></span>
## Configuring load balancing

APIG Ingresses support configuring load balancing algorithms based on annotations. The following file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
    nginx.ingress.kubernetes.io/load-balance: "round_robin" # Specify a load balancing algorithm. Available values include round_robin, least_conn, and random.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


The following table describes the annotations.


|Parameter |Type |Description |default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/load\-balance |String |Specifies a load balancing algorithm. Valid values:<br><br><br>* **round_robin**: load balancing based on round\-robin scheduling.<br><br>* **least_conn**: load balancing based on the minimum number of requests.<br><br>* **random**: random load balancing.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Exponential Weighted Moving Average (EWMA) algorithm is not supported. If you set the EWMA algorithm, it will automatically revert to the round\-robin method as the default.</div><br> |round_robin |


<span id=".6YWN572u6LaF5pe2"></span>
## Configuring timeouts

APIG Ingresses support configuring timeouts through annotations. The following file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
    apig.ingress.kubernetes.io/timeout: 30 # The request timeout for the APIG extension, in seconds.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


The following table describes the annotations.


|Parameter |Type |Description |default value |
|---|---|---|---|
|apig.ingress.kubernetes.io/timeout |Integer |Specifies the request timeout in seconds for the APIG extension. For example, if the value is set to 30, the gateway will return a `504 timeout` error message when the upstream service does not return a response within 30 seconds. |30 |


<span id=".6YWN572uLWh0dHAt6YeN5a6a5ZCR"></span>
## Configuring redirection

APIG Ingresses support configuring HTTP redirection to HTTPS through annotations. The following file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
    nginx.ingress.kubernetes.io/ssl-redirect: "true" # HTTP redirection to HTTPS.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


The following table describes the annotations.


|Parameter |Type |Description |default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/ssl\-redirect |String |Whether to redirect HTTP requests to HTTPS. Valid values:<br><br><br>* **true**: Enable redirection from HTTP requests to HTTPS.<br><br>* **false**: Disable redirection from HTTP requests to HTTPS. |No |


<span id="P08ZaISa"></span>
## Configuring retries

APIG Ingresses support annotation\-based retry settings. The following YAML file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
    nginx.ingress.kubernetes.io/proxy-next-upstream: "error timeout" # Configure retry conditions.
    nginx.ingress.kubernetes.io/retriable-status-codes: "429,500,502,503,504" # Configure HTTP status codes for retries.
    nginx.ingress.kubernetes.io/proxy-next-upstream-tries: "3" # Configure the number of retries.
    nginx.ingress.kubernetes.io/proxy-next-upstream-timeout: "20" # Configure the total retry timeout time.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


The following table describes the annotations.


|Parameter |Type |Description |default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/proxy\-next\-upstream |String |Specifies retry conditions. Valid values:<br><br><br>* `error`: Backend connection errors, such as service unavailable and port unreachable.<br><br>* `timeout`: Connection or read/write timeout.<br><br>* `http_503`: The 503 error returned by the back\-end service (indicating service unavailablity).<br><br>* `http_502`: The 502 error returned by the back\-end service (indicating a gateway error).<br><br>* `http_504`: The 504 error returned by the back\-end service (indicating a gateway timeout).<br><br>* `invalid_header`: Invalid response headers from the backend.<br><br>* `off`: Retry disabled.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify multiple retry conditions separated by spaces. For example, you can specify the <code>nginx.ingress.kubernetes.io/proxy-next-upstream: "error timeout"</code> annotation.</div><br> |No |
|nginx.ingress.kubernetes.io/retriable\-status\-codes |String |Specifies the HTTP status codes as a retry condition. For example, `429`, `500`, and `502`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify multiple HTTP status codes separated by commas (<code>,</code>). For example, you can specify the <code>nginx.ingress.kubernetes.io/retriable-status-codes: "429,500,502,503,504"</code> annotation.</div><br> |No |
|nginx.ingress.kubernetes.io/proxy\-next\-upstream\-tries |String |Specifies the maximum number of retry attempts on a request. The value is a positive integer. This number includes the initial request, meaning that if you set it to 1, retrying is prohibited. |No |
|nginx.ingress.kubernetes.io/proxy\-next\-upstream\-timeout |String |Specifies the total timeout for all retry requests. When the timeout is reached, retries are immediately stopped and an error is returned. The time (in seconds) is an integer value. If you set the value to 0, the retry time is unlimited. |0 |


<span id="BPkqt31R"></span>
## Configuring headers

APIG Ingresses support configuring headers through annotations. This support allows specified headers to be added, modified, or deleted after requests or responses are received. The following content in Yaml is an example with descriptions in it:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
    apig.ingress.kubernetes.io/request-header-control-add: "key value" # Add the specified header when forwarding a request to the backend service.
    apig.ingress.kubernetes.io/request-header-control-update: "key value" # Modify the specified header when forwarding a request to the backend service.
    apig.ingress.kubernetes.io/request-header-control-remove: "key value" # Delete the specified header when forwarding a request to the backend service.
    apig.ingress.kubernetes.io/response-header-control-add: "key value" # Add the specified header before forwarding the response from the backend service to the client.
    apig.ingress.kubernetes.io/response-header-control-update: "key value" # Modify the specified header before forwarding the response from the backend service to the client.
    apig.ingress.kubernetes.io/response-header-control-remove: "key value" # Delete the specified header from the response before forwarding the response to the client.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


The following table describes the annotations.


|Parameter |Type |Description |default value |
|---|---|---|---|
|apig.ingress.kubernetes.io/request\-header\-control\-add |String |Adds the specified header when forwarding a request to the backend service. If the header already exists, the specified value is appended to the original value. The syntax is as follows:<br><br><br>* A single header: Use the key\-value format.<br><br>* Multiple headers: Use the vertical bar (`\|`) in YAML to place each key\-value pair on a separate line. |No |
|apig.ingress.kubernetes.io/request\-header\-control\-update |String |Modifies the specified header when forwarding a request to the backend service. If the header already exists, the specified header value overwrites the existing header value. The syntax is as follows:<br><br><br>* A single header: Use the key\-value format.<br><br>* Multiple headers: Use the vertical bar (`\|`) in YAML to place each key\-value pair on a separate line. |No |
|apig.ingress.kubernetes.io/request\-header\-control\-remove |String |Deletes the specified header from the request when forwarding the request to the backend service. The syntax is as follows:<br><br><br>* A single header: Use the key\-value format.<br><br>* Multiple headers: Use the vertical bar (`\|`) in YAML to place each key\-value pair on a separate line. |No |
|apig.ingress.kubernetes.io/response\-header\-control\-add |String |Adds the specified header before forwarding the response from the backend service to the client. If the header already exists, the specified value is appended to the original value. The syntax is as follows:<br><br><br>* A single header: Use the key\-value format.<br><br>* Multiple headers: Use the vertical bar (`\|`) in YAML to place each key\-value pair on a separate line. |No |
|apig.ingress.kubernetes.io/response\-header\-control\-update |String |Modifies the specified header before forwarding the response from the backend service to the client. If the header already exists, the specified header value overwrites the existing header value. The syntax is as follows:<br><br><br>* A single header: Use the key\-value format.<br><br>* Multiple headers: Use the vertical bar (`\|`) in YAML to place each key\-value pair on a separate line. |No |
|apig.ingress.kubernetes.io/response\-header\-control\-remove |String |Deletes the specified header from the response before forwarding the response to the client. The syntax is as follows:<br><br><br>* A single header: Use the key\-value format.<br><br>* Multiple headers: Use the vertical bar (`\|`) in YAML to place each key\-value pair on a separate line. |No |


<span id=".6YWN572u5Li-5L6L"></span>
### Configuration examples

When APIG forwards HTTP requests to a backend service, the service may need to extract client\-specific details, such as IP addresses and port numbers, from the request headers to process the client information. For example, the backend service may want to obtain client information by defining custom request headers such as X\-Real\-IP and X\-Real\-Port.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Envoy supports adding dynamic values  to request and response headers. When you add dynamic values, use the percent sign (%) to separate variable names. For supported dynamic values, see <a href="https://cloudnative.to/envoy/configuration/http/http_conn_man/headers.html">Envoy documentation</a>.</div>


```yaml
annotations:
  # Add request headers. You can specify dynamic values as header values.
  apig.ingress.kubernetes.io/request-header-control-add: |-
    x-Real-IP %DOWNSTREAM_REMOTE_ADDRESS_WITHOUT_PORT%
    X-Real-Port %DOWNSTREAM_REMOTE_PORT%
  apig.ingress.kubernetes.io/request-header-control-update: |-
    aaa bb&*!b
    ccc ddd
  apig.ingress.kubernetes.io/request-header-control-remove: |-
    age
```


The previous annotation settings are expected to achieve the following effects:


* When the gateway accesses the upstream, two request headers are added: `x-Real-IP=client IP` and `X-Real-Port=client port`.

* When the gateway accesses the upstream, two request headers are overwritten: `aaa=bb&*!b` and `ccc=ddd`.

* When the gateway accesses the upstream, the request header with the key "age" is removed.


<span id="ZN0DJHRo"></span>
## Configuring session affinity

APIG Ingresses support annotation\-based session affinity settings. The following YAML file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: "apig-instance-demo" # Specify the APIGInstance resource name
    nginx.ingress.kubernetes.io/affinity: "cookie" # Configure session affinity. Only the cookie option is supported.
    nginx.ingress.kubernetes.io/session-cookie-name: "cookie-demo" # Specify the name of the cookie for implementing session affinity.
    nginx.ingress.kubernetes.io/session-cookie-path: "/" # Specify the path of the cookie for session affinity.
    nginx.ingress.kubernetes.io/session-cookie-max-age: "86400" # Specify the timeout (in seconds) of the cookie for session affinity. It defaults to session duration.
    nginx.ingress.kubernetes.io/session-cookie-expires: "86400" # Specify the timeout (in seconds) of the cookie for session affinity. It defaults to session duration.
spec:
  ingressClassName: apig
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


The following table describes the annotations.


|Parameter |Type |Description |Default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/affinity |String |Configures session affinity to allow requests from the same client to always be forwarded to the same back\-end service. The only supported value is `cookie`, which indicates cookie\-based session affinity. |cookie |
|nginx.ingress.kubernetes.io/session\-cookie\-name |String |Specifies the name of the cookie for session affinity. |No |
|nginx.ingress.kubernetes.io/session\-cookie\-path |String |Specifies the path of the cookie for session affinity. The browser will carry the specified cookie only when the client accesses this path, thereby achieving session affinity. |/ |
|nginx.ingress.kubernetes.io/session\-cookie\-max\-age |String |Specifies the timeout (in seconds) of the cookie for session affinity. It defaults to session duration. |No |
|nginx.ingress.kubernetes.io/session\-cookie\-expires |String |Specifies the timeout (in seconds) of the cookie for session affinity. It defaults to session duration.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is highly compatible and supports IE and other legacy browsers.</div><br> |No |


<span id="nfQyhJ3A"></span>
## Configuring a protocol for backend services

APIG Ingresses support configuring a protocol for backend services through annotations. The following file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # Namespace of the Ingress
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # Specify the APIGInstance resource name
    nginx.ingress.kubernetes.io/backend-protocol: "HTTP" # The protocol used by backend services. Support protocols include HTTP, HTTP2, and gRPC.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain names for external access
      http:
        paths:
        - pathType: Prefix # The path matching rule. Values include Exact, Prefix, and Regex.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The service port number to forward to.
```


The following table describes the annotations.


|Parameter |Type |Description |default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/backend\-protocol |String |Specifies a protocol for backend services. Supported protocols are **HTTP, HTTP2**, and **gRPC.**  |HTTP |
