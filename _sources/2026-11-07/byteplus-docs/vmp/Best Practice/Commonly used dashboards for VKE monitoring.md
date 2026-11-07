---
title: "Commonly used dashboards for VKE monitoring"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Common-dashboards-for-Vital-Kubernetes-Engine-monitoring"
---

Cluster monitoring is an important part of cluster O&M. Monitoring enables you to understand the usage and working status of various resources in the cluster, and be able to identify and handle exceptions in a timely manner to ensure the normal operation of businesses. This topic describes best practices for cluster monitoring and provides commonly used monitoring dashboards for cluster monitoring.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A cluster is integrated with Vital Managed Service for Prometheus (VMP). For more details, refer to [VKE integration](https://docs.byteplus.com/en/docs/vmp/cluster-monitoring).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to upgrade the prometheus\-agent in the cluster to the latest version. For more details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading an add\-on</a> and <a href="https://docs.byteplus.com/en/docs/vke/prometheus-agent">prometheus\-agent</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5pCt5bu6IEdyYWZhbmE="></span>
### Step 1: Install Grafana

You can install Grafana in a cluster and integrate Grafana with a VMP workspace to create a cluster\-oriented visual monitoring platform. For more details, refer to [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you use the monitoring dashboard provided in this topic, the version of Grafana needs to be 9.0.2 or later.</div>


<span id=".5q2l6aqk5LqM77ya5a-85YWl55uR5o6n5aSn55uY"></span>
### Step 2: Import the monitoring dashboard

After you deploy Grafana in the cluster, you can download the monitoring dashboard provided below and import it into the Grafana system for use. Procedure:


1. In the local environment, use kubectl to connect to the cluster and run the following command to configure port mapping for the Grafana service:


```bash
kubectl port-forward service/grafana 3000:3000 -n volcano-metrics
```



2. Open a browser in your local environment, paste **localhost:3000** into the address bar, and then press Enter to go to the Grafana login page. Log in to Grafana by using the default username `admin` and password `admin`.

3. Click **Dashboards** in the left navigation pane to go to the monitoring dashboard configuration page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26010b1553b69d17e713be94ed6302d3.png) </span>

4. Click **New** \> **Import** to go to the dashboard importing page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04f16df98438773c3a7d705e805149e9.png) </span>

5. Click **Upload dashboard JSON file** and select the local JSON file of the monitoring dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4bc34e3a1bb61c4f278ca91518f55c46.png) </span>

6. Specify the basic information about the monitoring dashboard and select a data source.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2158d94e3f5970243a2dab99973d4860.png) </span>

   
   |Parameter |Description |
   |---|---|
   |Name |(Optional) Modify the name of the monitoring dashboard based on your business requirements. |
   |Folder |(Optional) Select the folder where the dashboard is saved. If you do not modify the value, the dashboard is saved in the General folder by default. |
   |VMP |Select a data source. You need to select a VMP workspace that is bound to the target cluster from the drop\-down list. |
   

7. Click **import** to import the monitoring dashboard. Then, you can view the monitoring dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9b038196c4475d19a977f13f578f288.png) </span>


<span id=".5bi455So5aSn55uY"></span>
## Commonly used dashboards

<span id=".QVBJU2VydmVyIOebkeaOp-Wkp-ebmA=="></span>
### ApiServer monitoring dashboard

The dashboard mainly displays the monitoring information of the API server on the cluster control plane.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bd91d6ac7f4f40cc87af0508121d14a5.png) </span>


|Information category |Description |
|---|---|
|Key metrics |Displays the key metrics of the API server in a cluster, such as API QPS, read request success rate, and write request success rate. |
|Overview |Displays the summary information of the API server in a cluster, such as the GET read request latency, LIST read request latency, write request latency, number of read requests being processed, and number of write requests being processed. |
|Resource analysis |Displays the number of resource objects for the API server in a cluster. |
|QPS and latency |Displays the QPS and latency information of the API server in a cluster, such as QPS by verb and read QPS with non\-2xx returned values. |
|Admission controller and webhook |Displays the admission controller and webhook information of the API server in a cluster, such as admission controller latency, admission webhook latency, and admission webhook QPS. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e0fc214212b4c79bcbef86f15cbb223c.json" name="ApiServer-20231201.json">ApiServer-20231201.json</Attachment>


