---
title: "Configuring URL rewrite rules in Nginx Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-URL-rewrite-rules-for-an-Nginx-Ingress"
---

Nginx Ingress can rewrite request URLs. This topic introduces how to configure the URL rewrite feature of Nginx Ingress.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


<span id=".6IOM5pmv6K-05piO"></span>
## Background information

In certain application scenarios, the path in a back\-end service URL can differ from the one configured in the corresponding NGINX Ingress. By default, Nginx Ingress forwards traffic to backend services running at the same URL as the requests. If you do not create URL rewrite rules, your requests to those applications will receive `404` responses. Therefore, you need to rewrite URLs by configuring rules to ensure requests can reach the expected destinations.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cluster has been connected. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* Installed ingress\-nginx add\-on. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

An NGINX Ingress supports configuring URL rewriting based on annotations. The following YAML file provides an example.

```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress # Ingress name
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: "/$2"
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
        path: /demo(/|$)(.*) # The access path.
        pathType: ImplementationSpecific
```


The following table describes the annotations.


|Key |Type |Required |Description |Default value |
|---|---|---|---|---|
|nginx.ingress.kubernetes.io/rewrite\-target |String |Yes |The target URI for URL rewriting. It uses regular expressions to define capture groups. |No |


In the `nginx.ingress.kubernetes.io/rewrite-target` annotation, you can use regular expressions to define capture groups. For example, in the sample file above, `$2` means that all characters matched in the second pair of parentheses `(.*)` in the path field are inserted as the value of the `nginx.ingress.kubernetes.io/rewrite-target` annotation. For example:


* Request to `example.com/demo` will be rewritten to `example.com/`

* Requests to `example.com/demo/` will be rewritten to `example.com/`

* Requests to `example.com/demo/test` will be rewritten as `example.com/test`


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

<span id=".5p-l55yL6YWN572u"></span>
### Viewing configuration

Run the following command to view the Ingress configuration.

```Bash
kubectl get ingress
```


If the response is similar to the following one, the Ingress has been created. The address `180.xxx.xxx.xxx` is the public or private IP of the CLB configured for the Nginx Ingress.

```Bash
NAME            CLASS   HOSTS           ADDRESS           PORTS   AGE
nginx-ingress   nginx   example.com     180.xxx.xxx.xxx   80      74s
```


<span id=".6K6_6Zeu5pyN5Yqh"></span>
### Testing the connections to services

The default path of the back\-end service is `/`, while the path configured in the Ingress is `/demo`. If URL rewrite rules are not configured, a `404` response is returned because the request path does not exist.

```Bash
curl -H "Host: example.com" http://180.xxx.xxx.xxx/demo
```


The expected response is as follows:

```HTML
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx</center>
</body>
</html>
```


With this URL rewriting configured, use the following command to access the service.

```Bash
curl -H "Host: example.com" https://180.xxx.xxx.xxx/demo
```


If the following response is returned, the back\-end service is accessible.

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
