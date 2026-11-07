---
title: "Monitoring AI training jobs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Monitoring-AI-training-Jobs"
---

When you use AI training models to handle business use cases, monitoring the status of training jobs and the load of underlying resources is crucial, as it directly affects the effectiveness of training jobs. This topic provides commonly used monitoring dashboards for AI training and explains how to import these dashboards into the Grafana system for use.

<span id=".5L2_55So6K-05piO"></span>
## Notes

[Limits](https://docs.byteplus.com/en/docs/vke/Limits), you must strictly follow the procedures (or the recommended resources) in this document. If you need to modify the procedures to suit your service requirements, contact the customer manager for consultation.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cluster has cloud native observability enabled and has the node\-exporter add\-on installed. For more information, see [Enabling cloud native observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Prometheus\-agent add\-on has been upgraded to version v2.0.5 or later. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.   </div>
   

* The rdma\-device\-plugin add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* The nvidia\-device\-plugin and dcgm\-exporter add\-ons have been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.bnZpZGlhLWRldmljZS1wbHVnaW4t57uE5Lu2).

* The VMP workspace associated with the cluster has been connected to your self\-hosted Grafana service. Grafana must be version v9.0.2 or later. For details, see [Integrating data from VMP into self-managed Grafana](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).


<span id=".6YWN572uLWFpLeiuree7g-S7u-WKoQ=="></span>
## Configuring AI training jobs

