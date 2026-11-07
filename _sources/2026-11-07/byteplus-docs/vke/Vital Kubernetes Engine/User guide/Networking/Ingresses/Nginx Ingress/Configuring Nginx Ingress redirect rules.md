---
title: "Configuring Nginx Ingress redirect rules"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-redirect-rules-for-an-Nginx-Ingress"
---

Nginx Ingress can redirect traffic permanently and temporarily, as well as from HTTP to HTTPS. This topic introduces how to configure the Nginx Ingress redirect feature.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cluster has been connected. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* Installed ingress\-nginx add\-on. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).


<span id=".6YWN572u5rC45LmF6YeN5a6a5ZCR"></span>
## Configure permanent redirection

An NGINX Ingress allows you to configure permanent redirection by using an annotation. The following content includes a configuration example and annotation descriptions:

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress # Ingress name
  annotations:
    nginx.ingress.kubernetes.io/permanent-redirect: "https://www.volcengine.com" # Redirect to the target URL.
spec:
  ingressClassName: nginx # Specify an Ingress controller.
  rules:
  - host: example.com # The domain name in the forwarding rule.
    http:
      paths:
      - backend:
          service:
            name: service-demo # The name of the service where requests are forwarded.
            port:
              number: 80 # The port that the service opens to receive forwarded requests.
        path: / # The access path.
        pathType: Prefix # Path type. Available values include Exact (exact match) and Prefix (prefix match).
```


The following table describes the annotations.


|Key |Type |Required |Description |default value |
|---|---|---|---|---|
|nginx.ingress.kubernetes.io/permanent\-redirect |String |Yes |The target website address to redirect to. |No |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, the status code for a permanent redirect is <code>301</code>.</div>


<span id=".6YWN572u5rC45LmF6YeN5a6a5ZCR6L-U5Zue54q25oCB56CB"></span>
## Configuring status code for permanent redirect

An NGINX Ingress allows you to configure permanent redirection with the specified HTTP status code by using annotations. The following content includes a configuration example and annotation descriptions:

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress # Ingress name
  annotations:
    nginx.ingress.kubernetes.io/permanent-redirect: "https://www.volcengine.com" # Redirect to the target URL.
    nginx.ingress.kubernetes.io/permanent-redirect-code: "308" # The HTTP status code for the redirection.
spec:
  ingressClassName: nginx # Specify an Ingress controller.
  rules:
  - host: example.com # The domain name in the forwarding rule.
    http:
      paths:
      - backend:
          service:
            name: service-demo # The name of the service where requests are forwarded.
            port:
              number: 80 # The port that the service opens to receive forwarded requests.
        path: / # The access path.
        pathType: Prefix # Path type. Available values include Exact (exact match) and Prefix (prefix match).
```


The following table describes the annotations.


|Key |Type |Required |Description |default value |
|---|---|---|---|---|
|nginx.ingress.kubernetes.io/permanent\-redirect |String |Yes |Redirect to the specified website. |No |
|nginx.ingress.kubernetes.io/permanent\-redirect\-code |String |Yes |Specify the status code returned when redirecting. Available values: `301` or `308`. |No |


<span id=".6YWN572u5Li05pe26YeN5a6a5ZCR"></span>
## Configuring temporary redirection

An NGINX Ingress allows you to configure temporary redirection by using an annotation. The following content includes a configuration example and annotation descriptions:

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress # Ingress name
  annotations:
    nginx.ingress.kubernetes.io/temporal-redirect: "https://www.volcengine.com" # Redirect to the target URL.
spec:
  ingressClassName: nginx # Specify an Ingress controller.
  rules:
  - host: example.com # The domain name in the forwarding rule.
    http:
      paths:
      - backend:
          service:
            name: service-demo # The name of the service where requests are forwarded.
            port:
              number: 80 # The port that the service opens to receive forwarded requests.
        path: / # The access path.
        pathType: Prefix # Path type. Available values include Exact (exact match) and Prefix (prefix match).
```


The following table describes the annotations.


|Key |Type |Required |Description |Default value |
|---|---|---|---|---|
|nginx.ingress.kubernetes.io/temporal\-redirect |String |Yes |Redirect to the specified website. |No |


<span id=".6YWN572uLWh0dHAt6YeN5a6a5ZCR5YiwLWh0dHBz"></span>
## Configuring redirection from HTTP to HTTPS

An NGINX Ingress allows you to configure redirection from HTTP to HTTPS by using an annotation. The following content includes a configuration example and annotation descriptions:

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress # Ingress name
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "true" # HTTP redirection to HTTPS.
spec:
  ingressClassName: nginx # Specify an Ingress controller.
  rules:
  - host: example.com # The domain name in the forwarding rule.
    http:
      paths:
      - backend:
          service:
            name: service-demo # The name of the service where requests are forwarded.
            port:
              number: 80 # The port that the service opens to receive forwarded requests.
        path: / # The access path.
        pathType: Prefix # Path type. Available values include Exact (exact match) and Prefix (prefix match).
```


The following table describes the annotations.


|Key |Type |Required |Description |default value |
|---|---|---|---|---|
|nginx.ingress.kubernetes.io/ssl\-redirect |Boolean |Yes |Whether to redirect HTTP requests to HTTPS. Valid values:<br><br><br>* **true**: Enable redirection from HTTP requests to HTTPS.<br><br>* **false**: Disable redirection from HTTP requests to HTTPS. |No |


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

The following command is an example of permanent redirection validation. The address `180.xxx.xxx.xxx` is the public or private IP of the CLB configured for the Nginx Ingress.

```Bash
curl -H "Host: example.com" http://180.xxx.xxx.xxx -I -k
```


The following is the expected response showing the redirection details.

```HTML
HTTP/1.1 301 Moved Permanently
Date: Thu, 07 Dec 2023 06:56:48 GMT
Content-Type: text/html
Content-Length: 162
Connection: keep-alive
Location: https://www.volcengine.com
```
