---
title: "Gateway supported annotations"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Annotations_Supported_by_the_Gateway"
---

An APIG Ingress allows you to configure diverse routing capabilities based on annotations. This topic describes the scenarios and methods of using annotations to configure an APIG Ingress.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The annotations in YAML files are case\-sensitive.</div>


<span id="L9dAoBbb"></span>
## Configuring canary releases

APIG Ingresses support configuring canary releases through annotations and allow traffic splitting based on headers or service weights. For details, see [Using APIG Ingresses to implement canary releases and blue-green deployments](https://docs.byteplus.com/en/docs/vke/Implement_canary_release_and_blue-green_deployment_using_APIG_Ingress).

<span id="m8Efoj4R"></span>
## Configuring rewrites

APIG Ingresses support rewriting based on annotations. The following YAML file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # The namespace of the Ingress.
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # The name of the APIGInstance resource.
    nginx.ingress.kubernetes.io/rewrite-target: /test/ # Configuration rewrite. The original path is rewritten to the specified path.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # The domain name that is externally accessible.
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


|Parameter |Type |Description |Default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/rewrite\-target |String |The path rewrite for the APIG instance. This allows the original path in the Ingreess to be rewritten to a specified target. Group capture is supported.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><code>rewrite-target</code> supports exact matching and prefix matching.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the original <code>path</code> ends with <code>/</code>, the path specified by <code>rewrite-target</code> must also end with <code>/</code>. If the original <code>path</code> does not end with <code>/</code>, the path specified by <code>rewrite-target</code> cannot end with <code>/</code> either.</div><br> |No |


<span id="VXk6ruN9"></span>
## Configuring CORS

APIG Ingresses support configuring cross\-origin resource sharing (CORS) through annotations. The following file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # The namespace of the Ingress.
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # The name of the APIGInstance resource.
    nginx.ingress.kubernetes.io/enable-cors: "true" # Enable or disable CORS.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # The domain name that is externally accessible.
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
|nginx.ingress.kubernetes.io/enable\-cors |String |Specifies whether to enable CORS. Available values:<br><br><br>* **true**<br><br>* **false** |No |


<span id="BemNBgr2"></span>
## Configuring load balancing

APIG Ingresses support configuring load balancing algorithms based on annotations. The following file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # The namespace of the Ingress.
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # The name of the APIGInstance resource.
    nginx.ingress.kubernetes.io/load-balance: round_robin # The load balancing algorithm.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # The domain name that is externally accessible.
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The Service port number to forward to.
```


Here are the descriptions for the annotations included in the YAML file.


|Parameter |Type |Description |Default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/load\-balance |String |Specifies a load balancing algorithm. Valid values:<br><br><br>* **round_robin**: load balancing based on round\-robin scheduling.<br><br>* **least_conn**: load balancing based on the minimum number of requests.<br><br>* **random**: random load balancing.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Exponential Weighted Moving Average (EWMA ) algorithm is not supported. If you set the EWMA algorithm, it will automatically revert to the round\-robin method as the default.</div><br> |round_robin |


<span id="Bmn4eAke"></span>
## Configuring timeouts

APIG Ingresses support configuring timeouts through annotations. The following file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # The namespace of the Ingress.
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # The name of the APIGInstance resource.
    apig.ingress.kubernetes.io/timeout: 30 # The request timeout for the APIG extension, in seconds.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # The domain name that is externally accessible.
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
|apig.ingress.kubernetes.io/timeout |Integer |Specifies the request timeout in seconds for the APIG extension. For example, if the value is set to 30, the gateway will return a `504 timeout` error message when the upstream service does not return a response within 30 seconds. |30 |


<span id="zCvJCpQX"></span>
## Configuring HTTP redirection

APIG Ingresses support configuring HTTP redirection to HTTPS through annotations. The following file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # The namespace of the Ingress.
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # The name of the APIGInstance resource.
    nginx.ingress.kubernetes.io/ssl-redirect: "true" # HTTP redirection to HTTPS.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # The domain name that is externally accessible.
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
          path: / # The matching path for the request.
          backend:
            service:
              name: service-demo # The name of the service to forward requests to.
              port: 
                number: 80 # The Service port number to forward to.
```


Here are the descriptions for the annotations included in the YAML file.


|Parameter |Type |Description |Default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/ssl\-redirect |String |Specifies whether to redirect HTTP requests to HTTPS. Available values:<br><br><br>* **true**<br><br>* **false** |No |


<span id="hUuEcYTi"></span>
## Configuring headers

APIG Ingresses support configuring headers through annotations. This support allows specified headers to be added, modified, or deleted after requests or responses are received. The following content in Yaml is an example with descriptions in it:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # The namespace of the Ingress.
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # The name of the APIGInstance resource.
    apig.ingress.kubernetes.io/request-header-control-add: key value # Add the specified header when forwarding a request to the backend service.
    apig.ingress.kubernetes.io/request-header-control-update: key value # Modify the specified header when forwarding a request to the backend service.
    apig.ingress.kubernetes.io/request-header-control-remove: key value # Delete the specified header when forwarding a request to the backend service.
    apig.ingress.kubernetes.io/response-header-control-add: key value # Add the specified header before forwarding the response from the backend service to the client.
    apig.ingress.kubernetes.io/response-header-control-update: key value # Modify the specified header before forwarding the response from the backend service to the client.
    apig.ingress.kubernetes.io/response-header-control-remove: key value # Delete the specified header from the response before forwarding the response to the client.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # The domain name that is externally accessible.
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


|Parameter |Type |Description |Default value |
|---|---|---|---|
|apig.ingress.kubernetes.io/request\-header\-control\-add |String |Adds the specified header when forwarding a request to the backend service. If the header already exists, the specified value is appended to the original value. The syntax is as follows:<br><br><br>* A single header: use the Key Value format.<br><br>* Multiple headers: use the YAML pipe character `\|` to keep each Key Value pair on a separate line. |No |
|apig.ingress.kubernetes.io/request\-header\-control\-update |String |Modifies the specified header when forwarding a request to the backend service. If the header already exists, the specified header value overwrites the existing header value. The syntax is as follows:<br><br><br>* A single header: use the Key Value format.<br><br>* Multiple headers: use the YAML pipe character `\|` to keep each Key Value pair on a separate line. |No |
|apig.ingress.kubernetes.io/request\-header\-control\-remove |String |Deletes the specified header from the request when forwarding the request to the backend service. The syntax is as follows:<br><br><br>* A single header: use the Key Value format.<br><br>* Multiple headers: use the YAML pipe character `\|` to keep each Key Value pair on a separate line. |No |
|apig.ingress.kubernetes.io/response\-header\-control\-add |String |Adds the specified header before forwarding the response from the backend service to the client. If the header already exists, the specified value is appended to the original value. The syntax is as follows:<br><br><br>* A single header: use the Key Value format.<br><br>* Multiple headers: use the YAML pipe character `\|` to keep each Key Value pair on a separate line. |No |
|apig.ingress.kubernetes.io/response\-header\-control\-update |String |Modifies the specified header before forwarding the response from the backend service to the client. If the header already exists, the specified header value overwrites the existing header value. The syntax is as follows:<br><br><br>* A single header: use the Key Value format.<br><br>* Multiple headers: use the YAML pipe character `\|` to keep each Key Value pair on a separate line. |No |
|apig.ingress.kubernetes.io/response\-header\-control\-remove |String |Deletes the specified header from the response before forwarding the response to the client. The syntax is as follows:<br><br><br>* A single header: use the Key Value format.<br><br>* Multiple headers: use the YAML pipe character `\|` to keep each Key Value pair on a separate line. |No |


<span id="MPU924XD"></span>
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


<span id="QpE4Z0Nu"></span>
## Configuring a protocol for backend services

APIG Ingresses support configuring a protocol for backend services through annotations. The following file provides an example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: apig-ingress # The name of the Ingress.
  namespace: default  # The namespace of the Ingress.
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # The name of the APIGInstance resource.
    nginx.ingress.kubernetes.io/backend-protocol: HTTP # The protocol used by backend services. Support protocols include HTTP, HTTP2, and gRPC.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # The domain name that is externally accessible.
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


|Parameter |Type |Description |Default value |
|---|---|---|---|
|nginx.ingress.kubernetes.io/backend\-protocol |String |Specifies a protocol for backend services. Supported protocols are **HTTP, HTTP2**, and **gRPC.**  |HTTP |
