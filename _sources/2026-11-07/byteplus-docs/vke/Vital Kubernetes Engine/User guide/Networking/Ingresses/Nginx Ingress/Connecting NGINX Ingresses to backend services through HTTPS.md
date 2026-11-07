---
title: "Connecting NGINX Ingresses to backend services through HTTPS"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-HTTPS-to-connect-an-Nginx-Ingress-to-back-end-services"
---

In most cases, HTTP is used to connect NGINX Ingresses to backend services. To ensure the security of backend communication, you can configure annotations to connect to backend servers by using HTTPS. This topic describes how to connect NGINX Ingresses to backend servers by using HTTPS.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Installed ingress\-nginx add\-on in the cluster. For details, see [Ingress-nginx add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.aW5ncmVzcy1uZ2lueC3nu4Tku7Y=).

* You have already purchased a Secure Sockets Layer (SSL) certificate and key.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5L-d5a-G5a2X5YW4"></span>
### Step 1: Configure a secret


1. The SSL certificate and key have been obtained. This topic takes `tls.key` and `tls.crt` as an example.

2. Run the following command to create a secret named ingress\-secret of type `kubernetes.io/tls`.

   ```Bash
   kubectl create secret tls ingress-secret --key tls.key --cert tls.crt
   ```
   


<span id=".5q2l6aqk5LqM77ya6YWN572u6Lev55Sx6KeE5YiZ"></span>
### Step 2: Configure an Ingress


1. Create a YAML file for an Ingress. The code of the sample file`nginx-ingress.yaml` is as follows:

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: nginx-ingress # Ingress name
     annotations:
       nginx.ingress.kubernetes.io/backend-protocol: "HTTPS" # Connect to the back-end server over HTTPS.
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
     tls:
       - secretName: ingress-secret # The name of the Secret used by the Ingress.
   ```
   

2. Run the following command to create the Ingress.

   ```Bash
   kubectl apply -f nginx-ingress.yaml
   ```
