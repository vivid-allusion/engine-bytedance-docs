---
title: "Autoscaling based on self-managed Prometheus"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Horizontal_Pod_Autoscaler_based_on_self-built_Prometheus"
---

When you use a self\-managed Prometheus system to monitor clusters, you can deploy the open source Prometheus adapter in the clusters to connect to your self\-managed Prometheus. This achieves Horizontal Pod Autoscaler (HPA) based on custom metrics. This topic describes how to deploy the open source Prometheus adapter in a cluster and achieve HPA.

<span id=".5beu5byC5oCn6K-05piO"></span>
## Differences

You can use a self\-managed Prometheus system or VMP to connect to a VKE cluster and achieve HPA based on metrics. The following table describes the main differences when different systems are connected.

<span id=".cHJvbWV0aGV1cy1hZGFwdGVyLee7hOS7tuS4juW8gOa6kC1wcm9tZXRoZXVzLWFkYXB0ZXI="></span>
### Prometheus adapter add\-on and open source Prometheus adapter


|Item |Prometheus adapter add\-on |Open source Prometheus adapter |
|---|---|---|
|Stability and support |VKE provides stability guarantee and technical support. |You need to manage and maintain it yourself and seek support from the community. |
|Adaptability |It can automatically adapt to VMP. |You need to set up and adapt to a Prometheus service. |
|Ease of use |It is easy to use. |The features are consistent with the community edition. |


<span id=".5omY566hLXByb21ldGhldXMt5LiO6Ieq5bu6LXByb21ldGhldXM="></span>
### VMP and self\-managed Prometheus


|Item |VMP |Self\-managed Prometheus |
|---|---|---|
|Adaptability |Highly compatible with VKE clusters. |It is managed and maintained by the user and is consistent with the community version. |
|Service scope |Provides a complete managed solution from collection to observation. |\- |
|Access method |Supports the standard Prometheus access method. |\- |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster has been created and is running as expected. For detailed operations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The self\-managed Prometheus service has been deployed, and the VKE cluster can access the service and collect metric data as expected.

* Configure the local environment (Linux/Mac):

   * Install and configure the Helm tool. Make sure that Helm can be connected to the specified Helm repository.

   * The kubectl tool is installed on your on\-premises computer. For details, see [Installing and configuring kubectl](https://kubernetes.io/docs/tasks/tools/).

   * The target cluster is connected through kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* When you modify the Prometheus URL and configure authentication, invalid configurations may cause the Prometheus adapter to fail to obtain metric data, which will affect the autoscaling feature of HPA.

* When you pull an image, if the specified image architecture is inconsistent with the architecture of the Kubernetes cluster nodes, the image may not run as expected in the cluster.

* When you configure custom metrics, invalid configurations will prevent HPA from autoscaling as expected. This may cause resource waste or degraded business performance.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5ouJ5Y-WLWNoYXJ0"></span>
### Step 1: Pull a chart


1. On your on\-premises computer, run the following command to pull the Prometheus adapter chart locally.


```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm pull prometheus-community/prometheus-adapter
```



2. Extract the pulled chart file and access the extracted folder. The file named `prometheus-adapter-4.11.0.tgz` is used as an example in this topic.


```bash
tar -zxvf prometheus-adapter-4.11.0.tgz && cd prometheus-adapter
```


<span id=".5q2l6aqk5LqM77ya5L-u5pS56YWN572u"></span>
### Step 2: Modify configurations


1. Open the `values.yaml` file on your on\-premises computer and change the Prometheus URL to the query address of your self\-managed Prometheus system. If the port number is not required, you can delete it.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1b9ed452a90fa7232bd8d2168386798e.png) </span>

2. If you have configured basic authentication for the self\-managed Prometheus system, add the `extraArguments` field in `values.yaml` to authenticate the Prometheus adapter. Generate the token using online or offline tools with your Prometheus basic authentication credentials, then add it to the corresponding parameter.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cbe1230564cf85756f615d3d65cd8aa4.png) </span>


<span id=".5q2l6aqk5LiJ77ya5p6E5bu66ZWc5YOP"></span>
### Step 3: Build an image


