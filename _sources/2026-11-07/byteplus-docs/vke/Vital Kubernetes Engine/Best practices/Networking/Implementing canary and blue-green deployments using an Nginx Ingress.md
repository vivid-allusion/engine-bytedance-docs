---
title: "Implementing canary and blue-green deployments using an Nginx Ingress"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Implementing-canary-and-blue-green-deployments-using-an-Nginx-Ingress"
---

You can add annotations to an Nginx Ingress to enable blue\-green deployment and canary deployment. This topic describes how to implement blue\-green and canary deployment using an Nginx Ingress.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

<span id=".5LuA5LmI5piv54Gw5bqm5Y-R5biD"></span>
### What is canary deployment?

Canary deployment, also known as canary release, is a software release strategy that enables developers to gradually roll out new software versions to production environments instead of releasing to all clients at a time. The purpose is to mitigate risks associated with software releases by initially releasing the software to a small scope of clients for observing the performance of the software. After the stability of the software is proven, release the software to all clients.

The benefits of canary deployment include:


* **Phased release**: Rather than releasing a new version to all users simultaneously, the release scope is gradually expanded as per a plan. For example, you can initially release a new version to 1% of the users, monitor the performance for a specific period of time, then expand to 10%, and finally release it to all other users.

* **Risk control**: By restricting the user scope of the new software version, you can swiftly roll back the software if issues occur. This method prevents widespread impacts.

* **Real\-time monitoring**: Throughout a canary deployment, you can monitor the status of the software in real time, including the performance metrics, user feedback, and other information. This helps you determine whether the performance of the new version is stable.

* **Flexible rollback**: If significant issues arise with the new version, you can rapidly roll back the software to the previous version, minimizing impacts.


Canary deployment is vital for ensuring software quality and user experience, particularly in large\-scale and complex systems. It enables developer teams to manage software release processes more flexibly and securely while mitigating potential risks.

<span id=".bmdpbngtaW5ncmVzcy3lj5HluIPmtYHnqIs="></span>
### Nginx Ingress\-based software release process

You can add annotations to an Nginx Ingress to implement application releases in different scenarios, including canary deployment, blue\-green deployment, and A/B testing. The release process is as follows:


1. Create two applications and Services in the target cluster.

2. Create two Ingresses for the Services: a regular Nginx Ingress and a Canary Nginx Ingress to which the `nginx.ingress.kubernetes.io/canary: "true"` annotation is added.

3. Use annotations to configure a traffic splitting strategy for the Canary Nginx Ingress to enable canary deployment.


<span id=".bmdpbngtaW5ncmVzcy3ms6jop6Por7TmmI4="></span>
### Nginx Ingress annotations

You can add the following annotations to an Nginx Ingress to enable canary deployment:


* `nginx.ingress.kubernetes.io/canary-by-header`: This annotation specifies a header\-based traffic splitting strategy for canary deployment. If the specified header is included a request and the value is "always", the request is forwarded to the back\-end Service specified in the Canary Nginx Ingress.

* `nginx.ingress.kubernetes.io/canary-by-header-value`: This annotation specifies a header value. The valid values include but are not limited to `"always"` and `"never"`. This annotation must be used together with the `canary-by-header` annotation. When the header value in a request matches the value that you specified with this annotation, the request is forwarded to the back\-end Service specified in the Canary Nginx Ingress.

* `nginx.ingress.kubernetes.io/canary-by-header-pattern`: The usage method of this annotation is similar to that of the `canary-by-header-value` annotation. The difference is that this annotation uses regular expressions to specify header values instead of a fixed value.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If this annotation coexists with <code>canary-by-header-value</code>, this <code>annotation</code> is ignored.   </div>
   

* `nginx.ingress.kubernetes.io/canary-by-cookie`: This annotation specifies a cookie\-based traffic splitting strategy for canary deployment. If the specified Cookie header is included in a request and the value is `"always"` or `"never"`, the request is forwarded to the back\-end Service specified in the Canary Nginx Ingress. The cookie traffic splitting strategy does not support custom values.

* `nginx.ingress.kubernetes.io/canary-weight`: This annotation specifies a weight\-based traffic splitting strategy for blue\-green deployment. It specifies the percentage of requests that the Canary Nginx Ingress distributes. The valid value range is from 0 to 100. If you set the value to 100, all requests are forwarded to the back\-end Service specified in the Canary Nginx Ingress.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>



* <div data-tips="true" data-tips-type="tip">The priorities of the above annotations are as follows: <code>canary-by-header</code> \> <code>canary-by-cookie</code> \> <code>canary-weight</code>.</div>


* <div data-tips="true" data-tips-type="tip">For a Canary Nginx Ingress, <code>non-canary</code> annotations other than <code>nginx.ingress.kubernetes.io/load-balance</code> and <code>nginx.ingress.kubernetes.io/upstream-hash-by</code> are ignored.</div>