<span id=".RVRDRCDnm5HmjqflpKfnm5g="></span>
### Etcd monitoring dashboard

The dashboard mainly displays the monitoring information of the etcd server on the cluster control plane. The information includes etcd alive status, number of leader changes in the past day, disk size, total number of key\-value pairs, and other information.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_252415abe3374cf7e26d3038163cce57.png) </span>

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5966d917fcdce4064df03d1d3134eec4.json" name="Etcd-20231201.json">Etcd-20231201.json</Attachment>


<span id=".U2NoZWR1bGVyIOebkeaOp-Wkp-ebmA=="></span>
### Scheduler monitoring dashboard

The dashboard mainly displays the monitoring information of the scheduler on the cluster control plane.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9d3089555a2ae5e321614d0fa2407eff.png) </span>


|Information category |Description |
|---|---|
|Overview |Displays the summary information of the cluster scheduler, including scheduler cluster statistics and scheduler pending Pods. |
|Kubernetes API |Displays the API information of the scheduler in a cluster, including Kubernetes API QPS and Kubernetes API request latency. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e5edc4c795087f27bf783b17d83715b1.json" name="Scheduler-20231201.json">Scheduler-20231201.json</Attachment>


<span id=".6ZuG576k5qaC6KeI5aSn55uY"></span>
### Cluster Overview dashboard

The dashboard displays the summary information of a cluster.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_73b481ce37bf1e7c0fafd3c928cf448f.png) </span>


|Information category |Description |
|---|---|
|Node overview |Displays the summary information of nodes in a cluster, such as the total number of nodes, average memory utilization of nodes, average CPU utilization of nodes, top 10 memory utilization of nodes, and top 10 CPU utilization of nodes. |
|Namespace overview |Displays the summary information of the namespaces in a cluster, such as the namespace list, and the number of various workloads in each namespace. |
|Container overview |Displays the summary information of nodes in a cluster, such as the total number of Pods, top 10 container memory utilization, top 10 container CPU utilization, and container network overview. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c1ecfe197fab51da6ce362ff412e9311.json" name="Cluster Overview-20231201.json">Cluster Overview-20231201.json</Attachment>


<span id=".5ZG95ZCN56m66Ze05qaC6KeI5aSn55uY"></span>
### Namespace overview dashboard

The dashboard displays cluster overview information at the namespace level.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6e2ec9c4df2477096a53d21d822d2641.png) </span>


|Information category |Description |
|---|---|
|Resource quantity |Displays the quantity of various resources in the namespace, such as Pods, containers, and workloads. |
|Resource utilization |Displays resource utilization in the namespace, such as CPU utilization and memory utilization. |
|Abnormal resources |Displays the number of abnormal resources that need to be concerned about in a namespace, such as workloads in the NotReady state and PersistentVolumeClaims (PVCs) that are not mounted. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dd9b85ee3b1fd95aedd2cd741bf0f1e7.json" name="Namespace Overview-20231201.json">Namespace Overview-20231201.json</Attachment>


<span id=".6IqC54K55qaC6KeI5aSn55uY"></span>
### Node Overview dashboard

The dashboard displays the summary information of a node.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ebed3678f0a4ef54725b75c4d85340ca.png) </span>


|Information category |Description |
|---|---|
|Node overview |Displays the summary information of a node, such as the run time, total memory, total CPU, total Pods, and Pod list. |
|Node resource |Displays the summary information of a node, such as node CPU utilization, node memory utilization, node disk read/write IOPs, node network, and node TCP connections. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ef91f00a6642932900c67fa9dd66e5b4.json" name="Node Overview-20231201.json">Node Overview-20231201.json</Attachment>


<span id=".6IqC54K5IFRvcE4g5aSn55uY"></span>
### Node TopN dashboard

