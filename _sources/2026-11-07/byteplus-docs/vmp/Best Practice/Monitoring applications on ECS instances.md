---
title: "Monitoring applications on ECS instances"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Monitoring-applications-in-an-ECS-instance"
---

When you deploy applications on ECS instances, you can integrate them with VMP to monitor the basic resources of ECS instances and your applications. This topic describes how to monitor applications deployed on ECS instances.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

When your applications (such as databases or middleware) are deployed on ECS instances, they may be distributed across one or more VPCs, and each VPC may contain multiple ECS instances. To ensure that applications run as expected, you need to achieve unified observability of these ECS instances, basic add\-ons, and the applications.

Based on the characteristics of the applications themselves, VMP supports the following methods to achieve observability of ECS instances and applications:


* For cloud\-native add\-ons or applications that directly provide metrics ports that meet Prometheus requirements, they can be directly integrated with VMP to achieve metric observability.

* For some traditional applications and middleware that do not provide interfaces for Prometheus monitoring and do not support Prometheus data format. You can deploy corresponding exporters on ECS instances within the VPC, then integrate with VMP to complete service discovery and metric observability.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For the observability method of ECS instance resources themselves, please refer to <a href="https://docs.byteplus.com/en/docs/vmp/ECS-monitoring">Elastic Compute Service Access</a> or <a href="https://docs.byteplus.com/en/docs/vmp/Monitoring-ECS-instances">Monitoring ECS Instances</a>.</div>


* <div data-tips="true" data-tips-type="tip">This article takes RabbitMQ deployed on an ECS instance as an example to introduce how to observe applications deployed on ECS instances. For the method of setting up RabbitMQ on an ECS instance, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Building-RabbitMQ">Setting Up RabbitMQ</a>.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* VMP and ECS must be deployed in the same region.

* An ECS instance is created and bound to a public IP address. For more details, refer to [Using the wizard to buy ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u5a6J5YWo57uE"></span>
### Step One: Configure a security group

To ensure that the hosted collector can correctly collect the monitoring data of the ECS instance, you need to first configure a security group for metric collection. Procedure:


1. Log in to the [VPC console](https://console.byteplus.com/vpc).  

2. Click **Security Group** in the left navigation pane.

3. Click **Create Security Group** in the security group list and configure the security group for the hosted collector. The security group will be bound to the Elastic Network Interface (ENI) of the pod for the hosted collector during the configuration of an integration task, which allows the hosted collector to access the specified target IP address ranges and ports.

   * Click the **VPC** drop\-down menu and select the VPC of the user.

   * In the **Access Rules** section, click the **Outbound** tab and click **Add Rule**. Then, configure the security rules for the hosted collector. Among which, the destination IP address is the subnet where the collection target is located, e.g., `172.16.0.0/12`, and the port number is TCP protocol `9419` port.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cf9ba92bf2dc41dbe6d57608a06dc277.png) </span>

4. Configure the security group used by the ECS instance. This topic uses the **Default** security group as an example. In **Inbound** rules, add a rule to allow traffic on the metric collection port. Among which, the source address will use the security group configured for the collector in the article, and the port type will be TCP `9419` port.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c574accab6ec8ced842da44214729ce4.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also create a new security group and add both the hosted collector and the ECS instance to the new security group. In this case, you do not need to configure new access rules. The default outbound and inbound rules in the new security group allow mutual access between the hosted collector and the ECS instance.   </div>
   

<span id=".5q2l6aqk5LqM77ya5ZyoIEVDUyDlrp7kvovkuK3pg6jnvbIgcmFiYml0bXFfZXhwb3J0ZXI="></span>
### Step Two: Deploy rabbitmq_exporter on the ECS instance

To ensure that the hosted collector can correctly collect the RabbitMQ metrics in the ECS instance, you need to install rabbitmq_exporter on the ECS instance.


1. Log in to the ECS instance. For details, please refer to [Log in to the Instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. run the following command to download rabbitmq_exporter.


```bash
wget https://github.com/kbudde/rabbitmq_exporter/releases/download/v1.0.0-RC19/rabbitmq_exporter_1.0.0-RC19_linux_amd64.tar.gz
```



3. run the following command to unzip the rabbitmq_exporter installation package.


```bash
tar -zxvf rabbitmq_exporter_1.0.0-RC19_linux_amd64.tar.gz
```



4. Create the configuration file `config.example.json` for rabbitmq_exporter on the ECS instance and complete the configuration.


```bash
sudo vi config.example.json
```


The content in the configuration file is as follows:

```JSON
{
    "rabbit_url": "http://127.0.0.1:15672",
    "rabbit_user": "guest",
    "rabbit_pass": "guest",
    "publish_port": "9419",
    "publish_addr": "",
    "output_format": "TTY",
    "ca_file": "ca.pem",
    "cert_file": "client-cert.pem",
    "key_file": "client-key.pem",
    "insecure_skip_verify": false,
    "exlude_metrics": [],
    "include_exchanges": ".*",
    "skip_exchanges": "^$",
    "include_queues": ".*",
    "skip_queues": "^$",
    "skip_vhost": "^$",
    "include_vhost": ".*",
    "rabbit_capabilities": "no_sort,bert",
    "aliveness_vhost": "/",
    "enabled_exporters": [
            "exchange",
            "node",
            "overview",
            "queue",
            "aliveness"
    ],
    "timeout": 30,
    "max_queues": 0
}
```


The parameters that need to be focused on and modified are shown in the table below.


|Parameters |Description |
|---|---|
|rabbit_url |IP address and port number of the ECS instance where RabbitMQ is located. As RabbitMQ and rabbitmq_exporter are deployed on the same ECS instance in this example, it is configured as `http://127.0.0.1:15672`. |
|rabbit_user |The username for RabbitMQ log in. This user needs to have `administrator` or `monitoring` permission. For configuration methods, please refer to [Setting up RabbitMQ](https://docs.byteplus.com/en/docs/ecs/Building-RabbitMQ). |
|rabbit_pass |RabbitMQ login password. |
|publish_port |RabbitMQ metric exposure port number is default `9419`. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more configuration parameters of rabbitmq_exporter, please refer to the <a href="https://github.com/kbudde/rabbitmq_exporter">Official Document</a>.</div>



5. Execute the following command to start rabbitmq_exporter.


```bash
./rabbitmq_exporter -config-file config.example.json &
```


The expected feedback result is as follows, indicating that rabbitmq_exporter can correctly collect metrics.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b286a16abafde4508c809e366134db0b.png) </span>

6. Execute the following command on the ECS instance to confirm that rabbitmq_exporter is working properly and to view the monitoring data.

```bash
curl 127.0.0.1:9419/metrics
```


The expected feedback result is as follows, and monitoring information can be viewed normally, indicating that rabbitmq_exporter is working properly.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d6ace798b7e032872787905e36852d7a.png) </span>

<span id=".5q2l6aqk5LiJ77ya6YWN572u6ZuG5oiQ5Lu75Yqh"></span>
### Step Three: Configure an integration task


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation pane, click **Integration Center** \> **Component**. On the page that appears, click **ECS custom collection**.

4. In the **Create ECS access task** panel, click **Create access task**.



&nbsp;

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7273a56105ab31b778aaca38eabb2283.png) </span>

