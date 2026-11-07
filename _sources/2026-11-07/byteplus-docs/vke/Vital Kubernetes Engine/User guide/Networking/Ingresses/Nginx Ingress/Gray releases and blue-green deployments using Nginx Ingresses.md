---
title: "Gray releases and blue-green deployments using Nginx Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Implement_canary_release_and_blue-green_deployment_using_Nginx_Ingress"
---

Nginx Ingresses enable you to use annotations to implement gray releases and blue\-green deployments. This topic introduces how to do so.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

<span id=".5LuA5LmI5piv54Gw5bqm5Y-R5biD"></span>
### What is gray release

Gray release, also known as Canary release, is a software release strategy that allows developers to gradually deploy new versions of software to the production environment, rather than releasing them all at once. This approach first releases software within several limited scopes and finally expands to all users if the software goes well in each scope, so as to reduce the risks in software releases.

The main characteristics of gray releases include:


* **Gradual release**: Instead of releasing the new version to all users at once, the rollout is expanded step by step according to a plan. For example, first making it available to 1% of users, observing for a period of time, then expanding to 10%, and finally releasing to all users.

* **Risk control**: By limiting the user scope of a new software version, it is possible to quickly roll back in case of issues and avoid a large\-scale impact.

* **Real\-time monitoring**: During a gray release, closely monitor software health (including performance metrics and user feedback) to ensure new version stability.

* **Flexible rollback**: If the new version encounters serious problems, you can quickly roll back to the previous version to minimize the impact on users.


Gray release is very important for ensuring good software quality and user experience, especially in large\-scale and complex systems. It enables teams to manage the software release process with greater flexibility and security, reducing potential risks.

<span id=".bmdpbngtaW5ncmVzcy3lj5HluIPmtYHnqIs="></span>
### Release process with Nginx Ingresses

By using annotations, Nginx Ingress enables you to roll out services in different scenarios, including canary releases, blue\-green deployments, and A/B testing. The release process is as follows:


1. Create two applications and two services in the cluster.

2. Create two Ingresses for the services: one is a standard Nginx Ingress, the other is an Ingress with the `nginx.ingress.kubernetes.io/canary: "true"` annotation, referred to as the Canary Nginx Ingress.

3. Use annotations to configure the traffic splitting policy for the Canary Nginx Ingress according to the specific scenario.


<span id=".bmdpbngtaW5ncmVzcy3ms6jop6Por7TmmI4="></span>
### Annotations of Nginx Ingresses

The following annotations are available for gray releases with Nginx Ingresses:


* `nginx.ingress.kubernetes.io/canary-by-header`: Header\-based traffic splitting policy, applicable to gray releases. Requests with the specific header set to the value "always" will be forwarded to the backend services through Canary Nginx Ingresses.

* `nginx.ingress.kubernetes.io/canary-by-header-value`: Used together with `canary-by-header` to specify the value of the header. It can be set to, but not limited to, `"always"` or `"never"`. Requests with the specific header value will be forwarded to the backend services through Canary Nginx Ingresses.

* `nginx.ingress.kubernetes.io/canary-by-header-pattern`: It is similar to `canary-by-header-value`, but it uses a regular expression to match request header values, instead of using certain values.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This <code>annotation</code> will be ignored if it exists together with <code>canary-by-header-value</code>.   </div>
   

* `nginx.ingress.kubernetes.io/canary-by-cookie`: Cookie\-based traffic splitting policy, applicable to gray releases. Requests with the specified cookie keys set to the value `"always"` or `"never"` will be forwarded to the backend services through Canary Nginx Ingresses accordingly. Custom values are not supported in Cookie\-based traffic splitting policies.

* `nginx.ingress.kubernetes.io/canary-weight`: A traffic splitting policy based on service weight, applicable to blue\-green deployments. This annotation specifies the traffic percentage forwarded by Canary Nginx Ingresses, with a range from 0 to 100. 100 percent means all traffic will be forwarded to the backend services through Canary Nginx Ingresses.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The priorities of the above annotations are: <code>canary-by-header</code> \> <code>canary-by-cookie</code> \> <code>canary-weight</code>.</div>


