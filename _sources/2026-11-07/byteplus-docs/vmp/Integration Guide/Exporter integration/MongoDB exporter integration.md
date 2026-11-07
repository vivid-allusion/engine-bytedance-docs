---
title: "MongoDB exporter integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Integrating-through-MongoDB-Exporter"
---

Vital Managed Service for Prometheus (VMP) monitors the operational status of MongoDB by using the exporter. This topic describes how to deploy mongodb\-exporter in a cluster and monitor MongoDB.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* VMP

   * A VMP workspace has been created. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* VKE

   * A BytePlus root user has been created, and VKE has been activated.

   * The VKE cluster has been integrated with VMP. For details, see [VKE integration](https://docs.byteplus.com/en/docs/vmp/cluster-monitoring).

* Grafana has been deployed and integrated with the workspace.

   * [Deploying Grafana in a VKE cluster and accessing workspaces](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)

   * [Deploying Grafana on an ECS instance and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/Deploying_Grafana_on_an_ECS_instance_and_integrating_Grafana_with_a_workspace)


<span id=".6YWN572u5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YOo572yIG1vbmdvZGItZXhwb3J0ZXI="></span>
### Step 1: Deploy mongodb\-exporter


1. Log in to the [VKE](https://console.byteplus.com/vke) console.

2. In the left navigation pane, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the name of the cluster to go to the cluster details page.

4. Click **Workload \> Deployment** in the left navigation pane. Click **Create with Yaml** to deploy mongodb\-exporter.


```Yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodb-exporter# Specify the name of the exporter.
  namespace: volcano-metrics# Specify the namespace where the exporter is located.
  labels: 
    app-name: mongodb-exporter# Specify the label of the exporter.
spec:
  replicas: 1
  selector:
    matchLabels:
      app-name: mongodb-exporter# Change the name based on your business requirements. You can use the information about the MongoDB instance.
  template:
    metadata:
      labels:
        app-name: mongodb-exporter# Change the name based on your business requirements. You can use the information about the MongoDB instance.
    spec:
      containers:
        - args:
            - "--collect-all"
            - "--mongodb.uri=mongodb://<user-name>:<password>@<mongodb-address>:<mongodb-port>"
          image: bitnami/mongodb-exporter:latest# Pull the exporter image from Docker Hub.
          imagePullPolicy: IfNotPresent
          name: mongodb-exporter# Specify the container name.
          ports:
            - containerPort: 9216# Specify the container port number.
              name: metric-port# Specify the container port name.
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      terminationGracePeriodSeconds: 30
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In this example, <code>--collect-all</code> is used to collect all metrics of MongoDB. You can also adjust the collection scope by specifying the appropriate parameters. For details, see <a href="https://github.com/percona/mongodb_exporter/blob/main/REFERENCE.md">mongodb\-exporter</a>.</div>


<span id=".5q2l6aqk5LqM77ya6YWN572u6YeH6ZuG6KeE5YiZ"></span>
### Step 2: Configure a collection rule


1. In the left navigation pane of the cluster details page, click **Workload \> Resource Explorer**.

2. Click **Create with Yaml** to configure a collection rule by using PodMonitor.

   * Select **Custom** from the **Type** list.

   * Enter the YAML configuration in the **Yaml** field.


```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: mongodb-exporter# Specify the name of PodMonitor.
  namespace: volcano-metrics# Specify the namespace of PodMonitor.
  labels: 
    volcengine.vmp: "true"# Configure the labels for PodMonitor to allow the labels to be identified by prometheus-agent.
spec:
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port# Specify the container port name of the exporter.
    path: /metrics# Specify the URI path for metric exposure. The value is /metrics by default if it is not specified.
    relabelings:# Configure metric relabeling. If this parameter is not required, it can be omitted.
    - action: replace
      sourceLabels:
      - instance
      regex: (.*)
      targetLabel: instance
      replacement: 'mongodb-xxxxxx'# Specify the ID of the MongoDB instance.
  namespaceSelector:
    matchNames: 
    - volcano-metrics# Specify the namespace of the exporter.
  selector: 
    matchLabels:
      app-name: mongodb-exporter# Specify the label value of the exporter to locate and select the target pod.
```


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results


1. Execute the following command to configure Grafana port forwarding:


```bash
kubectl port-forward service/grafana 3000:3000 -n volcano-metrics
```



2. Open a browser in your local environment (Linux/Mac), paste **localhost:3000** into the address bar, and then press Enter to go to the Grafana login page. Log in to Grafana by using the default username `admin` and password `admin`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76b0d6fc909f3113679be523218ecad5.png) </span>

3. After you log in to Grafana, you can create a dashboard to view the metric information of MongoDB.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_99129aec24a26bf9eca170d707b65a9a.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed parameters of mongodb\-exporter, refer to <a href="https://github.com/percona/mongodb_exporter">mongodb\-exporter</a>.   </div>
