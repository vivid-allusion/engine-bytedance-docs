---
title: "Monitoring custom Kubernetes clusters"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Monitoring_custom_Kubernetes_clusters"
---

Multi\-cloud cluster monitoring is a common requirement of users. This topic describes how to use Vital Managed Service for Prometheus (VMP) to monitor custom Kubernetes clusters.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

<span id=".5aSa5LqR6ZuG576k55uR5o6n6Z2i5Li055qE5oyR5oiY"></span>
### Challenges in multi\-cloud cluster monitoring

The usage of multi\-cloud clusters (such as multi\-vendor clusters and hybrid cloud clusters consisting of public cloud clusters and self\-built clusters) provides the following benefits for enterprises: diversified risks, reduced costs, abundant resources, and flexible selections. However, the cross\-vendor and cross\-region cluster architecture also leads to the following issues, which are outstanding in multi\-cloud monitoring:  


* **Challenges in data aggregation and visualization**: Monitoring data is distributed across different geographic locations, which cannot be aggregated and displayed in a centralized manner. As a result, a monitoring dashboard that provides a global view cannot be created, and administrators cannot know the status and performance of all clusters at a glance.

* **Resource and cost management**: To monitor multi\-cloud clusters, you must build multiple monitoring systems, which leads to higher resource consumption and monitoring costs.

* **Complexity of configuration and management**: Repeated configuration and management policies may be required to manage multi\-cloud clusters, which increases management complexity. In addition, monitoring consistency cannot be ensured caused by monitoring system fragmentation. In this way, potential faults and issues cannot be identified in a timely manner.

* **Fault diagnosis and response**: In a multi\-cloud environment, locating and diagnosing issues may be more difficult because cross\-cloud resources and services may be involved. Therefore, the processes that consist of monitoring, fault response, and upgrade must be consistent. This ensures that issues are resolved in a timely manner to reduce impacts on businesses.


To ensure the monitoring consistency for multi\-cloud clusters, VMP provides multi\-cloud cluster monitoring solutions and collection agents. This allows users to monitor cloud services and integrate and monitor third\-party clusters and self\-managed clusters in a centralized manner.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic describes how to quickly configure multi\-cloud cluster monitoring by using one of the easiest ways. The related agents adopt the default specifications and are not mounted with a PersistentVolumeClaim (PVC) for persistent storage. This helps users quickly know how to integrate custom clusters with VMP.</div>


<span id=".55uR5o6n5pa55qGI"></span>
### Monitoring solution