* <div data-tips="true" data-tips-type="tip">A Canary Nginx Ingress will ignore all the annotations that do not contain <code>Canary</code>, except <code>nginx.ingress.kubernetes.io/load-balance</code> and <code>nginx.ingress.kubernetes.io/upstream-hash-by</code>.</div>


* <div data-tips="true" data-tips-type="tip">For more details about annotations, see <a href="https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/">Official documentation</a>.</div>



<span id=".5Zyo6ZuG576k5Lit6YOo572y5pyN5Yqh"></span>
## Deploying services in clusters


1. Use the following YAML configuration to create old version applications and services.

   ```YAML
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

   ```YAML
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
   

3. Use the following YAML configuration to create an Nginx Ingres and point it to the old version service.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: ingress-old # Ingress name
   spec:
     ingressClassName: nginx # Specify the Ingress Controller.
     rules:
       - host: example.com  # The domain name for external access.
         http:
           paths:
           - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
             path: / # The matching path for the request.
             backend:
               service:
                 name: service-old # The name of the service to forward requests to.
                 port: 
                   number: 80 # Service port number to forward to
   ```
   

4. Execute the following command to verify whether the old version of the service is accessible. In the command, `<EXTERNAL_IP>` is the IP address exposed externally by the NGINX Ingress.

   ```Bash
   curl -H "Host: example.com" http://<EXTERNAL_IP>
   ```
   

   The following result indicates that the old application version is accessible:

   ```Bash
   This is the old version of nginx
   ```
   


<span id=".6YWN572u54Gw5bqm5Y-R5biD"></span>
## Configuring gray releases

Nginx Ingresses can implement gray releases with policies based on headers, cookies, or server weights.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">At most two versions of identical backend services are allowed, and they need to share the same Canary Nginx Ingress.</div>


* <div data-tips="true" data-tips-type="warning">The old version services need to be retained, even if all traffic is forwarded by Canary Nginx Ingress. Otherwise, errors will occur.</div>



<span id=".5Z-65LqOLWhlYWRlci3lrp7njrDngbDluqblj5HluIM="></span>
### Gray releases based on headers


1. Use the following YAML configuration to bind Canary Nginx Ingress to the new version services. The annotations shown below are used to enable and configure Canary, so as to filter and forward traffic based on headers. In this example, requests with the header name `Region` and value set to `beijing` will be forwarded to the new version services.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: ingress-new # Ingress name
     annotations:
       nginx.ingress.kubernetes.io/canary: "true" # Enable Canary
       nginx.ingress.kubernetes.io/canary-by-header: "Region" # Configure header-based traffic splitting policy
       nginx.ingress.kubernetes.io/canary-by-header-pattern: "beijing" # Requests with the header named Region and the value set to beijing will be forwarded
   spec:
     ingressClassName: nginx # Specify the Ingress Controller.
     rules:
       - host: example.com  # The domain name for external access.
         http:
           paths:
           - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
             path: / # The matching path for the request.
             backend:
               service:
                 name: service-new # The name of the service to forward requests to.
                 port: 
                   number: 80 # The service port number to forward to.
   ```
   

2. Execute the following commands to test. The expected results are as follows.

   * When the `Region` does not exist, requests are forwarded to the old service.

      ```Bash
      curl -H "Host: example.com" http://<EXTERNAL_IP>
      This is the old version of nginx
      ```
      

   * When `Region` exists and its value is not `beijing`, forward to the old service.

      ```Bash
      curl -H "Host: example.com" -H "Region: shanghai" http://<EXTERNAL_IP>
      This is the old version of nginx
      ```
      

   * When `Region` exists and its value is `beijing`, it forwards to the new version of the service.

      ```Bash
      curl -H "Host: example.com" -H "Region: beijing" http://<EXTERNAL_IP>
      This is the new version of nginx
      ```
      


<span id=".5Z-65LqOLWNvb2tpZS3lrp7njrDngbDluqblj5HluIM="></span>
### Gray releases based on cookies


