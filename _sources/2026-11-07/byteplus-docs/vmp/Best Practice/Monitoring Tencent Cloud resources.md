---
title: "Monitoring Tencent Cloud resources"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Monitoring_Tencent_Cloud_resources"
---

Vital Managed Service for Prometheus (VMP) allows you to access the metrics of Tencent Cloud services by using exporters. This topic describes how to deploy the Tencent Cloud exporter in a Vital Kubernetes Engine (VKE) cluster to monitor Tencent Cloud services.

## Background

### Basic information

The open source monitoring exporter (qcloud exporter) can automatically export the metrics of Tencent Cloud services in the Prometheus format. You can use VMP to pull the metrics exported by the qcloud exporter to monitor Tencent Cloud resources in BytePlus.

> **tip**

* > For more information about the Tencent Cloud exporter, refer to [Official open source addresses](https://github.com/tencentyun/tencentcloud-exporter).

* > For the cloud service metrics that can be exported by the Tencent Cloud exporter and the corresponding namespaces of the cloud services, refer to the [official documentation of Tencent Cloud](https://cloud.tencent.com/document/product/248/62458).

### Collection configuration

You can perform the following configuration to define the collection configuration and metric conversion features of the Tencent Cloud exporter:

```yaml
credential:
  access_key: <YOUR_ACCESS_KEY>                  # Required. The access key ID of the cloud API.
  secret_key: <YOUR_ACCESS_SECRET>               # Required. The secret access key of the cloud API.
  region: <REGION>                               # Required. The region where the instance is located.

rate_limit: 15                                   # The rate limit for pulling Tencent Cloud metrics. The default maximum value is 20 QPS.


// 整个产品纬度配置, 每个产品一个 item
products:
  - namespace: QCE/CMONGO                        # Required. The product namespace.
    all_metrics: true                            # This parameter is commonly used. We recommend setting the value to true to export all supported metrics.
    all_instances: true                          # This parameter is commonly used. We recommend setting the value to true to export all instances in the region.
    extra_labels: [InstanceName,Zone]            # Optional. Export instance fields as metric labels.
    only_include_metrics: [Inserts]              # Optional. Only export these metrics. When it is specified, all_metrics is ignored.
    exclude_metrics: [Reads]                     # Optional. Do not export these metrics.
    only_include_instances: [cmgo-xxxxxxxx]      # Optional. Only export these instance IDs. When it is specified, all_instances is ignored.
    exclude_instances: [cmgo-xxxxxxxx]           # Optional. Do not export these instance IDs.
    custom_query_dimensions:                     # Optional. This parameter is not commonly used. It specifies custom query conditions for metrics. When this parameter is specified, all_instances, only_include_instances, and exclude_instances are ignored. Use this parameter to query metrics that do not support instance-level queries.
      - target: cmgo-xxxxxxxx
    statistics_types: [avg]                      # Optional. Pull N data points and then perform calculations such as max, min, avg, and last. The last calculation is used by default which returns the latest value.
    period_seconds: 60                           # Optional. The metric statistical period.
    range_seconds: 300                           # Optional. The selected time range: Start time = now - range_seconds, and end time = now.
    delay_seconds: 60                            # Optional. The time offset: End time = now - delay_seconds.
    metric_name_type: 1                          # Optional. The name formatting type for exported metrics. 1 indicates converting uppercase letters to lowercase letters and adding underscores. 2 indicates converting to lowercase letters. The default value is 2.
    reload_interval_minutes: 60                  # Optional. When all_instances is set to true, the instance list is periodically reloaded. We do not recommend setting the frequency too high.


# The single metric-level configuration, one item per metric.
metrics:
  - tc_namespace: QCE/CMONGO                     # The product namespace. This is the same as namespace.
    tc_metric_name: Inserts                      # The metric name defined by Cloud Monitor.
    tc_metric_rename: Inserts                    # The display name of the exported metric.
    tc_metric_name_type: 1                       # Optional. The name formatting type for exported metrics. 1 = uppercase to lowercase with underscores. 2 = lowercase. The default value is 1.
    tc_labels: [InstanceName]                    # Optional. Export instance fields as metric labels.
    tc_myself_dimensions:                        # Optional. The parameter is the same as custom_query_dimensions.
    tc_statistics: [Avg]                         # Optional. The parameter is the same as statistics_types.
    period_seconds: 60                           # Optional. The parameter is the same as period_seconds.
    range_seconds: 300                           # Optional. The parameter is the same as range_seconds.
    delay_seconds: 60                            # Optional. The parameter is the same as delay_seconds.
```

When you perform the configuration, you mainly modify the following content:

* Configure the `credential` authentication information of the cloud API, including `access_key`, `secret_key`, and `region`.

* Configure `products` metrics and instance exported information.

For example, if you need to collect and export the metric information of all instances for TencentDB for MongoDB, you can configure the following settings:

```yaml
credential:
  access_key: <YOUR_ACCESS_KEY>               # The access key ID of the cloud API.
  secret_key: <YOUR_ACCESS_SECRET>            # The secret access key of the cloud API.
  region: "ap-guangzhou"                      # The region where the instance is located.

products:
  - namespace: QCE/CMONGO                     # The product namespace.
    all_metrics: true                         # Export all supported metrics.
    all_instances: true                       # Export all instances in the region
    extra_labels: [InstanceName,Zone]         # Export instance fields as metric labels
```

## Prerequisites

* A BytePlus root user has been created, and VKE has been activated.

* A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* The VKE cluster has been integrated with VMP. For details, see [VKE integration](https://docs.byteplus.com/en/docs/vmp/cluster-monitoring).

## Configuration procedure

### Step 1: Build an image of the Tencent Cloud exporter

1. Run the following command to build an image of the Tencent Cloud exporter, which facilitates the deployment of the exporter in the VKE cluster:

```bash
git clone https://github.com/tencentyun/tencentcloud-exporter.git
cd tencentcloud-exporter
# Build an image.
docker build -t <image> .
```

2. After the image is built, upload the image to [CR](https://docs.byteplus.com/en/docs/cr/what-is-cr) for use. For more details, see [Pushing and pulling images with Docker](https://docs.byteplus.com/en/docs/cr/Push_and_pull_artifacts). You can also use another public cloud or self\-built image registry.

### Step 2: Deploy the exporter in the cluster

1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. Click **Cluster** in the left navigation pane.

3. On the cluster list page, click the target cluster that you want to configure.

4. In the left navigation bar of the cluster details page, click **Configurations \> ConfigMap**. On the page that appears, click **Create with Yaml** to configure the exporter. Modify the `access_key`, `secret_key`, and `region` fields based on your business requirements. For more details about parameters, refer to [Collection configuration](https://docs.byteplus.com/en/docs/vmp/Monitoring_Tencent_Cloud_resources#.6YeH6ZuG6YWN572u).

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: qcloud-exporter-config
  namespace: default
data:
  product.yaml: |-
    credential:
      access_key: <YOUR_ACCESS_KEY>
      secret_key: <YOUR_ACCESS_SECRET>
      region: <REGION>

    products:
      - namespace: QCE/CMONGO
        all_metrics: true
        all_instances: true
        extra_labels: [InstanceName,Zone]
```

> **tip**

> Modify the `credential` authentication information of the cloud API in the preceding configurations, including `access_key`, `secret_key`, and `region`.

5. In the left navigation bar of the cluster details page, click **Workload \> Deployment**. On the page that appears, click **Create with Yaml** to deploy the exporter in the cluster.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: qcloud-exporter
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: qcloud-exporter
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: qcloud-exporter
    spec:
      containers:
      - args:
        - --config.file=/usr/local/etc/product.yaml
        image: <image>
        imagePullPolicy: IfNotPresent
        name: exporter
        ports:
        - containerPort: 9123
          name: http
          protocol: TCP
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /usr/local/etc
          name: config
          readOnly: true
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
      volumes:
      - configMap:
          defaultMode: 420
          name: qcloud-exporter-config
        name: config
```

6. In the left navigation bar of the cluster details page, click **Services and Ingresses \> Service**. On the page that appears, click **Create with Yaml** to configure the service that corresponds to the exporter.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: qcloud-exporter
  namespace: default
  labels:
    app: qcloud-exporter
spec:
  ports:
  - name: http
    port: 9123
    protocol: TCP
    targetPort: 9123
  selector:
    app: qcloud-exporter
  type: ClusterIP
```

### Step 3: Configure a collection rule

1. In the left navigation bar of the cluster details page, click **Workload \> Resource Explorer**. On the page that appears, click **Create with Yaml** to configure the collection rule through ServiceMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the YAML configuration in the **Yaml** field.

```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: qcloud-exporter    # Enter a unique name.
  namespace: default # Specify the namespace of ServiceMonitor.
  labels: 
    volcengine.vmp: "true" # Configure the labels of ServiceMonitor to allow the labels to be identified by prometheus-agent.
spec:
  endpoints:
  - interval: 60s
    port: http # Specify the service port name.
    path: /metrics # Specify the URI path for metric exposure. The value is /metrics by default if it is not specified.
  namespaceSelector:
    any: true
  selector:
    matchLabels:
      app: qcloud-exporter # Specify the label value of the service to locate the target service.
```

## Validate results

You can view metric data by using the Explore feature of VMP. For more details, refer to [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).

You can also use self\-built Grafana to read data stored in VMP and create metric dashboards. For more details, see [Deploying Grafana and connecting to a workspace in the VKE cluster](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).
