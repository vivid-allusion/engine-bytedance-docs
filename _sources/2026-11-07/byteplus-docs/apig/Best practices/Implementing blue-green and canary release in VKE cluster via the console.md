---
title: "Implementing blue-green and canary release in VKE cluster via the console"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Implementing_blue-green_deployment_and_canary_release_of_container_services_via_the_console"
---

The API gateway is deeply integrated with container services VKE, allowing real\-time dynamic acquisition of K8S Service information deployed in the VKE cluster, serving as the traffic entry point for the K8S Service. Additionally, the API gateway provides Upstream traffic allocation, facilitating canary release of services for users, achieving agile iteration and smooth upgrades. This article introduces how to achieve blue\-green deployment and canary release of applications in container services through the API gateway.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

To ensure stable service provision, enterprises pay great attention to the selection of package update strategies. Currently, the widely adopted package update strategies in the industry include blue\-green deployment and canary release; please select the appropriate package update strategy based on actual circumstances.


* **Blue\-green release**: Simultaneously runs two versions of the application. During a blue\-green deployment, the old version continues to serve, and once the new version is up and running, traffic is switched entirely to the new version. Generally, the new version maintains the same resource specifications as the old version, meaning the service has two completely identical deployment environments. After the new version starts providing services, the old version will serve as a hot backup. If there is a problem after the new version is published, traffic can be quickly switched back to the old version, significantly shortening the fault recovery time.

* **Canary release**: Also known as a canary release, it is a package update strategy for a smooth transition from an old version to a new version. This package update strategy first publishes a new version, splitting a small portion of the live traffic from the old version to the new version to test the new version's actual performance in the production environment. After the new version performs as expected in the environment, progressively increase the allocation ratio of traffic until it completely replaces the old version.


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

