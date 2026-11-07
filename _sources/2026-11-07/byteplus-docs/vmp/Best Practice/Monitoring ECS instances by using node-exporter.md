---
title: "Monitoring ECS instances by using node-exporter"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Monitoring-ECS-instances"
---

Vital Managed Service for Prometheus (VMP) allows you to monitor Elastic Compute Service (ECS) instances to obtain the metric information of the ECS instances. This topic describes how to monitor ECS instances by using node\-exporter.

<span id="rOqr8kGU"></span>
## Background

node\-exporter ****is an important component in the Prometheus open\-source ecosystem. It collects metrics from Linux server hardware and operating systems, such as CPU, memory, disk, network, and file systems. It provides the metric data as an HTTP service to help Prometheus scrape the data and thus monitor the operational status of Linux servers.

Compared with other monitoring tools, node\-exporter mainly provides the following benefits:


* **Deep integration with the Prometheus ecosystem**: As an official Prometheus component, node\-exporter works seamlessly with Alertmanager and Grafana to form a complete monitoring loop.

* **Lightweight and efficient**: Developed in the Go language, node\-exporter occupies few resources, has a minimal impact on monitored node performance, and applies to large\-scale cluster deployment.

* **Comprehensive and flexible metric collection**: By default, node\-exporter covers system underlying metrics and allows you to add custom metrics by using custom scripts or add\-ons such as the text file collector. This enables node\-exporter to apply to different monitoring scenarios.

* **Active community and rich ecosystem**: Leveraging the large Prometheus community, node\-exporter is updated and maintained in a timely manner, supports node auto\-discovery in cloud\-native environments such as Kubernetes, and adapts to the containerized deployment trend.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* VMP and ECS must be deployed in the same region.

