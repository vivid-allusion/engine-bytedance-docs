---
title: "Building cluster observability dashboards by using self-managed Grafana"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cluster-monitoring-practices-and-common-dashboards"
---

Cluster monitoring is an important part of cluster operations and maintenance. You can monitor the usage and status of various resources in clusters to identify and handle exceptions in a timely manner. This ensures normal business operations. This topic describes how to build a cluster dashboard by using a self\-managed Grafana.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The observability feature for the target resources has been enabled in the target cluster. For details, see [Basic observability](https://docs.volcengine.com/docs/6460/1213991?lang=zh).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you upgrade the prometheus\-agent add\-on in the cluster to the latest version. For details, see <a href="https://docs.byteplus.com/en/docs/vke/prometheus-agent-add-on?lang=en">prometheus\-agent</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5pCt5bu6LWdyYWZhbmE="></span>
### Step 1: Deploy Grafana

You can set up a self\-managed Grafana environment in various environments. For example:


* In a VKE cluster, set up Grafana and integrate it with a VMP workspace. For more details, see [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

* In an ECS instance, set up Grafana and integrate it with a VMP workspace. For details, see [Deploying Grafana in an ECS instance and integrating Grafana with a workspace](https://docs.volcengine.com/docs/6731/1545456?lang=zh).

* Set up a self\-managed Grafana environment in another environment and use a public address to integrate it with a VMP workspace. For more information, see [Creating common workspaces](https://docs.volcengine.com/docs/6731/106522?lang=zh).


<span id=".5q2l6aqk5LqM77ya5a-85YWl55uR5o6n5aSn55uY"></span>
### Step 2: Obtain the cluster dashboard


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, click **Custom Dashboard**. Then, click the **Built\-in dashboard** tab to view the list of system preset dashboards.

   The following table lists the correspondence between monitoring dashboards in VKE and preset dashboards in the Observability Platform.

   
   |VKE dashboard category |VKE dashboard name |Dashboard name in the Observability Platform |
   |---|---|---|
   |Cluster monitoring |Cluster monitoring overview |vke\-cluster\-dashboard |
   ||Cluster namespace monitoring |vke\-namespace\-dashboard |
   |Core add\-on monitoring |kube\-apiserver monitoring |vke\-apiserver\-dashboard |
   ||etcd monitoring |vke\-etcd\-dashboard |
   ||kube\-scheduler monitoring |vke\-scheduler\-dashboard |
   ||cluster\-autoscaler monitoring |vke\-ca\-dashboard |
   ||kube\-controller\-manager monitoring |vke\-kcm\-dashboard |
   ||Metrics\-server monitoring |vke\-metrics\-server\-dashboard |
   |Node monitoring |Overview of nodes |vke\-nodes\-dashboard |
   ||Node details monitoring |vke\-node\-dashboard |
   ||Virtual node monitoring |vci\-virtual\-node\-dashboard |
   |Workload monitoring |Deployment monitoring |vke\-deployment\-dashboard |
   ||StatefulSet monitoring |vke\-statefulset\-dashboard |
   ||DaemonSet monitoring |vke\-daemonset\-dashboard |
   ||Pod monitoring |vke\-pod\-dashboard |
   ||Container monitoring |vke\-container\-dashboard |
   ||Elastic scaling monitoring |vke\-hpa\-dashboard |
   ||Smart scaling monitoring |vke\-katalyst\-dashboard |
   |Network service monitoring |core\-dns monitoring |vke\-core\-dns\-dashboard |
   ||node\-local\-dns monitoring |vke\-local\-dns\-dashboard |
   ||vpc\-cni monitoring |vke\-cni\-dashboard |
   |Storage service monitoring |PVC monitoring |vke\-pvc\-dashboard |
   ||FSX monitoring |vke\-csi\-fsx\-dashboard |
   |GPU monitoring |Cluster\-level GPU monitoring |vke\-cluster\-gpu\-dashboard |
   ||GPU instance\-level monitoring |* When the nvidia\-device\-plugin add\-on version is earlier than v2.0.0, use vke\-instance\-gpu\-dashboard.<br><br>* When the nvidia\-device\-plugin add\-on version is v2.0.0 or later, use vke\-instance\-gpu\-v2\-dashboard.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details about add\-on versions, see <a href="https://docs.volcengine.com/docs/6460/350800?lang=zh">nvidia\-device\-plugin</a>.</div><br> |
   ||Pod\-level GPU monitoring |vke\-pod\-gpu\-dashboard |
   ||Node\-level GPU monitoring |* When the nvidia\-device\-plugin add\-on version is earlier than v2.0.0, use vke\-node\-gpu\-dashboard.<br><br>* When the nvidia\-device\-plugin add\-on version is v2.0.0 or later, use vke\-node\-gpu\-v2\-dashboard.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details about add\-on versions, see <a href="https://docs.volcengine.com/docs/6460/350800?lang=zh">nvidia\-device\-plugin</a>.</div><br> |
   ||User\-level GPU monitoring |vke\-user\-gpu\-dashboard |
   |Image acceleration service monitoring |P2P image acceleration monitoring |vke\-p2p\-dashboard |
   ||Image lazy loading (Nydus) monitoring |vke\-nydus\-dashboard |
   |Resource management monitoring |CPU Burst monitoring |vke\-katalyst\-cpu\-burst\-dashboard |
   ||katalyst monitoring |vke\-katalyst\-dashboard |
   |AIOps |Detection and self\-healing |vke\-aiops\-remediation\-dashboard |
   

3. Click the name of the target dashboard to go to its details page. In the upper‑right corner of the page, click **Export** \> **Grafana JSON** to export the dashboard to your on\-premises computer.

4. Open the exported dashboard file in your local environment and delete the `templating.list[0].current` field. As shown in the deleted part of the following code:

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The <code>templating.list[0].current</code> field stores the cluster ID that was selected when the Grafana JSON was exported. This is leftover content from the original platform and is not applicable in your self‑managed environment. After you remove this parameter, the cluster ID drop\-down list will start with no value selected when you import the dashboard into Grafana. This allows you to manually select a cluster ID from the drop\-down list again.   </div>
   

   ```JSON
     "templating": {
       "list": [
         {
           "id": "3",
           "type": "query",
           "name": "ClusterId",
           "label": "Cluster ID",
           "datasource": {
             "type": "prometheus",
             "uid": "${DS_PROMETHEUS}"
           },
           "query": "kube_node_info",
           "regex": "/.*cluster=\"(.*?)\".*/",
           "includeAll": false,
           "multi": false,
           "current": {
             "selected": true,
             "text": [
               "cd8jut6fm1pqj***"
             ],
             "value": [
               "cd8jut6fm1pqjl***"
             ]
           },
           "definition": "kube_node_info"
         }
       ]
     },
   ```
   

5. After modification is complete, save the file.


<span id="g3Eug3P1"></span>
### Step 3: Import the monitoring dashboard


1. Log in to the self\-managed Grafana environment.

2. In the left navigation bar, click **Dashboards** to go to the dashboard configuration page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26010b1553b69d17e713be94ed6302d3.png) </span>

4. Choose **New** \> **Import** from the dropdown menu to enter the dashboard import page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04f16df98438773c3a7d705e805149e9.png) </span>

5. Click **Upload dashboard JSON file** and select the monitoring dashboard JSON file saved on your local machine.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4bc34e3a1bb61c4f278ca91518f55c46.png) </span>

6. Specify basic information for the monitoring dashboard and select a data source.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_67b9376dba280c41779c6e31240f000c.png) </span>

   
   |Parameter |Description |
   |---|---|
   |Name |(Optional) Modify the name of the monitoring dashboard based on your business requirements. |
   |Folder |(Optional) Select the folder where the dashboard is saved. |
   |prometheus |Select the configured data source. |
   

7. Click **Import** to finish the import. Then you can view the monitoring dashboard.


&nbsp;
