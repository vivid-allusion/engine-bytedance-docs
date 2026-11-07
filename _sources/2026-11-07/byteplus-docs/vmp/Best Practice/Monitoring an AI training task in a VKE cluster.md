---
title: "Monitoring an AI training task in a VKE cluster"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Monitoring-Artificial-Intelligence-training-jobs-in-Vital-Kubernetes-Engine"
---

It is crucial to monitor training task status and underlying resource loads when you use AI training models to process business use cases. This topic describes how to monitor an AI training task in a Vital Kubernetes Engine (VKE) cluster.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Vital Kubernetes Engine (VKE)

   * The cloud native observability feature is enabled, and the node\-exporter agent is installed. For more details, refer to [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The prometheus\-agent add\-on needs to be upgraded to v2.0.5 or later. For more details, refer to <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading an add\-on</a>.      </div>
      

   * The rdma\-device\-plugin agent is installed. For more details, refer to [Installing an add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

   * The nvidia\-device\-plugin agent is installed, and dcgm\-exporter is also installed. For more details, refer to [Installing an add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.bnZpZGlhLWRldmljZS1wbHVnaW4t57uE5Lu2).

* Vital Managed Service for Prometheus

   * A workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

   * An alert notification policy has been created. For more details, see [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules).

   * An alert aggregation policy has been created. For details, see [Creating alert aggregation policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572uIEFJIOiuree7g-S7u-WKoQ=="></span>
### Step 1: Configure an AI training task

You can deploy an AI training task in the cluster and use GPU and RDMA resources by using workloads. For configuration methods, refer to [NVIDIA GPU scheduling](https://docs.byteplus.com/en/docs/vke/NVIDIA-GPU-scheduling) and [Using RDMA resources in VKE clusters](https://docs.byteplus.com/en/docs/vke/Using-RDMA-resources-in-VKE-clusters).

To view information related to the training task on the dashboard, you need to add the `ai.vke.volcengine.com/task`, `ai.vke.volcengine.com/job`, `ai.vke.volcengine.com/team`, and `ai.vke.volcengine.com/user` labels to the training task. The following section shows an example.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ai-demo # The name of the training task.
  namespace: default # The namespace where the training task is located.
spec: 
  replicas: 1 # The number of replicas for the training task.
  selector: 
    matchLabels: 
      app: ai-demo
  template: 
    metadata: 
      labels: 
        app: ai-demo
        ai.vke.volcengine.com/task: master # The role of the training task, such as master, chief, and worker.
        ai.vke.volcengine.com/job: ai-name # The name of the training task.
        ai.vke.volcengine.com/team: team-a # The team to which the training task belongs.
        ai.vke.volcengine.com/user: user-a # The member of the training task.
    spec:
      containers:
      - name: ai # The container name.
        image: doc-cn-beijing.cr.volces.com/vke/gpu-burn:1.0 # The image and version of the training task.
        command: [ "/bin/bash", "-c", "--" ]
        args: [ "while true; do sleep 3600; done;" ]
        resources:
          limits:
            nvidia.com/gpu: "1" # Specify the number of GPUs based on your business requirements.
```


<span id=".5q2l6aqk5LqM77ya5pCt5bu6IEdyYWZhbmEg5bm25a-85YWl55uR5o6n5aSn55uY"></span>
### Step 2: Install Grafana and import a monitoring dashboard

When you need to monitor running AI training tasks and underlying resources in the cluster, you can download a monitoring dashboard provided in this topic and import it into the Grafana system for use.

Procedure:


1. Deploy Grafana in a VKE cluster and integrate Grafana with a workspace. For more details, see [Deploying Grafana and connecting to a workspace in the VKE cluster](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

2. In the local environment, use kubectl to connect to the cluster and run the following command to configure port mapping for the Grafana service:


```bash
kubectl port-forward service/grafana 3000:3000 -n volcano-metrics
```



3. Open a browser in your local environment, paste **localhost:3000** into the address bar, and then press Enter to go to the Grafana login page. Log in to Grafana by using the default username `admin` and password `admin`.

4. Click **Dashboards** in the left navigation pane to go to the monitoring dashboard configuration page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26010b1553b69d17e713be94ed6302d3.png) </span>

5. Click **New** \> **Import** to go to the dashboard importing page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04f16df98438773c3a7d705e805149e9.png) </span>

6. Click **Upload JSON file** and select the on\-premises JSON file of the monitoring dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4b22e34776b472b1c300abb6d421d552.png) </span>

7. Specify the basic information about the monitoring dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a00248d8611cf338c30114cebb95db1.png) </span>

   
   |Parameter |Description |
   |---|---|
   |Name |(Optional) Modify the name of the monitoring dashboard based on your business requirements. |
   |Folder |(Optional) Select the folder where the dashboard is saved. If you do not modify the value, the dashboard is saved in the General folder by default. |
   |VMP |Select a data source. You need to select a VMP workspace that is bound to the target cluster from the drop\-down list. |
   

8. Click **import** to import the monitoring dashboard. Then, you can view the monitoring dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fca5d70796a3ab13f78911b8a6550a7d.png) </span>


<span id=".5q2l6aqk5LiJ77ya5byA5ZCvIEFJIOi1hOa6kOingua1iw=="></span>
### Step 3: Enable the AI resource observability feature


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. Click **Cluster** in the left navigation pane.

3. On the cluster list page, click the cluster for which you want to view events.

4. On the details page of the cluster, click **Configuration** in the left navigation pane.

5. Find the **AI resources** section and click **Enable** to enable AI resource observability.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dd7e992f50e54f96dc02219415bdafe2.png) </span>

6. The system automatically checks the prerequisites for enabling cluster observability, including the workspace configuration and add\-on status.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5389793cb4bdff3ee5e76c0abc871da6.png) </span>

7. Click **Enable** to enable AI resource observability.


<span id=".5q2l6aqk5Zub77ya6YWN572u5ZGK6K2m"></span>
### Step 4: Configure alerts


1. On the details page of the cluster, click **Configuration** in the left navigation pane.

2. On the Basic observability tab, click the AI tab, find the **AI resources** section, and then click **Edit configuration**. Then, click the **Alert** tab and specify the alert\-related parameters.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_47d0755decfe2d1778dfc3e117cc6dd0.png) </span>

   
   |Parameter |Description |
   |---|---|
   |Alert template |Select the required alert templates. You can select multiple templates. |
   |Alert aggregation strategy |Select an alerting aggregation policy from the Aggregation policy list. For more details, see [Creating alert aggregation policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules). |
   |Alert notification policy |Select an alerting notification policy from the Notify policy list. The system will send alerts to the specified contacts based on the alert levels and contact groups configured in the notification policy. For more details, see [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules). |
   

3. Click **Add** to complete the configuration.


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results

<span id=".5p-l55yL55uR5o6n5aSn55uY"></span>
### View the monitoring dashboard


1. In the local environment, use kubectl to connect to the cluster and run the following command to configure port mapping for the Grafana service:


```bash
kubectl port-forward service/grafana 3000:3000 -n volcano-metrics
```



2. Open a browser in your local environment, paste **localhost:3000** into the address bar, and then press Enter to go to the Grafana login page. Log in to Grafana by using the default username `admin` and password `admin`.

3. Click **Dashboards** in the left navigation bar to view the monitoring dashboard of the AI training task.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fca5d70796a3ab13f78911b8a6550a7d.png) </span>


<span id=".5p-l55yL5ZGK6K2m6YWN572u"></span>
### View alert configuration


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).  the 

2. In the left navigation bar, click **Alert center \> Alert rule**. Click the **Alert rule group** tab. In the alert rule group list, view the generated alert rule group.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_997329fe233f44025c1f8dc85ea08e20.png) </span>

3. Click the name of the alert rule group to go to the details page of the alert rule group. Click the **List of alert rules** tab to view all alert rules in the alert rules group. You can enable, disable, or edit the corresponding alert rule based on your business requirements. For specific operations, see [Managing alert rules](https://docs.byteplus.com/en/docs/vmp/Managing-alerting-rules) and [Managing alert rule groups](https://docs.byteplus.com/en/docs/vmp/Managing-alerting-rule-groups).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bd4328754f6bbe1815c90a9764d01c72.png) </span>


<span id=".QUkg5bi455So55uR5o6n5aSn55uY"></span>
## Common AI monitoring dashboards

<span id=".6ZuG576kIEFJIOebkeaOp-Wkp-ebmA=="></span>
### Cluster AI monitoring dashboard

This dashboard mainly displays **cluster\-level** information about AI training tasks and resource usage.


|Information category |Description |
|---|---|
|Cluster training task overview |Displays information about cluster AI training tasks, including the number of AI training tasks, the number of GPU workers, and the GPU utilization of training tasks. |
|Cluster GPU resource overview |Displays the information about cluster GPU resources, such as total number of GPUs, allocated GPUs, used GPUs, faulty GPUs, and the number of GPU nodes. |
|Resource usage details |Displays information about cluster resource usage, such as the number of training tasks, the number of GPU workers, the GPU utilization of training tasks, cluster GPU utilization, and cluster GPU failure rate. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1da9d560f53d5ed59be88d187251e9f1.json" name="Cluster AI Monitoring Dashboard-20230912.json">Cluster AI Monitoring Dashboard-20230912.json</Attachment>


<span id=".6IqC54K5IEdQVSDlpKfnm5g="></span>
### Node GPU dashboard

This dashboard mainly displays **node\-level** monitoring information, including monitoring information about GPU nodes and GPU devices.


|Information Category |Description |
|---|---|
|Node resource usage |Displays the monitoring information about GPU nodes, such as node IP address, GPU model, node status, CPU cores, memory, and number of GPUs. |
|Node resource usage details |Displays the monitoring information of GPUs, such as GPU utilization, GPU video memory usage, GPU XID errors, GPU encoder utilization, GPU clock frequency, and GPU power consumption. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_94d2e9c02fa62a22288267e447880380.json" name="Node GPU Dashboard-20230912.json">Node GPU Dashboard-20230912.json</Attachment>


<span id=".6K6t57uD5Lu75Yqh5aSn55uYKHJkbWEtZGV2aWNlLXBsdWdpbik="></span>
### Training task dashboard (rdma\-device\-plugin)

This dashboard displays **task\-level** monitoring information about AI training tasks and basic resources, including GPU and RDMA.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The data on the dashboard comes from the rdma\-device\-plugin agent. For more details, refer to <a href="https://docs.byteplus.com/en/docs/vke/AI-resource-observability">AI resource observability</a>.</div>



|Information Category |Description |
|---|---|
|Training task overview |Displays the overview of training tasks, including training tasks, training task workers, training tasks with low GPU utilization, and training task workers with low GPU utilization. |
|Training task None Worker list |Displays the None Worker list of the training task. |
|GPU |Displays the monitoring information of GPUs such as GPU utilization, GPU XID errors, GPU video memory usage, GPU temperature, and GPU power consumption. |
|RDMA |Displays the monitoring information of RDMA, such as inbound traffic, outbound traffic, number of inbound packets, number of outbound packets, inbound pause duration, and outbound pause duration. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9ec36ad5f9794591be6032e85a418360.json" name="Training Task Dashboard (rdma-device-plugin)-20230920.json">Training Task Dashboard (rdma-device-plugin)-20230920.json</Attachment>


<span id=".6K6t57uD5Lu75Yqh5aSn55uYKG5vZGUtZXhwb3J0ZXIp"></span>
### Training task dashboard (node\-exporter)

This dashboard displays **task\-level** monitoring information about AI training tasks and basic resources, including GPU and RDMA.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The data on the dashboard comes from the node\-exporter agent. For more details, refer to the <a href="https://github.com/prometheus/node_exporter/blob/master/collector/infiniband_linux.go">official documentation of node\-exporter</a>.</div>



|Information category |Description |
|---|---|
|Training task overview |Displays the overview of training tasks, including training tasks, training task workers, training tasks with low GPU utilization, and training task workers with low GPU utilization. |
|Training task None Worker list |Displays the None Worker list of the training task. |
|GPU |Displays the monitoring information of GPUs such as GPU utilization, GPU XID errors, GPU video memory usage, GPU temperature, and GPU power consumption. |
|RDMA |Displays the monitoring information of RDMA, such as inbound traffic, outbound traffic, inbound packets, outbound packets, link down, and error recovery. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aeee689b5950fcb7f4b2e5e6b107cd97.json" name="Training Task Dashboard (node-exporter)-20230912.json">Training Task Dashboard (node-exporter)-20230912.json</Attachment>
