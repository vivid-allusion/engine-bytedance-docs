---
title: "Using APIG Ingresses to implement gray releases and blue-green deployments"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Implement_canary_release_and_blue-green_deployment_using_APIG_Ingress"
---

APIG Ingresses enable you to use annotations to implement gray releases and blue\-green deployments. This topic introduces how to use APIG Ingresses to implement gray releases and blue\-green deployments.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

<span id=".5LuA5LmI5piv54Gw5bqm5Y-R5biD"></span>
### What is gray release

Gray release, also known as Canary release, is a software release strategy that allows developers to gradually deploy new versions of software to the production environment, rather than releasing them all at once. This approach first releases software within several limited scopes and finally expands to all users if the software goes well in each scope, so as to reduce the risks in software releases.

The main characteristics of gray releases include:


* **Gradual release**: Instead of releasing the new version to all users at once, the rollout is expanded step by step according to a plan. For example, first making it available to 1% of users, observing for a period of time, then expanding to 10%, and finally releasing to all users.

* **Risk control**: By limiting the user scope of a new software version, it is possible to quickly roll back in case of issues and avoid a large\-scale impact.

* **Real\-time monitoring**: During a gray release, you need to closely monitor software health, including performance metrics and user feedback, in order to ensure the stability of the new versions.

* **Flexible rollback**: If the new version encounters serious problems, you can quickly roll back to the previous version to minimize the impact on users.


Gray release is very important for ensuring good software quality and user experience, especially in large\-scale and complex systems. It enables teams to manage the software release process with greater flexibility and security, reducing potential risks.

<span id=".YXBpZy1pbmdyZXNzLeWPkeW4g-a1geeoiw=="></span>
### Release process with APIG Ingresses

By using annotations, APIG Ingresses enable you to release services in different scenarios, including canary releases, blue\-green deployments, and A/B testing. The release process is as follows:


1. Create two applications and two services in the cluster.

2. Create two Ingresses for the services: One is a standard APIG Ingress, and the other is an Ingress with the `nginx.ingress.kubernetes.io/canary: "true"` annotation, which is referred to as the Canary APIG Ingress. Then, bind these Ingresses to the same APIG Instance.

3. Use annotations to configure the traffic splitting policy for the Canary APIG Ingress according to the specific scenario.


<span id=".YXBpZy1pbmdyZXNzLeazqOino-ivtOaYjg=="></span>
### Annotations of APIG Ingresses

The following annotations are available for gray releases with APIG Ingresses:


* `nginx.ingress.kubernetes.io/canary-by-header`: Header\-based traffic splitting policy, applicable to gray releases. Requests with the specific header will be forwarded to the backend services through Canary APIG Ingresses.

* `nginx.ingress.kubernetes.io/canary-by-header-value`: Used together with `canary-by-header` to specify the value of the header. Requests with the specific header value will be forwarded to the backend services through Canary APIG Ingresses.

* `nginx.ingress.kubernetes.io/canary-weight`: A traffic splitting policy based on service weight, applicable to blue\-green deployments. This annotation specifies the traffic percentage forwarded by Canary APIG Ingresses, with a range from 0 to 100. 100 percent means all traffic will be forwarded to the backend services through Canary APIG Ingresses.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The priorities of the above annotations are: <code>canary-by-header</code> \> <code>canary-weight</code>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Application images have been uploaded to the Container Registry (CR). For details, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