VMP provides you with two ready\-to\-use metric collection solutions. VMP allows you to directly install collection agents in standard Kubernetes clusters and integrate the clusters with VMP workspaces to collect and aggregate metrics related to multi\-cloud clusters. This achieves the monitoring of multi\-cloud clusters in a centralized manner. For more details, see [Integrating self-managed Kubernetes clusters](https://docs.byteplus.com/en/docs/vmp/Connecting-to-self-built-Kubernetes-cluster).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus root user has been created, and VKE has been activated.

   * A cluster has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * The ingress\-nginx agent is installed in the cluster and internal network load balancing is configured. For more details, refer to [Installing an add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* Cloud Enterprise Network (CEN) is activated, and the internal network of  and the network where the custom cluster is located are connected. For more details, refer to the [documentation of CEN](https://docs.byteplus.com/en/docs/cen/Product-Overview-01).

* A self\-built or custom cluster is created.

   * The Kubernetes version of the custom cluster is v1.20 to v1.24. Otherwise, compatibility issues may occur.

   * Ensure that the custom cluster can access the public network. If not, refer to [How do I download and deploy a collector in an environment without a public network?](https://docs.byteplus.com/en/docs/vmp/Monitoring_custom_Kubernetes_clusters#.5peg5YWs572R546v5aKD5aaC5L2V5LiL6L295bm26YOo572y6YeH6ZuG5Zmo)

   * A namespace is created. This topic takes volcano\-metrics as an example.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not install the collection agents of the open source Prometheus or other monitoring systems in a custom cluster. These agents may conflict with the collector agent provided by VMP, leading to agent exceptions.   </div>
   

* kubectl can be used to connect to clusters in the local environment (Linux/Mac). The clusters include VKE clusters and custom Kubernetes clusters.


<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedure

<span id=".5q2l6aqk5LiA77ya5ZyoIFZLRSDpm4bnvqTkuK3phY3nva7lt6XkvZzljLrku6PnkIY="></span>
### Step 1: Configure a workspace proxy in the VKE cluster

VMP workspaces provide Remote Write URLs. After you connect the VPC of your custom cluster to the BytePlus network using CEN, you can use a proxy to write large\-scale metric data persistently to the VMP workspace.


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview). 

2. In the left navigation pane, click ** Services and Ingresses** \> **Service**. Click **Create with Yaml** to create a service. To access the VMP workspace via a Service of type `ExternalName`, you need to provide the workspace address. For information about obtaining a workspace address, see [Obtaining workspace addresses](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL?lang=en).


```yaml
apiVersion: v1
kind: Service
metadata:
  name: vmp-service
spec:
  externalName: write.prometheus-cn-beijing.ivolces.com # The domain name of the VMP workspace. Domain names of workspaces vary based on different regions.
  ports:
  - name: vmp
    port: 80
    protocol: TCP
    targetPort: 80
  sessionAffinity: None
  type: ExternalName
```



2. Click **Workload \> Resource Explorer** in the left navigation pane. Click **Create with Yaml** to create an Ingress. Specify the mapping relationship between the custom domain name and the service.

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the YAML configuration in the **Yaml**field.


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: vmp-ingress
spec:
  ingressClassName: nginx # The class name of the Ingress controller in the cluster. This field is used to select the Ingress instance.
  rules:
  - host: vmp-test.com # The custom domain name of the VMP workspace.
    http:
      paths:
      - backend:
          service:
            name: vmp-service # The service name, which must be consistent with the service configuration.
            port:
              number: 80
        path: /
        pathType: Prefix
```



3. After the configuration is complete, click **Services and Ingresses \> Ingress** in the left navigation pane to view the private IP address that corresponds to the Ingress.


<span id=".5q2l6aqk5LqM77ya5Zyo6Ieq5a6a5LmJ6ZuG576k5Lit6YWN572uIEROUw=="></span>
### Step 2: Configure DNS in the custom cluster

To ensure that the collector deployed in the custom cluster can identify the custom domain name, you need to configure CoreDNS in the custom cluster to specify the mapping relationship between the custom domain name and the internal IP address of the Ingress.


1. Use kubectl to connect to the custom cluster.

2. Run the following command to modify the CoreDNS configuration file:


```bash
kubectl edit configmap -n kube-system coredns
```


Add custom hosts in the configuration file, such as `192.168.48.3 vmp-test.com`.

```yaml
Corefile: |
    .:53 {
        errors
        health {
           lameduck 15s
        }
        ready
        
        hosts {
          192.168.48.3 vmp-test.com
          fallthrough
        }

        prometheus :9153
        forward . /etc/resolv.conf {
          prefer_udp
        }
        cache 30
        loop
        reload
        loadbalance
    }
```


<span id=".5q2l6aqk5LiJ77ya5Zyo6Ieq5a6a5LmJ6ZuG576k5Lit6YOo572y6YeH6ZuG5Zmo"></span>
### Step 3: Deploy the collector in the custom cluster

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"> provides two out\-of\-the\-box collection solutions: VMP Agent and VM Agent. This topic uses VM Agent deployment as an example. For details, see <a href="https://docs.byteplus.com/en/docs/vmp/Collection-solution-overview">Collector solution overview</a>.</div>



1. Download the collector deployment script to your local environment. For details, see [Obtaining scripts](https://docs.byteplus.com/en/docs/vmp/Obtaining-a-script).

2. Use kubectl to connect to the custom cluster.

3. Run the following command to deploy the VM Agent collector:


```bash
./install.sh \
--agent vmagent \ # The collector type.
--region cn-beijing \ # The region of the VMP workspace.
--namespace volcano-metrics \ # The namespace where components (such as collectors) are deployed.
--remote-write-url http://vmp-test.com/workspaces/b762e1a3-37***/api/v1/write \ # The Remote Write URL of the VMP workspace. You need to change the domain name to the custom domain name.
--basic-auth-username username-demo \ # The username for Basic Auth in the VMP workspace.
--basic-auth-password password-demo  # The password for Basic Auth in the VMP workspace.
```


<span id=".5qOA5p-l57uT5p6c"></span>
## Check results

<span id=".5p-l55yL57uE5Lu254q25oCB"></span>
### View agent status

After the agent is installed, you can go to the custom cluster page to view the working status of the collector agent. The following table describes the name, type, and feature of each agent.


|Agent Name |Workload Type |Namespace |Description |
|---|---|---|---|
|vmagent |StatefulSet |volcano\-metrics |Collects metrics exposed by kubelet, kubelet\-cadvisor, kube\-state\-metrics, and node\-exporter in the cluster. |
|vm\-operator |Deployment |volcano\-metrics |The controlling agent of VM Agent. |
|kube\-state\-metrics |StatefulSet |volcano\-metrics |Provides the metric data of Kubernetes resources. |
|node\-exporter |DaemonSet |volcano\-metrics |Provides the metric data of node resources. |


<span id=".5p-l55yLIGluZ3Jlc3Mg55uR5o6n"></span>
### View ingress\-nginx monitoring data

The proxy method is used to write monitoring data to the VMP workspace. The write performance is closely related to the performance of the Ingress instance in the VKE cluster. It is recommended that you use the observability feature of the VKE cluster to monitor and perform O&M on the Ingress instance. You can refer to the following topics:


* [ingress-nginx monitoring](https://docs.byteplus.com/en/docs/vke/Ingress-observability)

* [Nginx Ingress best practices](https://docs.byteplus.com/en/docs/vke/Nginx-Ingress-best-practices)

* [Monitoring custom Nginx Ingress controllers](https://docs.byteplus.com/en/docs/vke/Best-practices-for-monitoring-custom-Nginx-Ingress-controllers)


<span id=".55uR5o6n5ZKM5ZGK6K2m"></span>
## Monitoring and alerting

<span id=".5oyH5qCH"></span>
### Metric

You can quickly query and display metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<span id=".5aSn55uY"></span>
### Dashboard

You can build your own Grafana and view metrics and create dashboards through Grafana. It includes:


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id=".5ZGK6K2m"></span>
### Alert

You can configure alerts in the alerting center of VMP. For more details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).

<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ

<span id=".5peg5YWs572R546v5aKD5aaC5L2V5LiL6L295bm26YOo572y6YeH6ZuG5Zmo"></span>
### How do I download and deploy a collector in an environment without a public network?

The collectors provided by VMP are stored in Container Registry (CR) by default. If your custom cluster is deployed in an environment without public networks and cannot access the Internet, you can perform the following steps to download and deploy the collector:


1. Download the related collector image in an environment where you can access the Internet.

2. Upload the image to a private cloud registry.

3. When you deploy the collector, add the fields of the private registry to allow the collector image to be pulled from the private registry.


```bash
./install.sh \
--agent vmagent \ # The collector type.
--region cn-beijing \ # The region of the VMP workspace.
--namespace volcano-metrics \ # The namespace where components (such as collectors) are deployed.
--remote-write-url http://vmp-test.com/workspaces/b762e1a3-37***/api/v1/write \ # The Remote Write URL of the VMP workspace. You need to change the domain name to the custom domain name.
--basic-auth-username username-demo \ # The username for Basic Auth in the VMP workspace.
--basic-auth-password password-demo \ # The password for Basic Auth in the VMP workspace.
--private-registry xxx \ # The private registry address (with the namespace included).
--private-registry-username xxx \ # The username for private registry login.
--private-registry-password yyy # The password for private registry login.
```
