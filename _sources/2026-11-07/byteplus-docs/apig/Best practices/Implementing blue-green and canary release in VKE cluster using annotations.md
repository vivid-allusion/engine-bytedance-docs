---
title: "Implementing blue-green and canary release in VKE cluster using annotations"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Using_annotations_to_achieve_bluegreen_deployment_and_canary_release_in_VKE_application"
---

The API gateway deeply integrates with container services VKE, which can dynamically obtain information about K8S Services deployed in the VKE cluster in real\-time to serve as the traffic entry point for the K8S Services exposed externally. Simultaneously, the API gateway provides Upstream and traffic weight capabilities, facilitating users in deploying canary releases for services to achieve agile iterations and smooth upgrades. This article introduces how to implement blue\-green deployment and canary release for applications in container services via the API gateway.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

To ensure stable service provision externally, enterprises place great importance on the selection of package update strategies. The widely adopted service package update strategies in the industry include blue\-green deployment and canary release, please select a suitable package update strategy according to actual circumstances.


* **Blue\-green release**: Running two versions of the application simultaneously. During the blue\-green deployment, the old version continues to serve externally while the new version is brought online; subsequently, traffic is entirely switched to the new version. Generally, the resource specifications of the new version are kept consistent with those of the old version, equivalent to having two completely identical deployment environments for the service. Once the new version starts serving externally, the old version will be used as a hot standby. If issues arise after the new version is published, traffic can swiftly be switched back to the old version, greatly reducing the fault recovery time.

* **Canary release**: Also known as a canary deployment, is a package update strategy that smoothly transitions from the old version to the new version. This package update strategy first publishes a new version, splitting a small portion of the live traffic from the old version to the new version to test the new version's actual performance in the production environment. After the new version performs as expected in the environment, progressively increase the allocation ratio of traffic until it completely replaces the old version.


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