* <div data-tips="true" data-tips-type="tip">For more information on annotations, refer to the <a href="https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/">Annotations</a>.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Create a cluster. For more information, refer to [Creating a cluster](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* Upload your application image to your image registry. For more information, refer to [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).


<span id=".5Zyo6ZuG576k5Lit6YOo572y5pyN5Yqh"></span>
## Deploying your Services in the target cluster


1. Use the following YAML configurations to create an application and a Service as the old versions to be updated:


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-old
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx-old
  template:
    metadata:
      labels:
        app: nginx-old
    spec:
      containers:
      - name: nginx
        image: doc-ap-southeast-1.cr.bytepluses.com/vke/nginx-demo:v2.0
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: service-old
spec:
  selector:
    app: nginx-old
  ports:
  - name: rule
    protocol: TCP
    port: 80
    targetPort: 80
  type: NodePort
```



2. Use the following YAML configurations to create an application and a Service as the new versions:


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-new
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx-new
  template:
    metadata:
      labels:
        app: nginx-new
    spec:
      containers:
      - name: nginx
        image: doc-ap-southeast-1.cr.bytepluses.com/vke/nginx-demo:v3.0
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: service-new
spec:
  selector:
    app: nginx-new
  ports:
  - name: rule
    protocol: TCP
    port: 80
    targetPort: 80
  type: NodePort
```



3. Use the following YAML configurations to create an Nginx Ingress and point it to the old version of the Service:


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-old # The Ingress name.
spec:
  ingressClassName: nginx # The Ingress Controller.
  rules:
    - host: example.com  # The domain name that is used to expose the Service for external access.
      http:
        paths:
        - pathType: Prefix # The path matching rule. The default value is Prefix.
          path: / # The path.
          backend:
            service:
              name: service-old # The name of the Service with which you want to associate this Ingress.
              port: 
                number: 80 # The port on which the associated Service is exposed.
```



4. Run the following command to verify whether the old version of the Service can be accessed: Wherein, `<EXTERNAL_IP>` specifies the IP address of the Nginx Ingress exposed for external access.


```bash
curl -H "Host: example.com" http://<EXTERNAL_IP>
```


The expected result is as follows, indicating that the old version of the application is successfully accessed:

```bash
This is the old version of nginx
```


<span id=".6YWN572u54Gw5bqm5Y-R5biD"></span>
## Configuring canary deployment

In an Nginx Ingress, you can configure a header\-based, Cookie\-based, or weight\-based traffic splitting strategy for implementing canary deployment.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">注意</div>



* <div data-tips="true" data-tips-type="warning">You can configure only one Canary Nginx Ingress for a Service. Therefore, the back\-end Service can have up to two versions.</div>


* <div data-tips="true" data-tips-type="warning">After the traffic is completely switched to the Canary Nginx Ingress, the old version of the Service must be retained; otherwise, errors occur.</div>



<span id=".5Z-65LqOLWhlYWRlci3lrp7njrDngbDluqblj5HluIM="></span>
### Implementing header\-based canary deployment


1. Use the following YAML configurations to create a Canary Nginx Ingress to point to the new version of the Service: Use annotations to enable and configure canary deployment and implement traffic filtering and forwarding based on the specified header. In this example, if the `Region` header is included in a request and the value is `beijing`, the request is forwarded to the new version of the Service.


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-new # The Ingress name.
  annotations:
    nginx.ingress.kubernetes.io/canary: "true" # Enable canary.
    nginx.ingress.kubernetes.io/canary-by-header: "Region" # Specify a header-based traffic splitting strategy.
    nginx.ingress.kubernetes.io/canary-by-header-pattern: "beijing" # Specify that the requests in which the value of the Region header is beijing are forwarded to the specified Service.
spec:
  ingressClassName: nginx # The Ingress Controller.
  rules:
    - host: example.com  # The domain name that is used to expose the Service for external access.
      http:
        paths:
        - pathType: Prefix # The path matching rule. The default value is Prefix.
          path: / # The path.
          backend:
            service:
              name: service-new # The name of the Service with which you want to associate this Ingress.
              port: 
                number: 80 # The port on which the associated Service is exposed.
```



2. Run the following command to test. The expected result is as follows.

   * Forward the requests without the `Region` parameter to the old version of the Service.

   ```bash
   curl -H "Host: example.com" http://<EXTERNAL_IP>
   This is the old version of nginx
   ```
   

   * Forward the requests in which the value of the `Region` header is not `beijing` to the old version of the Service.

   ```bash
   curl -H "Host: example.com" -H "Region: shanghai" http://<EXTERNAL_IP>
   This is the old version of nginx
   ```
   

   * Forward the requests in which the value of the `Region` header is `beijing` to the new version of the Service.

   ```bash
   curl -H "Host: example.com" -H "Region: beijing" http://<EXTERNAL_IP>
   This is the new version of nginx
   ```
   


<span id=".5Z-65LqOLWNvb2tpZS3lrp7njrDngbDluqblj5HluIM="></span>
### Implementing Cookie\-based canary deployment


1. Use the following YAML configurations to create a Canary Nginx Ingress to point to the new version of the Service: Use annotations to enable and configure canary deployment and implement traffic filtering and forwarding based on the specified Cookie. In this example, if `Cookie` is included in a request and the value is `beijing`, the request is forwarded to the new version of the Service.


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-new # The Ingress name.
  annotations:
    nginx.ingress.kubernetes.io/canary: "true" # Enable canary.
    nginx.ingress.kubernetes.io/canary-by-cookie: "beijing" # Specify a Cookie-based traffic splitting strategy.
spec:
  ingressClassName: nginx # The Ingress Controller.
  rules:
    - host: example.com  # The domain name that is used to expose the Service for external access.
      http:
        paths:
        - pathType: Prefix # The path matching rule. The default value is Prefix.
          path: / # The path.
          backend:
            service:
              name: service-new # The name of the Service with which you want to associate this Ingress.
              port: 
                number: 80 # The port on which the associated Service is exposed.
```



2. Run the following command to test. The expected result is as follows.

   * Forward the requests without the `Cookie` parameter to the old version of the Service.

   ```bash
   curl -H "Host: example.com" http://<EXTERNAL_IP>
   This is the old version of nginx
   ```
   

   * Forward the requests in which the value of `Cookie` is not `beijing` to the old version of the Service.

   ```bash
   curl -s -H "Host: example.com" --cookie "shanghai=always" http://<EXTERNAL_IP>
   This is the old version of nginx
   ```
   

   * Forward the requests in which the value of `Cookie` is `beijing` to the new version of the Service.

   ```bash
   curl -s -H "Host: example.com" --cookie "beijing=always" http://<EXTERNAL_IP>
   This is the new version of nginx
   ```
   


<span id=".5Z-65LqO5pyN5Yqh5p2D6YeN5a6e546w54Gw5bqm5Y-R5biD"></span>
### Implementing weight\-based canary deployment


1. Use the following YAML configurations to create a Canary Nginx Ingress to point to the new version of the Service: Use annotations to enable and configure canary deployment and implement traffic filtering and forwarding based on the specified weight. The following sample code is used to forward 25% of the access requests to the new version of the Service.


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-new # The Ingress name.
  annotations:
    nginx.ingress.kubernetes.io/canary: "true" # Enable canary.
    nginx.ingress.kubernetes.io/canary-weight: "25" # Specify a weight-based traffic splitting strategy. The weight is set to 25, indicating that 25% of the access requests will be forwarded to the new version of the Service.
spec:
  ingressClassName: nginx # The Ingress Controller.
  rules:
    - host: example.com  # The domain name that is used to expose the Service for external access.
      http:
        paths:
        - pathType: Prefix # The path matching rule. The default value is Prefix.
          path: / # The path.
          backend:
            service:
              name: service-new # The name of the Service with which you want to associate this Ingress.
              port: 
                number: 80 # The port on which the associated Service is exposed.
```



2. Run the following command to execute 20 access tests:


```bash
for i in {1..20}; do curl -H "Host: example.com" http://<EXTERNAL_IP>; done;
```


The expected result is as follows, indicating that 25% of the requests are forwarded to the new version of the Service:

```bash
This is the old version of nginx
This is the new version of nginx
This is the old version of nginx
This is the new version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the new version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the new version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the new version of nginx
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">Because a small number of samples (20) are used, data deviation may occur, which is normal. Verify multiple times or increase the sample size.</div>


<span id=".6YWN572u6JOd57u_5Y-R5biD"></span>
## Configuring blue\-green deployment


1. To implement blue\-green deployment, set the weight of the new Service version to 100% in a weight\-based traffic splitting strategy.


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-new # The Ingress name.
  annotations:
    nginx.ingress.kubernetes.io/canary: "true" # Enable canary.
    nginx.ingress.kubernetes.io/canary-weight: "100" # Set the weight of the new version of the Service to 100% to implement blue-green deployment.
spec:
  ingressClassName: nginx # The Ingress Controller.
  rules:
    - host: example.com  # The domain name that is used to expose the Service for external access.
      http:
        paths:
        - pathType: Prefix # The path matching rule. The default value is Prefix.
          path: / # The path.
          backend:
            service:
              name: service-new # The name of the Service with which you want to associate this Ingress.
              port: 
                number: 80 # The port on which the associated Service is exposed.
```



2. Run the following command to execute 20 access tests:


```bash
for i in {1..20}; do curl -H "Host: example.com" http://<EXTERNAL_IP>; done;
```


The expected result is as follows. All requests are forwarded to the new version of the Service while the old version is retained, enabling traffic switching and rollback as needed.

```bash
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
This is the new version of nginx
```