1. Use the following YAML configuration to bind Canary Nginx Ingress to the new version services. The annotations shown below are used to enable and configure Canary, so as to filter and forward traffic based on cookies. In this example, requests with the specific `cookie` set to the value `"beijing"` will be forwarded to the new version services.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: ingress-new # Ingress name
     annotations:
       nginx.ingress.kubernetes.io/canary: "true" # Enable Canary
       nginx.ingress.kubernetes.io/canary-by-cookie: "beijing" # Configure cookie-based traffic splitting policy
   spec:
     ingressClassName: nginx # Specify the Ingress Controller.
     rules:
       - host: example.com  # The domain name for external access.
         http:
           paths:
           - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
             path: / # The matching path for the request.
             backend:
               service:
                 name: service-new # The name of the service to forward requests to.
                 port: 
                   number: 80 # Service port number to forward to
   ```
   

2. Execute the following commands to test. The expected results are as follows.

   * When `Cookie` does not exist, forward to the old service.

      ```Bash
      curl -H "Host: example.com" http://<EXTERNAL_IP>
      This is the old version of nginx
      ```
      

   * When `Cookie` exists and its value is not `beijing`, forward to the old service.

      ```Bash
      curl -s -H "Host: example.com" --cookie "shanghai=always" http://<EXTERNAL_IP>
      This is the old version of nginx
      ```
      

   * When `Cookie` exists and its value is `beijing`, forward to the new service.

      ```Bash
      curl -s -H "Host: example.com" --cookie "beijing=always" http://<EXTERNAL_IP>
      This is the new version of nginx
      ```
      


<span id=".5Z-65LqO5pyN5Yqh5p2D6YeN5a6e546w54Gw5bqm5Y-R5biD"></span>
### Gray releases based on service weights


1. Use the following YAML configuration to bind Canary Nginx Ingress to the new version services. The annotations shown below are used to enable and configure Canary, so as to filter and forward traffic based on service weights. In this example, 25% of requests are forwarded to the new version of the services.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: ingress-new # Ingress name
     annotations:
       nginx.ingress.kubernetes.io/canary: "true" # Enable Canary
       nginx.ingress.kubernetes.io/canary-weight: "25" # Configure a traffic splitting policy based on service weights. A weight of 25 means that 25% of the traffic is forwarded to the new version of the services.
   spec:
     ingressClassName: nginx # Specify an Ingress controller
     rules:
       - host: example.com  # The domain name for external access.
         http:
           paths:
           - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
             path: / # The matching path for the request.
             backend:
               service:
                 name: service-new # The name of the service to forward requests to.
                 port: 
                   number: 80 # Service port number to forward to
   ```
   

2. Execute the following command to test with 20 requests.

   ```Bash
   for i in {1..20}; do curl -H "Host: example.com" http://<EXTERNAL_IP>; done;
   ```
   

   The following responses indicate that 25% of the traffic has been forwarded to the new version of the services as expected.

   ```Bash
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
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is normal to have slight deviations in results due to the small sample size (20 requests). You can perform more tests or increase the sample size.   </div>
   

<span id=".6YWN572u6JOd57u_5Y-R5biD"></span>
## Configuring blue\-green deployments


1. 1. Traffic is split based on service weights. Setting the weight of the new version service to 100 implements blue\-green deployment.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: ingress-new # Ingress name
     annotations:
       nginx.ingress.kubernetes.io/canary: "true" # Enable Canary
       nginx.ingress.kubernetes.io/canary-weight: "100" # Configure the weight of the new Service to 100%, indicating a blue-green deployment
   spec:
     ingressClassName: nginx # Specify the Ingress Controller.
     rules:
       - host: example.com  # The domain name for external access.
         http:
           paths:
           - pathType: Prefix # Path matching rule, with Prefix (prefix matching) as the default setting.
             path: / # The matching path for the request.
             backend:
               service:
                 name: service-new # The name of the service to forward requests to.
                 port: 
                   number: 80 # Service port number to forward to
   ```
   

2. Execute the following command to test with 20 requests.

   ```Bash
   for i in {1..20}; do curl -H "Host: example.com" http://<EXTERNAL_IP>; done;
   ```
   

   The information below is what will be printed on the screen. All traffic has been forwarded to the new version services, while the old version is retained. You can shift traffic and roll back if necessary.

   ```Bash
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