The dashboard displays the top N information of the node, such as the top 5 memory usage, top 5 CPU usage, top 5 inbound and outbound traffic, and top 5 disk usage.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_532633a5e40c4f48a77e9efb1b2a3dcf.png) </span>

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e2731a3263ff6dc60f5cf15d12b29824.json" name="Node TopN-20231201.json">Node TopN-20231201.json</Attachment>


<span id=".6ZuG576kIERlcGxveW1lbnQg55uR5o6n5aSn55uY"></span>
### Kubernetes Deployment monitoring dashboard

The dashboard displays the monitoring information about the Deployment workload of the cluster. You can filter and view the monitoring details of the specified workload by namespace and workload name.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fce1a6ca6ea98f292c79a385c593b527.png) </span>


|Information category |Description |
|---|---|
|Overview information |Displays the overview information about the workload, such as the namespace, number of Pods, and status. |
|Resource information |Displays the resource usage information of a workload. such as memory utilization, CPU utilization, network IO, and disk IO. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_064f9c6da1f78e310734eb43ba9d6bb0.json" name="Kubernetes Deployment-20231201.json">Kubernetes Deployment-20231201.json</Attachment>


<span id=".6ZuG576kIFN0YXRlZnVsU2V0IOebkeaOp-Wkp-ebmA=="></span>
### Kubermetes StatefulSet monitoring dashboard

The dashboard displays the monitoring information about the StatefulSet workload of the cluster. You can filter and view the monitoring details of the specified workload by namespace and workload name.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4f84406032c82316f095e9aa59df10cd.png) </span>


|Information Category |Description |
|---|---|
|Overview information |Displays the overview information about the workload, such as the namespace, number of Pods, and status. |
|Resource information |Displays the resource usage information of a workload. such as memory utilization, CPU utilization, network IO, and disk IO. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b2782d14d150b6a14b518ea18db38221.json" name="Kubernetes StatefulSet-20231201.json">Kubernetes StatefulSet-20231201.json</Attachment>


<span id=".6ZuG576kIERhZW1vbnNldCDnm5HmjqflpKfnm5g="></span>
### Daemonset monitoring dashboard

The dashboard displays the monitoring information about the DaemonSet of the cluster, such as the number of Pods, CPU usage, memory usage, and network IO.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a2129b5138bd072c86fa91db3c275468.png) </span>

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_57646365965f01a275775e3e0909b9a6.json" name="Kubernetes Daemonset-20231201.json">Kubernetes Daemonset-20231201.json</Attachment>


<span id=".6ZuG576kIFdvcmtsb2FkIOebkeaOp-Wkp-ebmA=="></span>
### Workload monitoring dashboard

This dashboard displays the summary information of Deployments and Pods in a cluster.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eabaef6163f2086153a2ce4ca157d69e.png) </span>

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb3f4268e16bf85aa93e16cb630c9e67.json" name="Workload-20231201.json">Workload-20231201.json</Attachment>


<span id=".6ZuG576kIFBvZCDnm5HmjqflpKfnm5g="></span>
### Kubernetes Pod monitoring dashboard

The dashboard displays the monitoring information about the Pod in the cluster. You can filter and view the monitoring details of the specified Pod by namespace and Pod name.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f88321e42ec2d748c52306399b3ff7a1.png) </span>


|Information category |Description |
|---|---|
|Overview information |Displays the overview information about the Pod, such as the namespace, node name, status, CPU requests, and memory requests. |
|Resource information |Displays the resource usage information about the Pod, such as CPU usage, memory usage, CPU utilization, memory utilization, CPU load, and network information. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_579f324b8aeb5208f9b7e06caf0a86b8.json" name="Kubernetes Pod-20231201.json">Kubernetes Pod-20231201.json</Attachment>


<span id=".Q29yZUROUyDnm5HmjqflpKfnm5g="></span>
### CoreDNS monitoring dashboard

The dashboard displays the monitoring information about CoreDNS in the cluster, including the main information about DNS requests and DNS responses in DNS resolution. The information includes QPS, request success rate, response time, response size, DNS cache, and other information.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b4208ee6f2cc60849ba39c4489f183b.png) </span>

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_56cb9b0fd89881f513c6130a9cb6392c.json" name="CoreDNS-20231201.json">CoreDNS-20231201.json</Attachment>
