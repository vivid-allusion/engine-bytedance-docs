---
title: "Use API Gateway to implement north-south traffic management for multiple clusters"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Use_API_Gateway_to_implement_north-south_traffic_management_for_multiple_clusters"
---

The API gateway supports connecting to Vital Kubernetes Engine (VKE) clusters and custom clusters, providing robust north\-south traffic management features for multiple clusters. This article introduces common north\-south traffic management scenarios and configuration methods.

<span id="5IeAtMib"></span>
## Background information

The API gateway supports connecting to Vital Kubernetes Engine clusters and registered clusters, allowing connection to and management of standard Kubernetes clusters across different regions and infrastructures. The management scope includes local clusters, third\-party public cloud clusters, Internet Data Center (IDC) self\-built clusters, edge clusters, and other Kubernetes clusters that comply with CNCF (Cloud Native Computing Foundation) standards. Implement multi\-cluster management capability The API gateway can provide managed cloud\-native gateway features for multi\-cloud and multi\-cluster, and achieve a highly available and highly scalable method for Ingress traffic management. You can obtain information about Services deployed in different clusters in real time and dynamically. Each Service acts as the traffic entry point for providing external services. Also provides upstream traffic allocation, making it easier for users to perform canary releases of services and achieve agile iteration and smooth upgrades.

This article uses a service\-demo Service and two modified standard Nginx images as examples to demonstrate how to manage north\-south traffic across multiple clusters when connecting an API gateway to multiple clusters.

<span id="mb8MhmML"></span>
## Prerequisites