* The apig\-controller add\-on has been installed. For details, see [Add-on installation](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A KubeConfig for private networks has been generated in the cluster. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* An APIGInstance has been created and bound to a newly created or existing APIG instance. For details, see [Creating APIGInstance](https://docs.byteplus.com/en/docs/vke/Create_an_APIG_Ingress_using_kubectl#.5Yib5bu6LWFwaWdpbnN0YW5jZQ==).


<span id=".5Zyo6ZuG576k5Lit6YOo572y5pyN5Yqh"></span>
## Deploying services in clusters


1. Use the following YAML configuration to create legacy applications and services.


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
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v2.0
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


&nbsp;

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
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v2.0
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



2. Use the following YAML configuration to create new versions of applications and services.


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
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v3.0
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



3. Use the following YAML configuration to create an APIG Ingress and point it to the old version service.


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-old # Ingress name
  annotations: 
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # Specify resource name for the APIGInstance 
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain name that needs to be accessible externally
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting
          path: / # The matching path for the request
          backend:
            service:
              name: service-old # Service name to forward to
              port: 
                number: 80 # Service port number to forward to
```



4. Execute the following command to verify whether the legacy service is accessible. `<EXTERNAL_IP>` is the IP address exposed externally by APIG Ingress.


```bash
curl -H "Host: example.com" http://<EXTERNAL_IP>
```


The following response indicates the old version application has been reached successfully.

```bash
This is the old version of nginx
```


<span id=".6YWN572u54Gw5bqm5Y-R5biD"></span>
## Configuring gray releases

APIG Ingresses can implement gray releases with policies based on headers, cookies, or server weights.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">At most two versions of the same backend service are supported, because only one Canary APIG Ingress can be defined for the same service.</div>


* <div data-tips="true" data-tips-type="warning">The old version services need to be retained, even if all traffic is forwarded by Canary APIG Ingress. Otherwise, errors will occur.</div>



<span id=".5Z-65LqOLWhlYWRlci3lrp7njrDngbDluqblj5HluIM="></span>
### Gray releases based on headers


1. Use the following YAML configuration to bind Canary APIG Ingress to the new version of the services. The annotations shown below are used to enable and configure Canary, so as to filter and forward traffic based on headers. In this example, requests with the header name `Region` and value set to `beijing` will be forwarded to the new version services.


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-new # Ingress name
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # Specify resource name for the APIGInstance 
    nginx.ingress.kubernetes.io/canary: "true" # Enable Canary
    nginx.ingress.kubernetes.io/canary-by-header: "Region" # Configure header-based traffic splitting policy
    nginx.ingress.kubernetes.io/canary-by-header-value: "beijing" # Requests with the header named Region and the value set to beijing will be forwarded
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain name that needs to be accessible externally
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting
          path: / # The matching path for the request
          backend:
            service:
              name: service-new # Service name to forward to
              port: 
                number: 80 # Service port number to forward to
```



2. Execute the following commands to test. The expected results are as follows.

   * When `Region` does not exist, traffic is forwarded to the legacy service.

   ```bash
   curl -H "Host: example.com" http://<EXTERNAL_IP>
   This is the old version of nginx
   ```
   

   * When `Region` exists, and its value is not `beijing`, traffic is forwarded to the new version of the services.

   ```bash
   curl -H "Host: example.com" -H "Region: shanghai" http://<EXTERNAL_IP>
   This is the old version of nginx
   ```
   

   * When `Region` exists and its value is `beijing`, traffic is forwarded to the new version of the services.

   ```bash
   curl -H "Host: example.com" -H "Region: beijing" http://<EXTERNAL_IP>
   This is the new version of nginx
   ```
   


<span id=".5Z-65LqO5pyN5Yqh5p2D6YeN5a6e546w54Gw5bqm5Y-R5biD"></span>
### Gray releases based on service weights


1. Use the following YAML configuration to bind Canary APIG Ingress to the new version of the services. The annotations shown below are used to enable and configure Canary to filter and forward traffic based on service weights. In this example, 25% of requests are forwarded to the new version of the services.


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-new # Ingress name
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # Specify resource name for the APIGInstance 
    nginx.ingress.kubernetes.io/canary: "true" # Enable Canary
    nginx.ingress.kubernetes.io/canary-weight: "25" # Configure a traffic splitting policy based on service weights. A weight of 25 means that 25% of the traffic is forwarded to the new version of the services.
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain name that needs to be accessible externally
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting
          path: / # The matching path for the request
          backend:
            service:
              name: service-new # Service name to forward to
              port: 
                number: 80 # Service port number to forward to
```



2. Execute the following command to test with 20 requests.


```bash
for i in {1..20}; do curl -H "Host: example.com" http://<EXTERNAL_IP>; done;
```


The following responses indicate that 25% of the traffic has been forwarded to the new version of the services as expected.

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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is normal to have slight deviations in results due to the small sample size (20 requests). You can perform more tests or increase the sample size.</div>


<span id=".6YWN572u6JOd57u_5Y-R5biD"></span>
## Configuring blue\-green deployments


1. Traffic can be split based on service weights. When the weight of the new service is set to 100, blue\-green deployment can be achieved.


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-new # Ingress name
  annotations:
    ingress.vke.volcengine.com/apig-instance-name: apig-instance-demo # Specify resource name for the APIGInstance 
    nginx.ingress.kubernetes.io/canary: "true" # Enable Canary
    nginx.ingress.kubernetes.io/canary-weight: "100" # Configure the weight of the new Service to 100%, indicating a blue-green deployment
spec:
  ingressClassName: apig
  rules:
    - host: example.com  # Domain name that needs to be accessible externally
      http:
        paths:
        - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting
          path: / # The matching path for the request
          backend:
            service:
              name: service-new # Service name to forward to
              port: 
                number: 80 # Service port number to forward to
```



2. Execute the following command to test with 20 requests.


```bash
for i in {1..20}; do curl -H "Host: example.com" http://<EXTERNAL_IP>; done;
```


The expected result is as follows. All traffic has been forwarded to the new version services, while the old version is retained. You can shift traffic and roll back if necessary.

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
