---
title: "Configuring consistent hashing for load balancing with NGINX Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-consistent-hashing-for-an-Nginx-Ingress-for-load-balancing"
---

Nginx Ingresses support consistent hashing, which can effectively resolve load balancing instability caused by dynamically adding or removing backend servers. This topic describes how to configure consistent hashing for NGINX Ingresses.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


<span id=".6IOM5pmv6K-05piO"></span>
## Background information

The source IP Hash method supported by NGINX Ingresses by default uses a linear hash space. The system selects the target backend server based on the hash value computed from the source IP address. This ensures that the same source IP is always routed to the same backend server.

However, this approach has an issue: ‌when backend servers are added or removed, all source IPs must undergo re\-hashing‌ to adapt and reroute to the changed number of backend servers. This results in ‌massive session disruption or cache invalidation‌.

To address the above issue, NGINX Ingresses introduce a consistent hashing algorithm. This algorithm replaces the conventional linear hash space with a ring\-based hash space. When backend servers are added or removed, only a small portion of data (specifically, the segment adjacent to the added or removed server) requires rerouting. This approach effectively resolves load balancing disruption caused by dynamic scaling of backend servers.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cluster has been connected. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* Installed ingress\-nginx add\-on. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

Nginx Ingresses support consistent hashing for load balancing using annotations. The following file provides an example of NGINX Ingress configuration:

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress # Ingress name
  annotations:
    nginx.ingress.kubernetes.io/upstream-hash-by: "$request_uri"
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
        pathType: ImplementationSpecific
```


The following table describes the annotations.


|Key |Type |Required |Description |default value |
|---|---|---|---|---|
|nginx.ingress.kubernetes.io/upstream\-hash\-by |String |Yes |The consistent hashing rule. It supports NGINX parameters, text values, or any combination of the two. Examples:<br><br><br>*  **$request_uri**: indicates hashing based on the request URI.<br><br>*  **$request_uri$host**: Indicates hashing based on the request URI and domain name.<br><br>*  **${request_uri}\-text\-value**: indicates hashing based on the request URL and the text value. |No |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details, see <a href="https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#custom-nginx-upstream-hashing">Ingress\-Nginx Controller documentation</a>.</div>