5. (Optional) Service authorization.

   1. When you configure an ECS integration task for the first time, you need to grant permissions to allow VMP to access ECS and VPC. Click **Authorize** to configure service authorization.

   2. Click **Authorize Now** to authorize VMP to access other services.

6. Specify the details of the integration task.



&nbsp;


|Parameter |Description |
|---|---|
|Task name |Configure the name of the integration task. It can contain Chinese characters, letters (uppercase and lowercase), digits, and underscores (`_`), and must be 1 to 40 characters in length. |
|workspace |Select a created VMP workspace. |
|ECS VPC |Select the VPC where the ECS instance is located. |
|Security group |Select the security group for the hosted collector to use, which allows the hosted collector to access resources in the VPC of the user. Multiple options can be selected.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To ensure that the hosted collector can properly collect the metrics of the ECS instance, add the target CIDR block and port to the outbound access rules of the selected security groups.</div><br> |
|Subnet |Select a VPC subnet for service discovery. The system performs ECS service discovery in the selected subnet and monitors all ECS instances that meet requirements. Multiple options can be selected. |


   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the integration task is configured, the system automatically creates an elastic network interface (ENI) in the target VPC to connect the collector with the VPC. The system binds this ENI to the subnet and security group specified in the preceding configuration. You can go to the <strong>Network Interface</strong> page in the <a href="https://console.byteplus.com/vpc/region:vpc+cn-beijing/port">VPC console</a> to view the ENI whose name starts with catena_vmagent. For more information about ENIs, see <a href="https://docs.byteplus.com/en/docs/vpc/Network-interface-overview">Network interface overview</a>.   </div>
   

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
  - port: 9419
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For more parameter descriptions, refer to <a href="https://docs.byteplus.com/en/docs/vmp/ECS-monitoring">ECS integration</a>.</div>


* <div data-tips="true" data-tips-type="tip">The Job configurations will take effect about one minute after modification and deployment. Please wait patiently.</div>


8. Click **Confirm** to complete the configuration.


<span id=".5p-l55yL57uT5p6c"></span>
## View results

After the configuration is complete, you can view the status and details of the task. Check whether the target ECS instance is integrated with VMP properly.


1. Click **Integration Task** in the left navigation pane. Then, click the **Managed environment** tab.

2. Click the name of the target task to view task details.


<span id=".5p-l55yL5L-h5oGv"></span>
## View Information

<span id=".5oyH5qCH"></span>
### Metric

You can quickly query and display metric data by using the Explore feature of VMP. For more details, please refer to [Query Metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For common metrics of RabbitMQ, refer to the <a href="https://github.com/kbudde/rabbitmq_exporter">official document</a>.</div>


<span id=".5aSn55uY"></span>
### Dashboard

You can build your own Grafana and view RabbitMQ metrics and create dashboards through Grafana. It includes:


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id=".5ZGK6K2m"></span>
### Alert

You can configure relevant alerts for RabbitMQ in the Alert Center of VMP. For details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).