This article demonstrates the blue\-green deployment and canary release of applications within a container service cluster by configuring two services. The service has provided an interface to query the current version, the path being `/version`. After the user sends a request, the API gateway can forward the request to different services based on the header or weight, achieving multi\-version traffic management of the application.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Volcengine Kubernetes Engine

   * The container service has been actived.

   * A Volcengine Kubernetes Engine cluster has been created. For details, please refer to [Creating a cluster](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* API Gateway

   * The API Gateway has been activated.

   * An APIG instance has been created. For details refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

   * A Service has been created and a Custom Domain name has been bound. For details, please refer to [Creating a Service](https://docs.byteplus.com/en/docs/apig/Creating_a_service), [Adding CNAME record](https://docs.byteplus.com/en/docs/apig/Adding_domain_name).

   * A cluster has been imported into the API Gateway, and the Ingress route synchronization feature has been enabled. For details, please refer to [Importing the VKE cluster](https://docs.byteplus.com/en/docs/apig/Import_container_cluster), [Cluster route synchronization](https://docs.byteplus.com/en/docs/apig/Cluster_ingress_synchronization).


<span id=".5Z-65LqOIEhlYWRlciDlrp7njrDngbDluqblj5HluIM="></span>
## Implementing canary release based on Header

<span id=".5q2l6aqk5LiA77ya6YOo572y5pen54mI5pys5bqU55So"></span>
### Step 1: Deploy the old version of the application


1. Using the following YAML configuration, deploy version v1 of the application and service within the cluster.

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name:  service-old
     namespace: default
   spec:
     ports:
     - name: port
       port: 80
       targetPort: 80
       protocol: TCP
     selector:
       app: old
     type: ClusterIP
   ---
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: app-old
     namespace: default 
   spec:
     replicas: 2
     selector:
       matchLabels:
         app: old
     template:
       metadata:
         labels:
           app: old
       spec:
         containers:
         - image: cr-apig-cn-beijing.cr.volces.com/apig-demo/http-server:v1
           name: demo
           ports:
           - containerPort: 80
   ```
   

2. Use the following YAML configuration to create an Ingress in the cluster.

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: ingress-old
     namespace: default
   spec:
     ingressClassName: apig
     rules:
       - host: apig-example.com
         http:
           paths:
             - backend:
                 service:
                   name: service-old
                   port:
                     number: 80
               path: /version
               pathType: Exact
   ```
   

3. Execute the following command to conduct 10 access tests.

   ```bash
   for i in {1..10}; do curl apig-example.com/version;echo;done
   ```
   

   Expected results as follows, all requests are successfully forwarded to the v1 version application.

   ```bash
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   ```
   


<span id=".5q2l6aqk5LqM77ya54Gw5bqm5Y-R5biD5paw54mI5pys5pyN5Yqh"></span>
### Step 2: Canary release the new version of the Service.


1. Use the following YAML configuration to deploy v2 version applications and services in the cluster.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Use the APIG instance to publish applications in the cluster, supporting deployment within the same cluster and across clusters.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When deploying within the same cluster, applications need to be deployed under the same namespace in the same cluster.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When deploying across clusters, applications need to be deployed under the same\-named namespace across clusters.   </div>
   

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: service-new
     namespace: default
   spec:
     ports:
     - name: port
       port: 80
       targetPort: 80
       protocol: TCP
     selector:
       app: new
     type: ClusterIP
   ---
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: app-new
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: new
     template:
       metadata:
         labels:
           app: new
       spec:
         containers:
         - image: cr-apig-cn-beijing.cr.volces.com/apig-demo/http-server:v2
           name: demo
           ports:
           - containerPort: 80
   ```
   

2. Use the following YAML configuration to create an Ingress for the new version service in the cluster.

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     annotations:
       nginx.ingress.kubernetes.io/canary: 'true'
       # turn on canary release
       nginx.ingress.kubernetes.io/canary-by-header: 'foo'
       nginx.ingress.kubernetes.io/canary-by-header-value: 'bar'
       # When headers include foo=bar, forward to v2 version of the Service. When not carrying this header, forward to v1 version of the Service
     name: ingress-new
     namespace: default
   spec:
     ingressClassName: apig
     rules:
       - host: apig-example.com
         http:
           paths:
             - backend:
                 service:
                   name: service-new
                   port:
                     number: 80
               path: /version
               pathType: Exact
   ```
   

3. Execute the following command to perform 10 access tests without carrying a Header.

   ```bash
   for i in {1..10}; do curl apig-example.com/version;echo;done
   ```
   

   The expected result is as follows: all requests are successfully forwarded to version v1 of the application.

   ```bash
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   ```
   

4. Execute the following command, accessing 10 times with a Header for testing.

   ```bash
   for i in {1..10}; do curl -H "foo:bar" ${APIG Service Domain name}/version;echo;done
   ```
   

   The expected result is as follows: all requests are successfully forwarded to version v2 of the application.

   ```bash
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v2"}
   ```
   


As a result, both routes are accessed through `apig-example.com/version`. If the Header (foo=bar) is present, it’s forwarded to the version v2 Service; otherwise, it's forwarded to the version v1 Service. Implemented canary release based on Header.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In real\-world application scenarios, once the new version is validated, you can continue to increase the traffic weight allocated to the new version. During this time, pay attention to scale out the new version and scale in the old version as needed.</div>


<span id=".5Z-65LqO5p2D6YeN5a6e546w54Gw5bqm5Y-R5biD"></span>
## Implementing canary release based on weight.

<span id=".5q2l6aqk5LiA77ya6YOo572y5pen54mI5pys5bqU55So"></span>
### Step 1: Deploy the old version of the application.


1. Use the following YAML configuration to deploy the version v1 app and Service in the cluster.

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name:  service-old
     namespace: default
   spec:
     ports:
     - name: port
       port: 80
       targetPort: 80
       protocol: TCP
     selector:
       app: old
     type: ClusterIP
   ---
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: app-old
     namespace: default 
   spec:
     replicas: 2
     selector:
       matchLabels:
         app: old
     template:
       metadata:
         labels:
           app: old
       spec:
         containers:
         - image: cr-apig-cn-beijing.cr.volces.com/apig-demo/http-server:v1
           name: demo
           ports:
           - containerPort: 80
   ```
   

2. Use the following YAML configuration to create an Ingress in the cluster.

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: ingress-old
     namespace: default
   spec:
     ingressClassName: apig
     rules:
       - host: apig-example.com
         http:
           paths:
             - backend:
                 service:
                   name: service-old
                   port:
                     number: 80
               path: /version
               pathType: Exact
   ```
   

3. Execute the following command to perform 10 access tests.

   ```bash
   for i in {1..10}; do curl apig-example.com/version;echo;done
   ```
   

   The expected result is as follows, all requests are successfully forwarded to the v1 version of the application.

   ```bash
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   ```
   


<span id=".5q2l6aqk5LqM77ya54Gw5bqm5Y-R5biD5paw54mI5pys5pyN5Yqh"></span>
### Step 2: canary release a new version of the Service.


1. Use the following YAML configuration to deploy the v2 version of the application and its services in the cluster.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Use the APIG instance to publish applications within the cluster, supporting deployments within the same cluster as well as across different clusters.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For deployments within the same cluster, applications should be deployed under the same namespace in the same cluster.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For cross\-cluster deployments, applications should be deployed under the same\-name namespace across clusters.   </div>
   

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: service-new
     namespace: default
   spec:
     ports:
     - name: port
       port: 80
       targetPort: 80
       protocol: TCP
     selector:
       app: new
     type: ClusterIP
   ---
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: app-new
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: new
     template:
       metadata:
         labels:
           app: new
       spec:
         containers:
         - image: cr-apig-cn-beijing.cr.volces.com/apig-demo/http-server:v2
           name: demo
           ports:
           - containerPort: 80
   ```
   

2. Use the following YAML configuration to create an Ingress for the new version of the service in the cluster.

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     annotations:
       nginx.ingress.kubernetes.io/canary: 'true'
       # turn on canary release
       nginx.ingress.kubernetes.io/canary-weight: '30'
       # configuration traffic weight, forward 30% of the traffic to v2 Service, 70% of the traffic to v1 Service
     name: ingress-new
     namespace: default
   spec:
     ingressClassName: apig
     rules:
       - host: apig-example.com
         http:
           paths:
             - backend:
                 service:
                   name: service-new
                   port:
                     number: 80
               path: /version
               pathType: Exact
   ```
   

3. Execute the following command to perform 10 access tests.

   ```bash
   for i in {1..10}; do curl apig-example.com/version;echo;done
   ```
   

   The expected result is as follows: out of 10 requests, 3 are forwarded to the new version v2, and the traffic ratio meets expectations.

   ```bash
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v1"}
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In real business scenarios, after the new version is verified, the traffic weight to the new version can be increased accordingly. During this period, pay attention to scale\-out the new version and scale\-in the old version as needed.   </div>
