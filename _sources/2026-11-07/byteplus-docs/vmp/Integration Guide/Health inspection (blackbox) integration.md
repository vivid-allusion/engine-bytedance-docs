---
title: "Health inspection (blackbox) integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Blackbox_Integration"
---

After you integrate Vital Managed Service for Prometheus (VMP) with a Vital Kubernetes Engine (VKE) cluster, you can use Probe to perform blackbox monitoring on the cluster and applications. This topic describes how to configure blackbox monitoring through Probe.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

In a standard Kubernetes cluster, you can perform service discovery by configuring ServiceMonitor or PodMonitor to monitor resources or services within the cluster. For example, you can monitor host resource usage, container running status, and the operational data of the database middleware in the cluster. By monitoring the exposed metrics of the infrastructure that supports businesses and services, you can understand its internal running status and potential issues to reduce risks. This monitoring method that directly observes application internal metrics is called **whitebox monitoring**.

In addition to whitebox monitoring, **blackbox monitoring** is often used to monitor services. Blackbox monitoring is used to test and monitor the external visibility of services from the perspectives of users. Common blackbox monitoring provides HTTP probes, TCP probes, DNS probes, ICMP probes, gRPC probes, and other solutions, which can be used to check site or service accessibility and access efficiency. For example:


* **HTTP probe**: monitors HTTP service availability and SSL certificate validity period.

* **ICMP probe**: checks network connectivity and host liveness.

* **TCP probe**: detects host TCP port liveness.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2c2b25b11ddf4ec2e90fd31e9efc968e.png) </span>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The blackbox\-exporter add\-on is an official blackbox monitoring solution provided by the Prometheus community, which allows you to probe and monitor networks and applications via HTTP, HTTPS, DNS, TCP, ICMP, and gRPC. For more details, refer to the <a href="https://github.com/prometheus/blackbox_exporter">official documentation of Github</a>.</div>


The main differences and application scenarios between blackbox monitoring and whitebox monitoring are as follows:


* **Blackbox monitoring**: a fault\-oriented monitoring method, which is mainly used to monitor whether the external services of applications are running as expected from the perspectives of users. Blackbox monitoring can quickly detect faults when faults occur.

