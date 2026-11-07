---
title: "Custom ECS integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ECS-monitoring"
---

Vital Managed Service for Prometheus supports ECS integration to meet users' unified monitoring needs for cloud basic resources and custom business services. This topic describes the procedure for integrating an ECS instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

ECS serves as a cloud virtual server that is secure, stable, and scalable, and provides resources such as CPU, memory, disk, and network. You can use ECS to create a business environment that is elastic, available, secure, and reliable to effectively reduce IT maintenance costs.

You can monitor basic ECS instance resources or custom applications deployed on ECS instances by integrating them into VMP.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about ECS, refer to the <a href="https://docs.byteplus.com/en/docs/ecs/What-is-Elastic-Compute-Service">documentation of ECS</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* VMP and ECS have been activated.

* A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* An ECS instance is created. For details, see [Creating ECS instances](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances).

   * When monitoring basic ECS resources, please confirm that the monitoring add\-ons (cloud\-monitor\-agent, node\-exporter, etc.) are installed on the ECS instance. For details, see [How do I handle the "Cloud-monitor-agent unable to collect monitoring data" issue on ECS instances?](https://docs.byteplus.com/en/docs/ecs/Resolve-the-issue-of-missing-monitoring-metrics)

   * When monitoring custom business on ECS, please confirm the custom business is deployed, and the metric interface is exposed, or the corresponding exporter is deployed.

* Security groups are configured. For details, please refer to [Creating Security Groups](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

   * Create the security group used by the managed collector, and allow the subnet and port of the ECS instance in the **outbound rule**.

   * Configure the security group to which the ECS belongs, and allow the security group used by the managed collector to access the corresponding port in the **inbound rule**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The VMP workspace and the target ECS instance must be deployed in the same region.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Integration Center \> Component**. On the page that appears, click **Elastic Computing Services custom scraping**.

4. (Optional) Service authorization.

   1. When you configure an ECS integration task for the first time, you need to grant permissions to allow VMP to access ECS and VPC. Click **Authorize** to configure service authorization.

   2. Click **Authorize Now** to authorize VMP to access other services.

5. Configure integration task details.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8a960d599da02641485619f6fb135600.png) </span>

   
   |Parameter |Description |
   |---|---|
   |Task name |Configure the name of the integration task. |
   |workspace |Select a created VMP workspace. |
   |ECS VPC |Select the VPC where the ECS instance is located. |
   |Security group |Select the security group for the hosted collector to use, which allows the hosted collector to access resources in the VPC of the user.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To ensure that the hosted collector can collect the metrics of the ECS instance as expected, add the target CIDR block and port of the ECS instance to the outbound access rules of the selected security groups.</div><br> |
   |Subnet |Select one or more subnets. This setting is mainly for connecting networks. This setting can be used together with **Filtering ECS objects by subnet** to specify a granular ECS scope for metric collection. |
   |Filtering ECS objects by subnet |Specify the ECS scope for metric collection.<br><br><br>* **Disable**: (default) Do not use subnet filtering. The system will perform ECS service discovery within the selected VPC, and collect metrics from all ECS instances within all subnets in the VPC.<br><br>* **Enable**: Use subnet filtering. The system will perform ECS service discovery within the specified subnet of the VPC and collect metrics only from ECS instances within the specified subnet. |
   

6. The Job configuration includes items such as the collection time interval, collection timeout, collection protocol, and port number. You can configure multiple groups of jobs for a task.


Currently, three service discovery configurations are available:


|Service discovery configuration |Configuration example |
|---|---|
|volc_sd_configs |The default service discovery configuration. The following is an example:<br><br>```YAML```<br>```  volc_sd_configs:```<br>```  - port: 9091 # Required. The port number for collecting metrics.```<br>```    project_name: project_a # Optional. ECS instances are filtered by project.```<br>```    tag_filters: # Optional. ECS instances are filtered by label.```<br>```    - key: ecs-label # The label name for filtering ECS instances.```<br>```      values: ["demo-a", "demo-b"] # The label value for filtering ECS instances.```<br>```    instance_ids: # Optional. ECS instances are filtered by ID.```<br>```    - i-ycpy3h***```<br>```    - i-ycroi4***```<br>```    instance_name: ecs-demo # Optional. ECS instances can be filtered by name using fuzzy matching.```<br><br><br> |
|http_sd_configs |The service discovery configuration that is natively supported by Prometheus. With no ecosystem dependencies, the configuration applies to scenarios where a complex service discovery mechanism is not required and various backends are flexibly integrated, such as lightweight architectures without a service registry or integration with a custom registry. For more details, see the [official documentation](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#http_sd_config). Sample code:<br><br>```YAML```<br>```  http_sd_configs:```<br>```  - url: 'https://service-discovery.example.com/targets'  # Required. The HTTP or HTTPS endpoint for getting a list of targets.```<br>```    refresh_interval: 15s  # Optional. The time interval of pulling the target list.```<br>```    timeout: 8s  # The timeout for a single request to the endpoint.```<br>```    basic_auth:  # Optional. Basic authentication (username and password).```<br>```      username: 'prometheus-sd'  # Username.```<br>```      password: 'secure-pass-123'  # Password.```<br>```    tls_config:    # Optional. The TLS configuration for secure communication with an HTTPS endpoint.```<br>```      ca_file: '/etc/prometheus/root-ca.crt'  # Client certificate for mutual authentication.```<br>```      server_name: 'service-discovery.example.com'  # Hostname for verifying the server certificate.```<br>```      insecure_skip_verify: false  # Whether to skip certification verification. You are advised against skipping certification verification in production environments.```<br><br><br> |
|consul_sd_configs |The service discovery configuration that is natively supported by Prometheus. It natively integrates with Consul, offering a high degree of automation. It applies to scenarios where the Consul service mesh has been deployed, or large\-scale dynamic monitoring is required, such as the scenario where Consul is deployed as a service registry, monitoring of large\-scale microservices clusters, and multi\-data center environments. For more details, see the [official documentation](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#consul_sd_config). Sample code:<br><br>```YAML```<br>```    consul_sd_configs:```<br>```    - server: 'consul-server:8500' # Required. The HTTP API address of the Consul service.```<br>```      datacenter: 'dc-prod' # Optional. The name of the Consul data center, which must be consistent with the Consul cluster configuration.```<br>```      services: ['user-service', 'order-service', 'payment-*']  # Optional. The services to be monitored. Wildcards are supported.```<br>```      health_check: true # Optional. Whether to retain only instances for which the Consul health check status is passing. We recommend that you enable this feature in production environments.```<br>```      acl_token_file: '/etc/prometheus/consul-acl-token.txt' # Optional. The file path where the Consul ACL token is stored. You can read the ACL token from the file.```<br>```      timeout: 8s # Optional. The Consul connection timeout.```<br><br><br> |


The following content is a complete example of Job configuration in which the service discovery configuration `volc_sd_configs` is used.

```yaml
global:
  scrape_interval: 15s # Required. The global collection interval.
  scrape_timeout: 10s # Required. The global collection timeout.
  external_labels: # Optional. The labels that are automatically added to the collection metrics.
    cluster: cluster1
scrape_configs:
- job_name: ecs # Required. The name of the job.
  scrape_interval: 30s # Optional. The collection interval of the job, of which priority is higher than the global configuration.
  scrape_timeout: 30s # Optional. The collection timeout of the job, of which priority is higher than the global configuration.
  metrics_path: /metrics # Required. The URI path for metric collection. Default value: /metrics.
  honor_labels: true # Optional. The handling policy when labels conflict. If the value is set to true, labels are retained. If the value is set to false, labels are renamed.
  honor_timestamps: true # Optional. Whether the timestamps in the metrics are used.
  scheme: http # Required. The collection protocol. Valid values: http and https. Default value: http.
  params: # Optional. The HTTP protocol parameters, which are valid only when scheme is set to http.
    p1: ["v1", "v2"]
  tls_config: # Optional. The Transport Layer Security (TLS) configuration when the HTTP protocol is used, which is valid only when scheme is set to https.
    ca: MIICXwIBAA*** # Configure the Certificate Authority (CA) certificate.
    cert: MIICjzCCAfg*** # Configure the TLS certificate.
    key: MIICXQIBAA*** # Configure the TLS key.
    server_name: tls-server-demo # Configure the TLS server name.
    insecure_skip_verify: true # Specify whether to disable the validation of the HTTPS server certificate.
    min_version: TLS12 # The earliest version that is supported by TLS. Valid values: TLS10 (TLS 1.0), TLS11 (TLS 1.1), TLS12 (TLS 1.2), and TLS13 (TLS 1.3).
  headers: # Optional. The custom headers in HTTP requests.
    - a
    - b
  relabel_configs: # Optional. Configure metric relabeling. This parameter can be omitted if it is not required.
    - action: replace # The operation after label matching. Valid values: replace, keep, and drop.
      source_labels: [ xxxxxx ] # The original labels whose values are taken for relabeling.
      separator: ; # The separator in the regular expression, which is the semicolon (;) by default.
      target_label: xxxxxx # The label name that you need to add or reset when action is set to replace.
      regex: (.*) # Perform regular expression matching on the value of source_labels.
      modulus: 123 # The modulus of the hash value for the source label.
      replacement: $1
  metric_relabel_configs: # Optional. Configure relabeling after metric scraping. This parameter can be omitted if it is not required.
    - action: replace # The operation after label matching. Valid values: replace, keep, and drop.
      source_labels: [ xxxxxx ] # The original labels whose values are taken for relabeling.
      separator: ; # The separator in the regular expression, which is the semicolon (;) by default.
      target_label: xxxxxx # The label name that you need to add or reset when action is set to replace.
      regex: (.*) # Perform regular expression matching on the value of source_labels.
      modulus: 123 # The modulus of the hash value for the source label.
      replacement: $1
  sample_limit: 1024 # Optional. The number of samples collected by the collector each time. If the value is set 0, no limit is set.
  volc_sd_configs:
  - port: 9091 # Required. The port number for collecting metrics.
    project_name: project_a # Optional. ECS instances are filtered by project.
    tag_filters: # Optional. ECS instances are filtered by label.
    - key: ecs-label # The label name for filtering ECS instances.
      values: ["demo-a", "demo-b"] # The label value for filtering ECS instances.
    instance_ids: # Optional. ECS instances are filtered by ID.
    - i-ycpy3h***
    - i-ycroi4***
    instance_name: ecs-demo # Optional. ECS instance names can be used for fuzzy match and filter.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For more configuration item descriptions, refer to the <a href="https://prometheus.io/docs/prometheus/latest/configuration/configuration/#relabel_config">official documentation</a>.</div>


* <div data-tips="true" data-tips-type="tip">The job configurations will take effect about 1 minute after modification and deployment. Please wait patiently.</div>


* <div data-tips="true" data-tips-type="tip">When you configure multiple filter conditions for ECS instances, the conditions are in an <strong>AND</strong> relationship. In this way, only ECS instances that meet all conditions will be identified and monitored.</div>


7. Click **Confirm** to complete the configuration.


<span id="iJe5Js2t"></span>
## Validate results

After the configuration is complete, you can view the status and details of the task. Check whether the target ECS instance is integrated with VMP properly.


1. Select **Access Center \> Access Jobs** in the left **navigation bar** and select the **managed environment** tab.

2. Select the target job in the job list, click the job name, and enter the access job details. Select the **Target List** tab to view the ECS instances properly integrated with Vital Managed Service for Prometheus.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7d63d0a62f30ff191580c6500e26dedf.png) </span>

<span id="OzyYbVPS"></span>
## Related document


* [Monitoring ECS instances by using node-exporter](https://docs.byteplus.com/en/docs/vmp/Monitoring-ECS-instances)

* [Monitoring applications on ECS instances](https://docs.byteplus.com/en/docs/vmp/Monitoring-applications-in-an-ECS-instance)
