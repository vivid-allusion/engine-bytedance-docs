---
title: "Configuring CLB Ingress through annotations"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-a-CLB-Ingress-using-annotations"
---

CLB Ingress can provide richer features through annotations. This topic introduces the typical scenarios of configuring CLB Ingress through annotations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Read <a href="https://docs.byteplus.com/en/docs/vke/Precautions_for_using_CLB_Ingress">CLB Ingress considerations</a> carefully before getting started.</div>


* <div data-tips="true" data-tips-type="warning">ALB Ingresses offer richer features and greater reliability. To ensure the security and stability of your business, we recommend ALB Ingresses for business deployments in clusters. For details, see <a href="https://docs.byteplus.com/en/docs/vke/ALB-Ingress">ALB Ingress</a>.</div>


* <div data-tips="true" data-tips-type="warning">The annotations in YAML files are case\-sensitive.</div>



<span id=".6YWN572u55uR5ZCs5Zmo"></span>
## Configuring listeners

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A listener can be created based on an existing CLB instance or a new CLB instance. The following examples will use an existing CLB instance. The listeners of CLB Ingress can be configured through annotations. The following is an example YAML with comments for annotations.</div>


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    ingress.vke.volcengine.com/loadbalancer-id: "clb-rrxpqzg37eo0v0x58******"
    ingress.vke.volcengine.com/loadbalancer-scheduler: "wrr" 
    ingress.vke.volcengine.com/loadbalancer-protocol: "http" 
    ingress.vke.volcengine.com/loadbalancer-port: "80" 
  name: clb-ingress
  namespace: default
spec:
  ingressClassName: clb
  rules:
  - host: example.com
    http:
      paths:
      - backend:
          service:
            name: service-demo-a
            port:
              number: 80
        path: /foo
        pathType: Prefix
      - backend:
          service:
            name: service-demo
            port:
              number: 80
        path: /bar
        pathType: Prefix
```


Here are the descriptions for the annotations included in the YAML file.


|Key |Type |Required |Description |Default value |
|---|---|---|---|---|
|ingress.vke.volcengine.com/loadbalancer\-scheduler |String |No |The scheduling algorithms used by the load balancer. Available values:<br><br><br>* **wrr**: The higher the weight of the backend server, the more frequently (probabilistically) it is selected as the forwarding destination.<br><br>* **wlc**: Forward requests to the backend server that has the lowest ratio of **current connections to weight**.<br><br>* **sh**: It is a hash\-based algorithm that forwards requests from the same IP to a single backend server. |wrr |
|ingress.vke.volcengine.com/loadbalancer\-protocol |String |No |The listening protocol of the LoadBalancer instance. Available values:<br><br><br>* **http**: The listening protocol of the LoadBalancer instance is HTTP.<br><br>* **https**: The listening protocol of the LoadBalancer instance is HTTPS. |http |
|ingress.vke.volcengine.com/loadbalancer\-port |Integer |No |The external listening port of LoadBalancer, which is registered to the LoadBalancer service address. The value can range from 1 to 65535. |* HTTPS protocol: 443<br><br>* HTTP protocol: 80 |


<span id=".6YWN572u55u06YCaLXBvZC3mqKHlvI8="></span>
## Configuring LB\-to\-pod direct access mode

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The LB\-to\-pod direct access mode is only effective in clusters running with VPC\-CNI network model.</div>


* <div data-tips="true" data-tips-type="tip">LB\-to\-pod direct access mode can be enabled when specifying an existing CLB instance or creating a new CLB instance. The following examples will use an existing CLB instance. LB\-to\-pod direct access mode can be configured for CLB Ingress through annotations. The following is an example YAML with comments for annotations.</div>



```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    ingress.vke.volcengine.com/loadbalancer-id: "clb-rrxpqzg37eo0v0x58******"
    ingress.vke.volcengine.com/loadbalancer-pass-through: "true"
  name: clb-ingress
  namespace: default
spec:
  ingressClassName: clb
  rules:
  - host: example.com
    http:
      paths:
      - backend:
          service:
            name: service-demo
            port:
              number: 80
        path: /
        pathType: Prefix
```


Here are the descriptions for the annotations included in the YAML file.


|Key |Type |Required |Description |Default value |
|---|---|---|---|---|
|ingress.vke.volcengine.com/loadbalancer\-pass\-through |String |Yes |Whether to enable LB\-to\-pod direct access mode for LoadBalancer. Available values:<br><br><br>* **true**: Enable LB\-to\-pod direct access mode.<br><br>* **false**: Disable LB\-to\-pod direct access mode. |true |


<span id=".6YWN572u5YGl5bq35qOA5p-l"></span>
## Configuring health check

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Health checking can be configured when specifying an existing CLB instance or creating a new CLB instance. The following examples will use an existing CLB instance. Health checking in CLB Ingress can be configured through annotations. The following is an example YAML for annotations.</div>


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    ingress.vke.volcengine.com/loadbalancer-id: "clb-rrxpqzg37eo0v0x58******" 
    ingress.vke.volcengine.com/loadbalancer-healthcheck-enabled: "true" 
    ingress.vke.volcengine.com/loadbalancer-healthcheck-path: "/"
    ingress.vke.volcengine.com/loadbalancer-healthcheck-method: "GET"
    ingress.vke.volcengine.com/loadbalancer-healthcheck-httpcode: "http_2xx,http_3xx"
    ingress.vke.volcengine.com/loadbalancer-healthcheck-timeout: "2" 
    ingress.vke.volcengine.com/loadbalancer-healthcheck-interval: "2" 
    ingress.vke.volcengine.com/loadbalancer-healthy-threshold: "3" 
    ingress.vke.volcengine.com/loadbalancer-unhealthy-threshold: "3" 
  name: clb-ingress
  namespace: default
spec:
  ingressClassName: clb
  rules:
  - host: example.com
    http:
      paths:
      - backend:
          service:
            name: service-demo
            port:
              number: 80
        path: /
        pathType: Prefix
```


Here are the descriptions for the annotations included in the YAML file.


|Key |Type |Required |Description |Default value |
|---|---|---|---|---|
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-enabled |String |Yes |Whether to enable a health check. Available values:<br><br><br>* **true**: Enable health checking.<br><br>* **false**: Disable health checking. |true |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-path |String |No |Health checking path. |/ |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-method |String |No |Request methods for health checking. Available values: ** GET, HEAD**. |GET |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-httpcode |String |No |Set status codes for health checks. Available values: **http_2xx**, **http_3xx**, **http_4xx**, and **http_5xx** |http_2xx,http_3xx |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-timeout |String |No |Specify a timeout for health checking.<br><br><br>* Value range: 1–60<br><br>* Unit: seconds |2 |
|ingress.vke.volcengine.com/loadbalancer\-healthcheck\-interval |String |No |Specify the interval between health checks.<br><br><br>* Value range: 1–300<br><br>* Unit: seconds |2 |
|ingress.vke.volcengine.com/loadbalancer\-healthy\-threshold |String |No |The number of consecutive health check requests required to determine that the backend server is running properly.<br><br><br>* Value range: 2–10<br><br>* Unit: times |3 |
|ingress.vke.volcengine.com/loadbalancer\-unhealthy\-threshold |String |No |The number of consecutive health check requests required to determine that the backend server is not running properly.<br><br><br>* Value range: 2–10<br><br>* Unit: times |3 |