This article demonstrates blue\-green and canary releases of applications in a container service cluster through a **service\-demo** service. This service has provided an interface to query the current version, with the request path being `/version`. API gateway abstracts this **service\-demo** service as an Upstream, identifying old version v1 and new version v2 through Pod labels. After users send requests, the API gateway can forward the requests to new and old versions according to the set weights, achieving multi\-version traffic management of the application.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Vital Kubernetes Engine

   * The Volcengine Kubernetes Engine service has been activated.

   * An VKE cluster has been created. For details, please refer to [Creating a cluster](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* API Gateway

   * The API Gateway service has been activated.

   * An APIG instance has been created. For more details, please refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

   * A service has been created and a custom Domain name has been bound. For details please refer to [Creating a service](https://docs.byteplus.com/en/docs/apig/Creating_a_service), [Adding domain name](https://docs.byteplus.com/en/docs/apig/Adding_domain_name).

   * A cluster has been imported into the API Gateway. For details please refer to [Importing VKE cluster](https://docs.byteplus.com/en/docs/apig/Import_container_cluster).


<span id=".5Z-65LqO55u45ZCM5pyN5Yqh55qE5LiN5ZCM54mI5pys5a6e546w54Gw5bqm5Y-R5biD"></span>
## Implement canary release based on different versions of the same service

<span id=".5q2l6aqk5LiA77ya6YOo572y5pen54mI5pys5bqU55So"></span>
### Step 1: Deploy the previous version of the application


1. Use the following YAML configuration to deploy version v1 of the application and Service in the cluster.

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: app-old
     namespace: default 
   spec:
     replicas: 2
     selector:
       matchLabels:
         app: demo
     template:
       metadata:
         labels:
           app: demo
           version: v1
       spec:
         containers:
         - image: cr-apig-cn-beijing.cr.volces.com/apig-demo/http-server:v1
           name: demo
           ports:
           - containerPort: 80
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: service-demo
   spec:
     selector:
       app: demo
     ports:
     - name: rule
       protocol: TCP
       port: 80
       targetPort: 80
     type: NodePort
   ```
   

2. Create an upstream and associate it with the service\-demo service.

3. Add a `version:v1` label to the Upstream. This label corresponds to the `spec.template.metadata.labels` configuration of the Pod, used to differentiate between different versions of the application. For details, please refer to [Managing upstream versions](https://docs.byteplus.com/en/docs/apig/Managing_Upstream_Versions_of_Container_Service_Types).

4. Create a route, and publish the service. The request path is `/version`, the target Upstream is the service\-demo Service, the version is v1, and the weight is 100%.

5. Run the following commands to conduct 10 access tests.

   ```bash
   for i in {1..10}; do curl ${Gateway Service Domain name}/version;echo;done
   ```
   

   The expected results are as follows, all requests are successfully forwarded to the version v1 application.

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
   


<span id=".5q2l6aqk5LqM77ya5Y-R5biD5paw54mI5pys5bqU55So"></span>
### Step 2: Publish a new version of the application.


1. Deploy the version v2 of the application and Service using the YAML configuration in the cluster.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Use the APIG instance to publish applications in the cluster, supporting deployment within the same cluster and across clusters.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For intr\-cluster deployment, the applications need to be deployed under the same cluster and the same namespace.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For cross\-cluster deployment, the applications need to be deployed under the same namespace across clusters.   </div>
   

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: app-new
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: demo
     template:
       metadata:
         labels:
           app: demo
           version: v2
       spec:
         containers:
         - image: cr-apig-cn-beijing.cr.volces.com/apig-demo/http-server:v2
           name: demo
           ports:
           - containerPort: 80
   ```
   

2. Add the version identifier `version:v2` to the already created Upstream. For details, please refer to [Managing upstream versions](https://docs.byteplus.com/en/docs/apig/Managing_Upstream_Versions_of_Container_Service_Types).

3. Modify the created Ingress rules to forward traffic to versions v1 and v2 as per the required weight. In this example, configure the application weight as 80% for v1 and 20% for v2. For details, please refer to [Creating a route](https://docs.byteplus.com/en/docs/apig/Managing_route).

4. Execute the following commands to perform a test with 10 accesses.

   ```bash
   for i in {1..10}; do curl ${Gateway Service Domain name}/version;echo;done
   ```
   

   The expected result is as follows: 2 out of 10 requests are forwarded to the new version v2, and the traffic ratio meets expectations.

   ```bash
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In real business scenarios, after the new version is verified, you can continue to increase the traffic weight of the new version. During this period, pay attention to scale\-out the new version and scale\-in the old version as needed.   </div>
   

<span id=".5Z-65LqO5LiN5ZCM5pyN5Yqh5a6e546w54Gw5bqm5Y-R5biD"></span>
## Implement a canary release based on different services

<span id=".5q2l6aqk5LiA77ya6YOo572y5pen54mI5pys5bqU55So"></span>
### Step 1: Deploy the old version of the application


1. Use the following YAML configuration to deploy the v1 version of applications and services in the cluster.

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
   

2. Create a upstream and associate it with the service\-old service.

3. Create a route, and publish the service. In which, the request path is `/version`, the target Upstream is the Service\-old service, with a weight of 100%.

4. Execute the following commands to perform a 10\-access test.

   ```bash
   for i in {1..10}; do curl ${Service Domain name}/version;echo;done
   ```
   

   The expected results are as follows, all requests are forwarded to the version v1 application.

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
   


<span id=".5q2l6aqk5LqM77ya5Y-R5biD5paw54mI5pys5bqU55So"></span>
### Step 2: Publish a new version of the application


1. Use the following YAML configuration to deploy version v2 of the application and Service in the cluster.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Publish applications in the cluster using an APIG instance, supporting deployment within the same cluster and across clusters.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For deployment within the same cluster, it must be deployed under the same namespace of the same cluster.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For cross\-cluster deployment, it must be deployed under a namespace with the same name across clusters.   </div>
   

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
   

2. Create an upstream and associate it with servcie\-new service.

3. Modify the existing Ingress rules to forward traffic to service\-old Service and service\-new service according to the desired weight. In this example, configure service\-old service with a weight of 80% and service\-new service with a weight of 20%. For more details, please refer to [Route management](https://docs.byteplus.com/en/docs/apig/Managing_route).

4. Run the following commands for a 10\-time access test.

   ```bash
   for i in {1..10}; do curl ${Gateway Service Domain name}/version;echo;done
   ```
   

   The expected results are as follows: 2 out of 10 requests are forwarded to the new Service, and the traffic ratio meets the expected proportion.

   ```bash
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v2"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   {"code": 200, "message": "version: v1"}
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In real business scenarios, after the new Service is validated, you can continue to increase the traffic weight allocated to the new Service. During this period, pay attention to scale\-out the new Service and scale\-in the old Service as needed.   </div>
   

<span id=".5Z-65LqOIEhlYWRlciDlrp7njrDngbDluqblj5HluIM="></span>
## Implement canary release based on Header.

<span id=".5q2l6aqk5LiA77ya6YOo572y5pen54mI5pys5bqU55So"></span>
### Step 1: Deploy the old version of the application.


1. Use the following YAML configuration to deploy version v1 of the application and service in the cluster.

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
   

2. Create a upstream and associate it with the servcie\-old service.

3. Create a route and publish the service. In this case, the request `/version` targets the upstream 'service\-old', with a weight of 100%.

4. Execute the following command for 10 access tests.

   ```bash
   for i in {1..10}; do curl ${Gateway Service Domain name}/version;echo;done
   ```
   

   The expected result is as follows: all requests are forwarded to the version v1 application.

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
   


<span id=".5q2l6aqk5LqM77ya5Y-R5biD5paw54mI5pys5bqU55So"></span>
### Step 2: Publish the new version of the application.


1. Deploy the v2 version of the application and service in the cluster.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Publish applications within the cluster using an APIG instance, supporting intra\-cluster and inter\-cluster deployments.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For intra\-cluster deployments, it should be deployed in the same cluster and the same namespace.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For inter\-cluster deployments, it should be deployed in a similarly namespace across clusters.   </div>
   

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
   

2. Create an upstream and associate it with service\-new service.

3. Create a route, and publish service\-new service. Among them:

   * Configuration request header: Route matches when header foo is bar.

   * Target upstream: configured for the service\-new service.

4. Execute the following command, to perform 10 access requests without including Headers.

   ```bash
   for i in {1..10}; do curl ${Gateway Service Domain name}/version;echo;done
   ```
   

   The expected response result is as follows. Since the Header is not included, all access requests are forwarded to the v1 Service.

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
   

5. Execute the following commands, to perform 10 access requests that include Headers.

   ```bash
   for i in {1..10}; do curl -H "foo:bar" ${Gateway Service Domain Name}/version;echo;done
   ```
   

   The expected response result is as follows. Since the Header is included, all access requests are forwarded to the v2 Service.

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
   

   As shown above, both routes allow access through the same Service domain name; if the access includes a Header (foo=bar), it is forwarded to the v2 version of the application; otherwise, it is forwarded to the v1 version of the application.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In real business scenarios, after the new service has been validated, you can continue to increase the traffic weight directed to the new service. During this period, pay attention to scale\-out the new service, and scale\-in the old service as needed.   </div>
