---
title: "Configuring NGINX Ingresses for traffic mirroring"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_traffic_mirror_for_Nginx_Ingress"
---

NGINX Ingresses support traffic mirroring, which replicates traffic from a cluster to other clusters. This feature is commonly used for simulation testing or stress testing. This topic describes how to configure NGINX Ingresses to implement traffic mirroring.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The traffic mirroring feature of NGINX Ingresses, also known as request mirroring or traffic replication, enables the replication of request traffic from a cluster to multiple target clusters. It supports various application scenarios, including:


* **Stress testing**. When you release a new version of an application, you can replicate traffic from the production cluster where the old version is running to the test cluster for a stress test on the new version. Traffic mirroring allows you to test the availability and performance of the new version without affecting the production environment.

* **Troubleshooting**. When a failure occurs in the production environment, you can replicate the production environment traffic to the test environment for troubleshooting, without affecting the production environment.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Two clusters have been created. For convenience of demonstration, this example assumes two clusters: A and B.

* The ingress\-nginx add\-on has been installed and upgraded to the latest version.

* The cluster has been connected. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* The application image has been uploaded to Container Registry. For details, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).


<span id=".5Zyo6ZuG576k5Lit6YOo572y5Lia5Yqh"></span>
## Deploy applications in clusters

<span id=".5Zyo6ZuG576kLWEt6YeN6YOo572y5Lia5Yqh"></span>
### Deploy applications in cluster A

Deploy old versions of the application and service in cluster A. To do so, follow the steps below:


1. Use the following YAML configuration to create the old versions of the application and service:

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
   

3. Use the following YAML configuration to create an NGINX Ingress and point it to the old version service:

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
   


<span id=".5Zyo6ZuG576kLWIt5Lit6YOo572y5Lia5Yqh"></span>
### Deploy applications in cluster B

Deploy new versions of the application and service in cluster B. To do so, follow the steps below:


1. Use the following YAML configuration to create new versions of the application and service.

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
   

3. Use the following YAML configuration to create an NGINX Ingress and point it to the new version of the service.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: ingress-new # Ingress name
   spec:
     ingressClassName: nginx # Specify the Ingress Controller.
     rules:
       - host: example1.com  # The domain name for external access.
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
   

4. Execute the following command to verify whether the new version of the service is accessible. In the command, `<EXTERNAL_IP>` is the IP address exposed externally by the NGINX Ingress.

   ```Bash
   curl -H "Host: example1.com" http://<EXTERNAL_IP>
   ```
   

   The following result indicates that the new application version is accessible:

   ```Bash
   This is the new version of nginx
   ```
   


<span id=".6YWN572u5rWB6YeP5aSN5Yi2"></span>
## Configuring traffic mirroring

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Cluster B is the test cluster and the receiver of mirrored traffic. You do not need to configure traffic mirroring for cluster B. You need to configure traffic mirroring only for cluster A, which is the production cluster.</div>


* <div data-tips="true" data-tips-type="tip">After traffic is replicated from cluster A to cluster B, the client can receive responses only from cluster A. Responses from cluster B are discarded.</div>



To replicate all traffic that accesses the old application version on cluster A (production cluster) to cluster B (test cluster), you need to configure traffic mirroring on cluster A. To do so, follow the steps below:


1. Use kubectl to connect to production cluster A.

2. Run the following command to edit Nginx\-Ingress:

   ```Bash
   kubectl  edit ingress ingress-old
   ```
   

3. Add the annotation for the traffic mirroring feature in the NGINX Ingress configuration.

   ```YAML
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: ingress-old
     annotations: 
       nginx.ingress.kubernetes.io/mirror-host: example1.com # The target domain name of traffic mirroring.
       nginx.ingress.kubernetes.io/mirror-target: http://14.xxx.xxx.xxx # In cross-cluster scenarios, fill in the corresponding VIP of the NGINX Ingress. In same-cluster scenario, enter the service.
   spec:
     ingressClassName: nginx
     rules:
       - host: example.com
         http:
           paths:
           - pathType: Prefix
             path: /
             backend:
               service:
                 name: service-old
                 port: 
                   number: 80
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For configuration details about NGINX Ingress traffic mirroring, see <a href="https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/#mirror">Mirror</a>.   </div>
   

<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results


1. Query the ingress\-nginx\-controller logs for the new version of the application in cluster B. The results show that the forwarding IP address is the IP address of cluster A.

2. Query the log of the new version of the application `request: "GET /_mirror-30b2558b-5eab-42eb-8ffc-9c128a703479 HTTP/1.1`.

3. Query the logs for the old application version. The results show that calls to the old application version operate normally.


&nbsp;