1. Pull an image that matches the architecture of your Kubernetes cluster nodes from your on\-premises computer. This topic uses the `linux/amd64` architecture as an example.


```bash
docker pull --platform linux/amd64 registry.k8s.io/prometheus-adapter/prometheus-adapter:v0.12.0
```



2. Add tags to the pulled image and specify the address of the target container registry, image name, and version number. This topic takes `doc-cn-beijing.cr.volces.com/vke/prometheus-adapter-demo:v1.0` as an example.


```bash
docker tag registry.k8s.io/prometheus-adapter/prometheus-adapter:v0.12.0 doc-cn-beijing.cr.volces.com/vke/prometheus-adapter-demo:v1.0
```



3. Push the image to the target container registry. If you use the Container Registry (CR) service of BytePlus, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images) for more operation details.


```bash
docker push doc-cn-beijing.cr.volces.com/vke/prometheus-adapter-demo:v1.0
```



4. Modify the image path in the `values.yaml` file so that it points to the pushed image address.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fa6dee5f6533f4986cebe504bf87b6b.png) </span>


<span id=".5q2l6aqk5Zub77ya6YWN572u6Ieq5a6a5LmJ5oyH5qCH"></span>
### Step 4: Configure custom metrics


1. In the configuration section of custom metrics in `values.yaml`, set `default` to `false`, which indicates that the default configuration is disabled.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e14a8bc77a41a160aef16ae67b2f52b5.png) </span>

2. Specify the `custom` field. The following sample code takes the network metrics `container_network_receive_bytes_total` and `container_network_transmit_bytes_total` as examples.


```yaml
rules:
  default: false

  custom:
    - seriesQuery: 'container_network_receive_bytes_total'
      resources:
        overrides:
          namespace: {resource: "namespace"}
          pod: {resource: "pod"}
      name: {as: 'k8s_pod_network_receive_throughput'}
      metricsQuery: 'sum(rate(<<.Series>>{<<.LabelMatchers>>,pod!=""}[1m])) by (<<.GroupBy>>) / 125000.0'
    - seriesQuery: 'container_network_transmit_bytes_total'
      resources:
        overrides:
          namespace: {resource: "namespace"}
          pod: {resource: "pod"}
      name: {as: 'k8s_pod_network_transmit_throughput'}
      metricsQuery: 'sum(rate(<<.Series>>{<<.LabelMatchers>>,pod!=""}[1m])) by (<<.GroupBy>>) / 125000.0'
```


<span id=".5q2l6aqk5LqU77ya5a6J6KOFLWNoYXJ0"></span>
### Step 5: Install the chart

In the `prometheus-adapter` folder, run the following command to install the chart. Replace `prom-adapter` with another name based on your business requirements.

```bash
helm install prom-adapter .
```


<span id=".5p-l55yL6YWN572u"></span>
## Viewing configurations

After the Prometheus\-adapter is installed, log in to the cluster and check whether all related workloads are running as expected and the parameters are valid.


1. Log in to [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the cluster you want to configure.

4. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**. In the workload list, check whether all related workloads function as expected.

5. In the left navigation bar of the cluster management page, click **Configurations \> ConfigMap** to view ConfigMaps.

6. In the left navigation bar of the cluster management page, click **Workload \> Resource Explorer**. Select API Group from the **Category** list to view API groups.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. Create a workload in the cluster. This topic provides an example of how to create a Deployment.


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: workload-demo
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: workload-demo
  template:
    metadata:
      labels:
        app: workload-demo
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```



2. Create an HPA associated with the workload and configure autoscaling based on network metrics.


```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: hpa-demo
  namespace: default
spec:
  maxReplicas: 10
  metrics:
  - pods:
      metric:
        name: k8s_pod_network_receive_throughput
      target:
        averageValue: "80"
        type: AverageValue
    type: Pods
  - pods:
      metric:
        name: k8s_pod_network_transmit_throughput
      target:
        averageValue: "80"
        type: AverageValue
    type: Pods
  minReplicas: 1
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: workload-demo
```



3. View workload details. Click the **Autoscaling** tab, and you can view the HPA configuration of the current workload. Achieve horizontal scaling for the workload based on the self\-managed Prometheus system.