* **Whitebox monitoring**: a monitoring method, which is mainly used to monitor the internal running status of applications and predict potential issues accordingly from the perspectives of applications


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A typical and complete monitoring chain requires both whitebox monitoring and blackbox monitoring to work together, in which potential issues are identified through whitebox monitoring, and occurred issues are quickly identified through blackbox monitoring.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* VMP

   * A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* VKE

   * VKE has been activated.

   * A cluster has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   * The cluster is integrated with VMP. For more details, refer to [VKE integration](https://docs.byteplus.com/en/docs/vmp/cluster-monitoring).

   * If you need to monitor the external services of the cluster, enable the **public network access** for the cluster where the blackbox\-exporter add\-on is located. For more details, see [How to manually enable public network for a cluster?](https://docs.byteplus.com/en/docs/vke/How-do-I-manually-enable-internet-facing-access-for-a-cluster)


<span id=".5pON5L2c5q2l6aqk"></span>
## Configuration methods

<span id="BwIMSHRH"></span>
### Method 1: integration center (recommended)

<span id="HJcnl6My"></span>
#### Configure an integration task


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. In the left navigation bar, click **Integration Center \> Component**. On the page that appears, click **Health Inspection (Blackbox)**  to configure the integration task.

4. Configure the deployment environment of the collector. Click **VKE environment** and select an associated cluster.

5. Click **Create Integration Task** to specify the details of the integration task.

   
   |Parameter |Description |
   |---|---|
   |**Basic information** ||
   |Task name |Specify the name of the integration task. It can contain Chinese characters, letters (uppercase and lowercase), digits, and underscores (`_`), and must be 1 to 40 characters in length. |
   |**Scrape configuration** ||
   |JobName |Add job\-related labels to the collected metrics. After you specify this parameter, all collected metrics will be added with the related labels, which help you filter metrics by job. |
   |Metric scraping interval |Configure the collection interval of the collector. |
   |Detection method |Configure the probe method. **http_2xx**, **ping**, and **tcp** are supported. |
   |Detect target |Specify the probe target, which can be a domain name or an IP address. Example: `www.volcengine.com`. |
   

6. Click **Confirm** to complete the configuration.


<span id="VMD5HQuF"></span>
#### Obtain monitoring dashboards

Click the **Effect preview** tab to view sample monitoring dashboards. Click **Get the Grafana template** to download the Grafana monitoring dashboard template in JSON format.

<span id="T0nPyLgW"></span>
#### Query metrics

Click the **Acquisition metric** tab to view the list of metrics for the collection targets.

<span id="6nXqny9J"></span>
### Method 2: custom deployment

<span id=".5q2l6aqk5LiA77ya5Yib5bu6IFByb2JlIENSRCDotYTmupA="></span>
#### Step 1: Create a Probe CRD resource

If no Probe CRD resources exist in your cluster, you need to connect to the cluster in the local environment and execute the following command to create a Probe CRD resource in the cluster:

```bash
kubectl apply -f https://vmp-release-cn-beijing.tos-cn-beijing.volces.com/manifests/crds/promopeartor-crd-probes.yaml
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If your cluster is not deployed in the <strong>China (Beijing)</strong> region, you need to modify the <code>cn-beijing</code> field in the preceding command to the region ID of the corresponding region. For example, if your cluster is deployed in the China (Shanghai) region, the deployment command is <code>kubectl apply -f https://vmp-release-cn-shanghai.tos-cn-shanghai.volces.com/manifests/crds/promopeartor-crd-probes.yaml</code>. For region IDs of different regions, refer to <a href="https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones">Regions and Availability Zones</a>.</div>


* <div data-tips="true" data-tips-type="tip">For deployment methods of CRD resources corresponding to ServiceMonitor and PodMonitor, refer to <a href="https://docs.byteplus.com/en/docs/vmp/How-do-I-create-Custom-Resource-Definition-resources-such-as-ServiceMonitor-in-a-cluster">How do I create CRD resources such as ServiceMonitor in a cluster?</a></div>



<span id=".5q2l6aqk5LqM77ya5L2_55SoIENvbmZpZ01hcCDnrqHnkIYgYmxhY2tib3gtZXhwb3J0ZXIg6YWN572u"></span>
#### Step 2: Manage blackbox\-exporter configuration by using ConfigMap


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. Click **Cluster** in the left navigation pane.

3. On the cluster list page, click the target cluster that you want to configure.

4. In the left navigation pane of the cluster management page, select **Configuration** \> **Parameter**, and click **Create with Yaml** to create a parameter.


```YAML
apiVersion: v1
kind: ConfigMap
metadata:
  name: blackbox-config
  namespace: volcano-metrics
data:
  blackbox.yml: |-
    modules:
  ## ------------HTTP probe module configuration------------
      http_2xx: 
        prober: http
        timeout: 5s ## The probe timeout.
        http:
          valid_http_versions: ["HTTP/1.1", "HTTP/2.0"]   
          valid_status_codes: []  ## The returned HTTP status code. Default value: 2xx.
          method: GET ## The HTTP GET method.
          preferred_ip_protocol: "ip4" ## The HTTP probe is IPv6 by default. You need to specify this parameter to use IPv4 for probe.
  ## ------------HTTP POST probe module configuration------------
      http_post_2xx: 
        prober: http
        timeout: 5s ## The probe timeout.
        http:
          method: POST
          headers: 
            Content-Type: application/json ## Define the HTTP message head.
          body: '{}' ## Define the HTTP message body.
  ## ------------TCP probe module configuration------------
      tcp_connect: 
        prober: tcp
        timeout: 5s ## The probe timeout.
  ## ------------ICMP probe module configuration------------
      icmp: 
        prober: icmp
        timeout: 5s ## The probe timeout.
  ## ------------DNS detection module configuration------------
      dns: 
        prober: dns
        dns:
          query_name: "www.example.com"
          query_type: "A"
          valid_rcodes:
            - NOERROR
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The preceding parameters are for illustration only, in which several probe modules including <code>http_2xx</code>, <code>http_post_2xx</code>, <code>tcp_connect</code>, <code>icmp</code>, and <code>dns</code> are defined. If you have probe requirements via other protocols, you need to add the configurations of the corresponding probe modules. For more details, refer to the <a href="https://github.com/prometheus/blackbox_exporter/blob/master/example.yml">official documentation of Github</a>.</div>


<span id=".5q2l6aqk5LiJ77ya6YOo572yIGJsYWNrYm94LWV4cG9ydGVy"></span>
#### Step 3: Deploy blackbox\-exporter


1. In the left navigation pane of the cluster details page, click **Workload \> Deployment**. Click **Create with Yaml** to deploy blackbox\-exporter.


```Yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: blackbox
  namespace: volcano-metrics
spec:
  selector:
    matchLabels:
      app: blackbox
  template:
    metadata:
      labels:
        app: blackbox
    spec:
      containers:
      - image: prom/blackbox-exporter:latest # Pull the exporter image from Docker Hub.
        name: blackbox
        args:
        - --config.file=/etc/blackbox_exporter/blackbox.yml # Specify the configuration file of ConfigMap.
        - --log.level=error  # Error level control
        ports:
        - containerPort: 9115 # Specify the container port number.
        volumeMounts:
        - name: config
          mountPath: /etc/blackbox_exporter 
      volumes:
      - name: config
        configMap:
          name: blackbox-config # Mount the configuration file of ConfigMap.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed parameters of blackbox\-exporter, refer to <a href="https://github.com/prometheus/blackbox_exporter">blackbox\-exporter</a>.</div>



2. In the left navigation pane, click **Service and Routing \> Service**. Click **Create with Yaml** to create the service.


```yaml
apiVersion: v1
kind: Service
metadata:
  name: service-blackbox # The service name.
  namespace: volcano-metrics # The service namespace.
spec:
  selector:
    app: blackbox # Bind the service to backend Pods through the label selector.
  ports:
  - name: rule # The name of the service port mapping rule.
    protocol: TCP # The service protocol. TCP or UDP is supported.
    port: 9115 # The service port.
    targetPort: 9115 # The container port number.
  type: ClusterIP # The service type.
```


<span id=".5q2l6aqk5Zub77ya6YWN572u5pyN5Yqh5Y-R546w"></span>
#### Step 4: Configure service discovery


1. Click **Workload \> Resource Explorer** in the left navigation pane. Click **Create with Yaml** to configure service discovery.

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the YAML configuration in the **Yaml** field.


```yaml
apiVersion: monitoring.coreos.com/v1
kind: Probe
metadata:
  name: http-probe-example # Configure the service discovery name.
  namespace: volcano-metrics # Configure the namespace of the service discovery.
  labels: 
    volcengine.vmp: "true" # Configure the labels for the probe to allow the labels to be identified by prometheus-agent.
spec:
  jobName: http-example # Specify the task name.
  prober: 
    url: service-blackbox.volcano-metrics.svc.cluster.local:9115 # Specify the service address of blackbox-exporter by using a domain name.
  module: http_2xx # Configure the predefined module used by the probe task.
  targets: # Configure the collection target. Static configuration is used in this example. In actual use, other configurations are also supported, such as the Kubernetes service discovery feature.
    staticConfig: 
      static:
        - www.volcengine.com # Configure the collection object. A static object is configured in this example.
```


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results

<span id="IbCq37mL"></span>
### View the integration task

After the configuration is complete, you can view the status and details of the task. Check whether the integration task is running as expected.


1. In the left navigation bar, click **Access center \> Access task**.

2. Click **VKE environment** **.**  You can view the status of the integration task in the task list.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e5bcb9d0a9e68c7199e8550191e6729.png) </span>

After the integration task is created, you can perform the following O&M operations:


* Click the **name of the task** to go to the task details page.

* Click **Edit** in the **Actions** column to edit the task.

* Click **Suspend task** in the **Actions** column to suspend the task.

* Click **Delete** in the **Actions** column to delete the corresponding integration task.


<span id="MhGxaKlW"></span>
### Query task metrics

Click **Explore** in the left navigation pane. On the page that appears, use the `up` statement to view the status of collection jobs for the integration task. In this example, the statement is `up{job="blackbox_demo"}`. When the metric value is 1, it indicates that the collector is created and working as expected.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7af86d5de81c833c815a4d45042ace85.png) </span>

<span id="kArSFmxO"></span>
## Monitoring information

<span id="Evx7FV4a"></span>
### Query metrics

You can quickly query and display metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b82c1a121a5483b83c2231db5e87a3c0.png) </span>

<span id="EZ1HCS4k"></span>
### Create dashboards

You can install Grafana in a VKE cluster or an ECS instance and then use Grafana to view metrics and create dashboards.


* [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

* [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id="KuxxGQV5"></span>
### Configure alerts

You can configure alerts for the instance in the alerting center of VMP. For details, see [Creating alert rules](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rules).

<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ

<span id=".5aaC5L2V5a-5IGJsYWNrYm94LWV4cG9ydGVyIOi_m-ihjOiwg-ivleWSjCBEZWJ1Z--8nw=="></span>
### How to debug and troubleshoot blackbox\-exporter?

If you identify that an issue exists with the data collected by blackbox\-exporter or the add\-on is in an abnormal state, you can perform the following steps to directly view the data collected by blackbox\-exporter or perform debugging. The specific procedure is as follows:


1. Connect to the cluster locally via kubectl, and execute the following command to configure port mapping for the blackbox\-exporter component instance. `blackbox-84d7xxxx` is the name of add\-on instance.


```bash
kubectl port-forward pod/blackbox-84d7xxxx 9115:9115 -n volcano-metrics
```



2. Execute the following command to view the data and debugging information of the blackbox\-exporter add\-on: Here:

   * The `target` field indicates the probe target.

   * The `module` field indicates the used probe module.

   * `debug=true` indicates whether debugging is enabled. You can view the configuration information, collected metrics, add\-on logs, and other information about the blackbox\-exporter add\-on.


```bash
curl -s "localhost:9115/probe?target=https://www.volcengine.com&module=http_2xx&debug=true"
```