You can deploy AI training jobs in a cluster using workloads and utilize GPU and RDMA resources in the cluster. For details, refer to [NVIDIA GPU scheduling](https://docs.byteplus.com/en/docs/vke/NVIDIA-GPU-scheduling) and [Using RDMA resources in VKE clusters](https://docs.byteplus.com/en/docs/vke/Using-RDMA-resources-in-VKE-clusters).

To include the monitoring information about training jobs in the dashboard, you need to add the following labels to the training jobs: `ai.vke.volcengine.com/task`, `ai.vke.volcengine.com/job`, `ai.vke.volcengine.com/team`, and `ai.vke.volcengine.com/user`.

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ai-demo # The name of the training job.
  namespace: default # The namespace of the training job.
spec: 
  replicas: 1 # Number of replicas for the training job.
  selector: 
    matchLabels: 
      app: ai-demo
  template: 
    metadata: 
      labels: 
        app: ai-demo
        ai.vke.volcengine.com/task: master # The role of the training job, such as master, chief, or worker.
        ai.vke.volcengine.com/job: ai-name # The name of the training job.
        ai.vke.volcengine.com/team: team-a # Team to which the training job belongs.
        ai.vke.volcengine.com/user: user-a # Member to which the training job belongs.
    spec:
      containers:
      - name: ai # The container name.
        image: doc-cn-beijing.cr.volces.com/vke/gpu-burn:1.0 # The image and version of the training job.
        command: [ "/bin/bash", "-c", "--" ]
        args: [ "while true; do sleep 3600; done;" ]
        resources:
          limits:
            nvidia.com/gpu: "1" # Number of GPU cards.
```


<span id=".55uR5o6n5aSn55uY"></span>
## Monitoring dashboards

<span id=".6aKE572u55uR5o6n5aSn55uY"></span>
### Preset  monitoring dashboards

You can view the preset monitoring dashboards for AI training jobs by going to **Cloud native observability** \> **Monitoring center** \> **Dashboard**. For details, see [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability).

<span id=".5a-85YWl55uR5o6n5aSn55uY"></span>
### Importing monitoring dashboards

To monitor AI training jobs that run in the cluster and the underlying resources, you can download the monitoring dashboards provided below and import them into the Grafana system. To do so, follow the steps below:


1. Log in to the Grafana system using your account and password.

2. In the left navigation bar, select **Dashboards** to enter the dashboard configuration page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26010b1553b69d17e713be94ed6302d3.png) </span>

3. Choose **New** \> **Import** from the dropdown menu to enter the dashboard import page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04f16df98438773c3a7d705e805149e9.png) </span>

4. Click **Upload JSON file** and select the monitoring dashboard JSON file saved on your local machine.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4b22e34776b472b1c300abb6d421d552.png) </span>

5. Set basic information for the monitoring dashboard.

   
   |Parameter |Description |
   |---|---|
   |Name |(Optional) Modify the dashboard name as needed. |
   |Folder |(Optional) Select the folder where you want to save the dashboard. If you do not change the folder, it will be saved in the General folder by default. |
   |VMP |From the drop\-down menu, select the VMP workspace associated with the target cluster as the data source. |
   

6. Click **Import** to finish the import. Then you can view the monitoring dashboard.


<span id=".55uR5o6n5aSn55uY6K-05piO"></span>
## Monitoring dashboard details

<span id=".6ZuG576kLWFpLeebkeaOp-Wkp-ebmA=="></span>
### Cluster AI monitoring dashboard

This dashboard displays information about AI training jobs and resource usage at the **cluster level**.


|Information category |Description |
|---|---|
|Cluster\-level training job overview |Displays information about AI training jobs in the cluster, including the number of AI training jobs, number of GPU workers, and GPU utilization by training jobs. |
|Cluster\-level GPU resource overview |Displays GPU statistics, such as the total number of GPUs, number of allocated GPUs, number of used GPUs, number of faulty GPUs, and number of GPU nodes. |
|Resource usage details |Displays cluster resource usage, such as the number of training jobs, number of GPU workers, training job GPU utilization, cluster\-level GPU usage, and cluster\-level GPU failure rate. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_31f1393109455683219b97b505375483.json" name="Cluster AI monitoring dashboard-20250925.json">Cluster AI monitoring dashboard-20250925.json</Attachment>


<span id=".6IqC54K5LWdwdS3lpKfnm5g="></span>
### Node GPU dashboard

This dashboard displays monitoring information at the **node level**, including GPU node information and GPU card information.


|Information category |Description |
|---|---|
|Node resource usage |Displays GPU node information, such as node IP addresses, GPU model, node status, CPU cores, memory, and number of GPUs. |
|Node\-level resource usage details |Displays GPU card information, including GPU utilization, GPU memory usage, abnormal GPU Xid errors, GPU encoder utilization, GPU clock frequency, and GPU power consumption. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_94d2e9c02fa62a22288267e447880380.json" name="Node GPU dashboard-20230912.json">Node GPU dashboard-20230912.json</Attachment>


<span id=".6K6t57uD5Lu75Yqh5aSn55uYLXJkbWEtZGV2aWNlLXBsdWdpbg=="></span>
### Training job dashboard (rdma\-device\-plugin)

This dashboard displays monitoring information about AI training jobs and basic resources (GPU and RDMA) at the **job level**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The data on this dashboard comes from the rdma\-device\-plugin add\-on. For details, refer to <a href="https://docs.byteplus.com/en/docs/vke/AI-resource-observability">AI resource observability</a>.</div>



|Information category |Description |
|---|---|
|Training job overview |Displays training job overview, including training jobs, training job workers, training jobs with low GPU utilization, and training job workers with low GPU utilization. |
|Training jobs with no workers assigned |Displays a list of training jobs with no worker assigned. |
|GPU |Displays GPU monitoring information, such as GPU utilization, GPU Xid errors, GPU memory usage, GPU temperature, and GPU power consumption. |
|RDMA |Displays RDMA monitoring information, such as inbound traffic, outbound traffic, number of inbound packets, number of outbound packets, inbound pause duration, and outbound pause duration. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9ec36ad5f9794591be6032e85a418360.json" name="Training job dashboard (rdma-device-plugin)-20230920.json">Training job dashboard (rdma-device-plugin)-20230920.json</Attachment>


<span id=".6K6t57uD5Lu75Yqh5aSn55uYLW5vZGUtZXhwb3J0ZXI="></span>
### Training job dashboard (node\-exporter)

This dashboard displays monitoring information about AI training jobs and basic resources (GPU and RDMA) at the **job level**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The data on this dashboard comes from the node\-exporter add\-on. For details, see <a href="https://github.com/prometheus/node_exporter/blob/master/collector/infiniband_linux.go">node\-exporter documentation</a>.</div>



|Information category |Description |
|---|---|
|Training job overview |Displays training job overview, including training jobs, training job workers, training jobs with low GPU utilization, and training job workers with low GPU utilization. |
|Training jobs with no workers assigned |Displays a list of training jobs with no workers assigned. |
|GPU |Displays GPU monitoring information, such as GPU utilization, GPU Xid errors, GPU memory usage, GPU temperature, and GPU power consumption. |
|RDMA |Displays RDMA monitoring information, such as inbound traffic, outbound traffic, inbound packets, outbound packets, link down, and error recovery. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aeee689b5950fcb7f4b2e5e6b107cd97.json" name="Training job dashboard (node-exporter)-20230912.json">Training job dashboard (node-exporter)-20230912.json</Attachment>


<span id=".5Zui6Zif6K6t57uD5Lu75Yqh5aSn55uY"></span>
### Team training job dashboard

This dashboard displays monitoring information about AI training jobs at the **team level**.


|Information category |Description |
|---|---|
|Overview of training jobs for the team |Displays AI training information at the team level. This information includes the number of training jobs, number of GPU workers, GPU utilization by the training jobs, and abnormal training jobs. |
|Overview of training jobs for team members |Displays AI training information at the team member level. This information includes the number of training jobs, number of GPU workers, GPU utilization by the training jobs, and Xid errors of training jobs at the granularity of team members. |
|Training job list |Displays a list of all AI training jobs for a team. |


<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_216fb0d329e8886195782b6ca35d42ab.json" name="Team training job dashboard-20230912.json">Team training job dashboard-20230912.json</Attachment>
