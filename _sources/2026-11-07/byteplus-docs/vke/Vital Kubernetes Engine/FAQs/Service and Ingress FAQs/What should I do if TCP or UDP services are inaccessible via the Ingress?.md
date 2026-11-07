---
title: "What should I do if TCP or UDP services are inaccessible via the Ingress?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-can-I-do-if-I-cannot-access-a-TCP-or-UDP-Service-through-an-Ingress"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Issue description

TCP and UDP services are inaccessible through Ingresses.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution

Add TCP and UDP service access settings by following the steps below. For more information, see [Expose TCP and UDP services](https://kubernetes.github.io/ingress-nginx/user-guide/exposing-tcp-udp-services/).


1. In the corresponding ConfigMap (by default, tcp\-services and udp\-services in the kube\-system namespace), add the entries as needed.

   For example, map port 8080 of example\-go in the default namespace to port 9000. The example is as follows:

   ```YAML
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: tcp-services
     namespace: ingress-nginx
   data:
     9000: "default/example-go:8080"# Map port 8080 to port 9000.
   ```
   

2. In the Ingress Deployment (by default, nginx\-ingress\-controller in the kube\-system namespace), add the mapped port.

3. In the Service corresponding to the Ingress, add the mapped port. The example is as follows:

   ```Yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: ingress-nginx
     namespace: ingress-nginx
     labels:
       app.kubernetes.io/name: ingress-nginx
       app.kubernetes.io/part-of: ingress-nginx
   spec:
     type: LoadBalancer
     ports:
       - name: http
         port: 80
         targetPort: 80
         protocol: TCP
       - name: https
         port: 443
         targetPort: 443
         protocol: TCP
       - name: proxied-tcp-9000
         port: 9000
         targetPort: 9000
         protocol: TCP
     selector:
       app.kubernetes.io/name: ingress-nginx
       app.kubernetes.io/part-of: ingress-nginx
   ```
