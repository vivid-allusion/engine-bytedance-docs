---
title: "Creating Nginx Ingresses through kubectl"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-an-Nginx-Ingress-using-kubectl"
---

Vital Kubernetes Engine (VKE) provides an Nginx Ingress controller built on the community edition. It can convert Ingress rules to Nginx configurations and perform 7\-layer traffic forwarding through Nginx. This topic introduces how to configure Nginx Ingress using YAML.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Installed ingress\-nginx add\-on. For details, see [Installing ingress-nginx](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.aW5ncmVzcy1uZ2lueC3nu4Tku7Y=).

* The cluster has been connected. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id=".5Yib5bu6LW5naW54LWluZ3Jlc3M="></span>
## Creating Nginx Ingresses

<span id=".5Z-65LqO5Z-f5ZCN6L2s5Y-R"></span>
### Forwarding based on domain names

An NGINX Ingress can forward requests targeting different domain names to different back\-end services.


1. Create a YAML file for an Ingress. The following is an example named `nginx-ingress.yaml`.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: nginx-ingress # The name of the Ingress.
     namespace: default  # Namespace of the Ingress
   spec:
     ingressClassName: nginx # Specify the Ingress Controller.
     rules:
       - host: first.example.com  # The domain name for external access.
         http:
           paths:
           - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
             path: / # The matching path for the request.
             backend:
               service:
                 name: service-demo-a # The name of the service to forward requests to.
                 port: 
                   number: 80 # The service port number to forward to.
       - host: second.example.com  # Domain names for external access
         http:
           paths:
           - pathType: Prefix # The path matching rule. Valid values: Exact and Prefix.
             path: / # The matching path for the request.
             backend:
               service:
                 name: service-demo-b # The name of the service to forward requests to.
                 port: 
                   number: 80 # The service port number to forward to.
   ```
   

2. Execute the following command to create an Ingress.

   ```Bash
   kubectl apply -f nginx-ingress.yaml
   ```
   


<span id=".5Z-65LqO6Lev5b6E6L2s5Y-R"></span>
### Forwarding based on paths

An NGINX Ingress supports forwarding requests targeting different paths on the same domain name to different back\-end services.


1. Create a YAML file for Ingress. The following is an example named `nginx-ingress.yaml`.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: nginx-ingress # The name of the Ingress.
     namespace: default  # Namespace of the Ingress
   spec:
     ingressClassName: nginx # Specify the Ingress Controller.
     rules:
       - host: example.com  # The domain name for external access.
         http:
           paths:
           - path: /foo # The path that matches the request.
             pathType: Prefix # The path matching rule. Default value: Prefix.
             backend:
               service:
                 name: service-demo-a # The name of the service to forward requests to.
                 port: 
                   number: 80 # The service port number to forward to.
           - path: /bar # The path that matches the request.
             pathType: Prefix # The path matching rule. Default value: Prefix.
             backend:
               service:
                 name: service-demo-b # The name of the service to forward requests to.
                 port: 
                   number: 80 # The service port number to forward to.
   ```
   

2. Execute the following command to create an Ingress.

   ```Bash
   kubectl apply -f nginx-ingress.yaml
   ```
   


<span id=".5L2_55So6Ieq5a6a5LmJLW5naW54LWluZ3Jlc3MtY29udHJvbGxlcg=="></span>
### Using custom Nginx Ingress controllers

VKE supports deploying multiple independent Nginx Ingress Controller services in a cluster at the same time. For details, see [Deploying multiple NGINX Ingress controllers](https://docs.byteplus.com/en/docs/vke/Deploying-multiple-Nginx-Ingress-controllers).

You can use these NGINX Ingress controllers to provide different services externally as required. Procedure:


1. Create a YAML file for Ingress. The following is an example named `nginx-ingress.yaml`. Specifically, use the name in the `spec.ingressClassName` field to specify the Nginx Ingress controller service. In the following example, the controller `user-ingress-nginx` is specified.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: ingress-demo # The name of the Ingress.
     namespace: default # The namespace where the Ingress is located.
   spec:
     ingressClassName: user-ingress-nginx # The name of the custom NGINX Ingress controller.
     rules:
     - host: example.com # The domain name for external access.
       http:
         paths:
         - pathType: Prefix
           path: /
           backend:
             service:
               name: service-demo # The name of the service that the Ingress connects to.
               port:
                 number: 80 # The port number for the Ingress to connect to the service.
   ```
   

2. Execute the following command to create an application and a service.

   ```Bash
   kubectl apply -f nginx-ingress.yaml
   ```
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

<span id=".5p-l55yL6YWN572u"></span>
### Viewing configuration


1. Run the following command to view the Ingress configuration.

   ```Bash
   kubectl get ingress
   ```
   

   If the response is similar to the following one, the Ingress has been created. The address `180.xxx.xxx.xxx` is the public or private IP of the CLB configured for the Nginx Ingress.

   ```Bash
   NAME            CLASS   HOSTS          ADDRESS          PORTS   AGE
   nginx-ingress   nginx   example.com    180.xxx.xxx.xxx   80     74s
   ```
   


<span id=".6K6_6Zeu5pyN5Yqh"></span>
### Testing the connections to services

Run the following command to access the service by using the domain name.

```bash
curl -H "Host: example.com" http://180.xxx.xxx.xxx
```


If the response is similar to the following one, the back\-end service is accessible through the domain name.

```html
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