* An ECS instance is created and bound to a public IP address. For more details, refer to [Using the wizard to buy ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5a6J5YWo57uE"></span>
### Step One: Configure a security group


1. Log in to the [VPC console](https://console.byteplus.com/vpc).  

2. Click **Security Group** in the left navigation pane.

3. Click **Create Security Group** in the security group list and configure the security group for the hosted collector. The security group will be bound to the Elastic Network Interface (ENI) of the pod for the hosted collector during the configuration of an integration task, which allows the hosted collector to access the specified target IP address ranges and ports.

   * Click the **VPC** drop\-down menu and select the VPC of the user.

   * In the **Access Rules** section, click the **Outbound** tab and click **Add Rule**. Then, configure the security rules for the hosted collector. Set the Destination parameter to the CIDR block where the collection target is located, such as `172.16.0.0/12`, set the Protocol type parameter to TCP, and set the Port range parameter to `9100`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_039016f251ef26671de7f6ca273f0c71.png) </span>

4. Configure the security group used by the ECS instance. This topic uses the **Default** security group as an example. On the **Inbound Rules** tab, click Add Rule to add a rule to allow traffic on the metric collection port. Set the Source parameter to the security group configured for the collector, set the Protocol type parameter to TCP, and set the Port range parameter to `9100`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5a768f25a271f8c5c53c26aae2454659.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also create a new security group and add both the hosted collector and the ECS instance to the new security group. In this case, you do not need to configure new access rules. The default outbound and inbound rules in the new security group allow mutual access between the hosted collector and the ECS instance.   </div>
   

<span id=".5q2l6aqk5LqM77ya5ZyoIEVDUyDlrp7kvovkuK3pg6jnvbIgbm9kZS1leHBvcnRlcg=="></span>
### Step 2: Deploy node\-exporter in the ECS instance


1. Log in to the [ECS console](https://console.byteplus.com/ecs). 

2. Click **Instance & Image \> Instance** in the left navigation bar to go to the instance list page. Click the name of the target instance to go to the instance details page.

3. Run the following command to download and decompress the file package of node\-exporter:


```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.5.0/node_exporter-1.5.0.linux-amd64.tar.gz && tar -xvf node_exporter-1.5.0.linux-amd64.tar.gz
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6f2ee2c92ebd94c52d8d68461a3ebe3b.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you cannot download the exporter on the ECS instance, you can download the package to your local host and upload it to ECS. For more details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Using-SCP-to-upload-files-from-a-local-Linux-or-MacOS-to-a-Linux-instance">Using SCP to upload files from a local Linux or MacOS to a Linux instance</a>.</div>



4. Go to the decompressed folder and run the following command to start node\-exporter:


```bash
nohup ./node_exporter &
```



5. Run the following command to view the metrics exposed by node\-exporter and check whether it is running as expected:


```bash
curl http://127.0.0.1:9100/metrics
```


The following section shows the expected response result, in which the collected metrics can be viewed.

```bash
# HELP go_gc_duration_seconds A summary of the pause duration of garbage collection cycles.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 0
go_gc_duration_seconds{quantile="0.25"} 0
go_gc_duration_seconds{quantile="0.5"} 0
go_gc_duration_seconds{quantile="0.75"} 0
go_gc_duration_seconds{quantile="1"} 0
go_gc_duration_seconds_sum 0
go_gc_duration_seconds_count 0
# HELP go_goroutines Number of goroutines that currently exist.
# TYPE go_goroutines gauge
go_goroutines 7
# HELP go_info Information about the Go environment.
# TYPE go_info gauge
go_info{version="go1.19.3"} 1
# HELP go_memstats_alloc_bytes Number of bytes allocated and still in use.
# TYPE go_memstats_alloc_bytes gauge
go_memstats_alloc_bytes 2.626832e+06
# HELP go_memstats_alloc_bytes_total Total number of bytes allocated, even if freed.
# TYPE go_memstats_alloc_bytes_total counter
go_memstats_alloc_bytes_total 2.626832e+06
# HELP go_memstats_buck_hash_sys_bytes Number of bytes used by the profiling bucket hash table.
# TYPE go_memstats_buck_hash_sys_bytes gauge
go_memstats_buck_hash_sys_bytes 1.447059e+06
# HELP go_memstats_frees_total Total number of frees.
# TYPE go_memstats_frees_total counter
go_memstats_frees_total 2055
......
```


<span id=".5q2l6aqk5LiJ77ya6YWN572u6ZuG5oiQ5Lu75Yqh"></span>
### Step 3: Configure an integration task


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).  the 

2. In the top navigation bar, select the target region.

3. Click **Access Center \> Component** in the left navigation pane.

4. Click **ECS** to configure the ECS integration task.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_60a2e173370299311699c5dcb3642cbc.png) </span>

5. (Optional) Service authorization.

   1. When you configure an ECS integration task for the first time, you need to grant permissions to allow VMP to access ECS and VPC. Click **Authorize** to configure service authorization.

   2. Click **Authorize Now** to authorize VMP to access other services.

6. Configure the details of the integration task.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e31ed576d0382e7d8b5282c49c369630.png) </span>



&nbsp;


|Parameter |Description |
|---|---|
|Task name |Configure the name of the integration task. It can contain Chinese characters, letters (uppercase and lowercase), digits, and underscores (`_`), and must be 1 to 40 characters in length. |
|workspace |Select a created VMP workspace. |
|ECS VPC |Select the VPC where the ECS instance is located. |
|Security group |Select the security group for the hosted collector to use, which allows the hosted collector to access resources in the VPC of the user. Multiple options can be selected.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To ensure that the hosted collector can collect the metrics of the ECS instance as expected, add the target CIDR block and port to the outbound access rules of the selected security groups.</div><br> |
|Subnet |Select a VPC subnet for service discovery. The system performs ECS service discovery in the selected subnet and monitors all ECS instances that meet requirements. Multiple options can be selected. |


7. Configure the job and specify the collection interval and the port number for service discovery.


```yaml
global:
  scrape_interval: 15s
  scrape_timeout: 10s
scrape_configs:
- job_name: ecs
  scheme: http
  metrics_path: /metrics
  volc_sd_configs:
  - port: 9100
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For more parameter descriptions, refer to <a href="https://docs.byteplus.com/en/docs/vmp/ECS-monitoring">ECS integration</a>.</div>


* <div data-tips="true" data-tips-type="tip">The Job configurations will take effect about one minute after modification and deployment. Please wait patiently.</div>


8. Click **Confirm** to complete the configuration.


<span id=".5p-l55yL57uT5p6c"></span>
## View results

After the configuration is complete, you can view the status and details of the task. Check whether the target ECS instance is integrated with VMP properly.


1. Click **Integration Center** in the left navigation pane and click the **Integration Task** tab.

2. In the task list, find the target task and click **Target List** in the **Actions** column to view the ECS instances that are automatically identified by the system and integrated into VMP.


<span id=".5p-l55yL5L-h5oGv"></span>
## View Information

<span id=".5oyH5qCH"></span>
### Metric

You can quickly query and display metric data by using the Explore feature of VMP. For more details, please refer to [Query Metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For common metrics of RabbitMQ, refer to the <a href="https://github.com/kbudde/rabbitmq_exporter">official document</a>.</div>


<span id=".5aSn55uY"></span>
### Dashboard

You can build your own Grafana and view the metrics of the ECS instance and create dashboards through Grafana. It includes:


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id=".5ZGK6K2m"></span>
### Alert

You can configure alerts for the ECS instance in the alerting center of VMP. For details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).

<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ

<span id=".5aaC5L2V5p-l55yL5LqR5pyN5Yqh5Zmo55qEIDkxMDAg56uv5Y-j5piv5ZCm6KKr5Y2g55So"></span>
### How do I check whether port 9100 of ECS is occupied?

You can run the following command in the ECS console to check whether the port is occupied:

```bash
ss -naltp | grep 9100
```


If the following information is returned, it indicates that port 9100 is already occupied.

```Plain Text
LISTEN     0      128       [::]:9100                  [::]:*                   users:(("node_exporter",pid=1654,fd=3))
```


<span id=".5aaC5L2V5L-u5pS5IG5vZGUtZXhwb3J0ZXIg55qE57y655yB56uv5Y-j"></span>
### How do I modify the default port of node\-exporter?

By default, node\-exporter uses port 9100 to expose metrics. When port 9100 in ECS is occupied, you can modify the `--web.listen-address` parameter to change the metric exposure port of node\-exporter when you start node\-exporter. For example, change the port to port 9200.

```bash
nohup ./node_exporter  --web.listen-address=":9200"&
```