* Vital Kubernetes Engine (VKE)

   * Vital Kubernetes Engine has been activated.

   * The Vital Kubernetes Engine cluster has been created. For details, refer to [Create cluster](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * A custom cluster has been registered. For details, refer to [Register an existing cluster using the proxy method](https://docs.byteplus.com/en/docs/vke/Register_the_cluster_by_proxy).

* API Gateway

   * API Gateway has been activated.

   * An APIG instance has been created. For details, refer to [Create Instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

   * The service has been created and the custom domain name has been bound. For details, refer to [Create service](https://docs.byteplus.com/en/docs/apig/Creating_a_service) and [Add custom domain name](https://docs.byteplus.com/en/docs/apig/Adding_domain_name).


<span id="Dj7uVGX7"></span>
## Step 1: Import cluster


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, select **Backend management \> Associated Kubernetes**.

4. On the cluster list page, click **Import cluster** to separately import Vital Kubernetes Engine clusters and custom clusters. For details, refer to [Import container clusters](https://docs.byteplus.com/en/docs/apig/Import_container_cluster) and [Import registered clusters](https://docs.byteplus.com/en/docs/apig/Import_a_registered_cluster).


<span id="sVfzUOg5"></span>
## Step 2: Deploy an application


1. Use the following YAML configuration to deploy applications and services in the Vital Kubernetes Engine cluster.


```YAML
apiVersion: v1
kind: Service
metadata:
  name:  service-demo
  namespace: default
spec:
  ports:
  - name: port
    port: 80
    targetPort: 80
    protocol: TCP
  selector:
    app: demo
  type: ClusterIP
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
  namespace: default 
spec:
  replicas: 4
  selector:
    matchLabels:
      app: demo
  template:
    metadata:
      labels:
        app: demo
        clusterId: cd2vajnv989sp6*** # Add a Label to the Pod. Traffic management can be achieved through this Label. In this example, the cluster ID is used as the Label.
    spec:
      containers:
      - image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v2.0
        name: demo
        ports:
        - containerPort: 80
```



2. Use the following YAML configuration to deploy another version of the application and service in the registered cluster.


```YAML
apiVersion: v1
kind: Service
metadata:
  name: service-demo
  namespace: default
spec:
  ports:
  - name: port
    port: 80
    targetPort: 80
    protocol: TCP
  selector:
    app: demo
  type: ClusterIP
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo
  template:
    metadata:
      labels:
        app: demo
        clusterId: cd2va60cu04*** # Add a Label to the Pod to enable traffic management through that Label. In this example, the cluster ID is used as the Label.
    spec:
      containers:
      - image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v3.0
        name: demo
        ports:
        - containerPort: 80
```


<span id="JV7kP6bn"></span>
## Step 3: Create Upstream


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, select **Backend Management \> Upstream list**.

4. On the Upstream list page, click **Create Upstream** to create an Upstream of the Vital Kubernetes Engine type. For details, refer to [Create an Upstream of Vital Kubernetes Engine type](https://docs.byteplus.com/en/docs/apig/Creating_a_Vital_Kubernetes_Engine_type_Upstream).


<span id="PdVFq53W"></span>
## Step 4: Use API Gateway to manage north\-south traffic across multiple clusters

<span id="yGfWpVMZ"></span>
### Scenario 1: Default load balancing to the backend of the Service with the same name

The API gateway can dynamically obtain information about Services deployed in different clusters in real time, serving as the traffic entry point for Services to provide external services. By default, the API gateway load balances traffic to the backends of services with the same name across all clusters, evenly distributing traffic among all replicas. Therefore, the proportion of traffic routed to different clusters matches the proportion of application replicas in those clusters. For example, in this case, the number of application replicas in the Vital Kubernetes Engine cluster and the custom cluster is 4 to 1, so the proportion of traffic routed to each cluster is also 4 to 1. The traffic forwarding diagram is shown below.

Configuration steps:


1. In the left navigation bar, select **Route Management \> Route List**. Click **add route**, configure route information. Select the Upstream for the Vital Kubernetes Engine type, and set the application weight to 100%. 100% of the traffic will soon be forwarded to the corresponding Upstream. For more configuration details, refer to [Manage Routing](https://docs.byteplus.com/en/docs/apig/Managing_route).

2. Execute the following command to perform 10 access tests. `xxx.xxx.xxx.xxx` is the access entry IP address of the APIG instance. To obtain the IP address, refer to [Add access entry](https://docs.byteplus.com/en/docs/apig/Adding_access_entrance).


```Bash
for i in {1..10}; do curl -H "host: apig-example.com" xxx.xxx.xxx.xxx; sleep 1; done
```


The expected result is as follows: out of 10 requests, 2 are forwarded to the registered cluster, and the traffic ratio matches the ratio of application replicas. This meets expectations.

```Bash
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the new version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the new version of nginx
This is the old version of nginx
```


<span id="yGfWpVMZ"></span>
### Scenario 2: Route traffic based on weight

In multi\-cluster scenarios, the API gateway supports specifying canary labels in the Upstream, and allows assigning a weight to each canary label when configuring routing. The API gateway routes traffic based on weight. The traffic forwarding diagram is shown below.

Configuration steps are as follows:


1. In the left navigation bar, select **Backend Management \> Upstream List**. On the Upstream list page, click the target Upstream name to enter the Upstream Overview page.

2. Click **Add canary label** to add a version label for Upstream. This label corresponds to the `spec.template.metadata.labels` configuration in the Pod. For details, refer to Step 2 above. A cluster ID is used as an identifier in this document, for example `clusterId:cd2vajnv989sp6***`. For more configuration details, refer to [Management of Upstream versions for Vital Kubernetes Engine types](https://docs.byteplus.com/en/docs/apig/Managing_Upstream_Versions_of_Container_Service_Types).

3. In the left navigation bar, select **Route management \> Route list**. Click **add route**. Configure route list. Select an Upstream of the Vital Kubernetes Engine type, and route traffic to different clusters based on the specified weights. In this example, the weight of the Vital Kubernetes Engine cluster is 80%, and the weight of the custom cluster is 20%. For more configuration details, refer to [Manage routing](https://docs.byteplus.com/en/docs/apig/Managing_route).

4. Run the following command to perform 10 access tests. `xxx.xxx.xxx.xxx` is the entry IP address of the APIG instance. To obtain it, refer to [Add access entry](https://docs.byteplus.com/en/docs/apig/Adding_access_entrance).


```Bash
for i in {1..10}; do curl -H "host: apig-example.com" xxx.xxx.xxx.xxx; sleep 1; done
```


The expected result is as follows: of 10 requests, 2 are forwarded to the registered cluster, and the traffic ratio matches the weight, which meets expectations.

```Bash
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the new version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the new version of nginx
This is the old version of nginx
```


<span id="4axQk5Yb"></span>
### Scenario 3: Traffic is routed only to the specified cluster

When traffic routing is configured based on weight, if only one target cluster is specified in the route and the weight is set to 100%. This achieves the purpose of routing only to the specified cluster. The traffic forwarding diagram is shown below.

Configuration steps are as follows:


1. Select **Backend management \> Upstream list** from the navigation bar on the left. On the Upstream list page, click the target Upstream name to enter the Upstream Overview page.

2. Click **Add canary label** to add a version label for Upstream. This identifier corresponds to the `spec.template.metadata.labels` configuration in the Pod. For details, refer to Step 2 above. Cluster IDs are used in this document, for example `clusterId:cd2vajnv989sp6***`. For more configuration details, refer to [Manage Upstream versions for Vital Kubernetes Engine type](https://docs.byteplus.com/en/docs/apig/Managing_Upstream_Versions_of_Container_Service_Types).

3. In the left navigation bar, select **Route management \> Route list**, click **add route**, and configure the route information. Select the Upstream for Vital Kubernetes Engine, configure the application weight to 100%, and specify the cluster in the **canary label**. For details, refer to [Manage routing](https://docs.byteplus.com/en/docs/apig/Managing_route).

4. Run the following command to perform 10 access tests. `xxx.xxx.xxx.xxx` is the entry point IP address for the APIG instance. To obtain it, refer to [Add an access entry](https://docs.byteplus.com/en/docs/apig/Adding_access_entrance).


```Bash
for i in {1..10}; do curl -H "host: apig-example.com" xxx.xxx.xxx.xxx; sleep 1; done
```


The expected result is as follows: all requests are forwarded to the designated cluster, as expected.

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
```


<span id="eVxx3bts"></span>
### Scenario 4: Route traffic based on headers

In multi\-cluster scenarios, the API gateway supports specifying a canary label in the Upstream and routing traffic via the Header when configuring routes. The traffic forwarding diagram is shown below.

Configuration steps


1. In the left navigation bar, select **Backend management \> Upstream list**. On the Upstream list page, click the target Upstream name to enter the Upstream Overview page.

2. Click **Add canary label** to add a version label for Upstream. This identifier corresponds to the `spec.template.metadata.labels` configuration in the Pod. For details, refer to Step 2 above. A cluster ID is used as an identifier in this document, for example `clusterId:cd2vajnv989sp6***`. For more configuration details, refer to [Manage the Upstream version of Vital Kubernetes Engine types](https://docs.byteplus.com/en/docs/apig/Managing_Upstream_Versions_of_Container_Service_Types).

3. In the left navigation bar, select **Route management \> Route list**. Click **add route**, then configure the route list.

   * Configure a route that does not include a Header, and specify the forwarding cluster. In this example, traffic that does not include Header is forwarded to the Vital Kubernetes Engine cluster.

   * Configure a route that includes a Header, and specify the cluster to forward to. In this example, the Header is `foo:bar`, forwarded to a custom cluster.

4. Run the following commands to perform 10 access tests. `xxx.xxx.xxx.xxx` is the entry IP address of the APIG instance. To obtain this address, refer to [Add access entry](https://docs.byteplus.com/en/docs/apig/Adding_access_entrance).


```Bash
for i in {1..10}; do curl -H "host: apig-example.com" xxx.xxx.xxx.xxx; sleep 1; done
```


The expected result is as follows: when the incoming traffic does not contain the Header, all traffic is forwarded to the Vital Kubernetes Engine cluster, as expected.

```Bash
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
This is the old version of nginx
```



5. Execute the following command, and then perform 10 access tests including Header. Here, `xxx.xxx.xxx.xxx` is the entry IP address for the APIG instance. To obtain the IP address, refer to [Add access entry](https://docs.byteplus.com/en/docs/apig/Adding_access_entrance).


```Bash
for i in {1..10}; do curl -H "host: apig-example.com" -H "foo:bar" xxx.xxx.xxx.xxx; sleep 1; done
```


The expected result is as follows: when the incoming traffic contains the Header, all traffic is forwarded to the custom cluster, which is as expected.

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
```


&nbsp;
