---
title: "Elasticsearch exporter integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Integrating-through-ElasticSearch-Exporter"
---

VMP monitors the operational status of Elasticsearch by using the exporter. This topic describes how to deploy elasticsearch\-exporter in a cluster and how to monitor Elasticsearch.

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

<span id=".5q2l6aqk5LiA77ya5L2_55SoIFNlY3JldCDphY3nva4gRWxhc3RpY3NlYXJjaCDov57mjqXkuLI="></span>
### Step 1: Use a secret to configure the Elasticsearch connection string


1. Log in to the [VKE](https://console.byteplus.com/vke/overview) console.

2. Click **Cluster** in the left navigation pane.

3. On the cluster list page, click the name of the cluster that you want to configure.

4. In the left navigation pane of the cluster details page, click **Configurations** \> **Secret**. On the page that appears, click **Create with Yaml** to configure a secret.


```yaml
apiVersion: v1
kind: Secret
metadata:
  name: es-secret-demo # Specify the secret name.
  namespace: volcano-metrics # Specify the namespace of the secret.
type: Opaque
stringData:
  esURI: <proto>://<user>:<password>@<es-address>:<port> # Configure the link of Elasticsearch, which consists of the username, password, address, and port number.
```


<span id=".5q2l6aqk5LqM77ya6YOo572yIGVsYXN0aWNzZWFyY2gtZXhwb3J0ZXI="></span>
### Step 2: Deploy elasticsearch\-exporter


1. In the left navigation pane of the cluster details page, click **Workload \> Deployment**.

2. Click **Create with Yaml** to deploy elasticsearch\-exporter.


```Yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: es-exporter # Specify the name of the exporter.
  namespace: volcano-metrics # Specify the namespace of the exporter.
  labels: 
    app-name: es-exporter # Configure the labels of the exporter.
spec:
  replicas: 1 # Specify the number of replicas for the exporter.
  selector:
    matchLabels:
      app-name: es-exporter # Change the name based on your business requirements. It is recommended to add information about the Elasticsearch instance.
  template:
    metadata:
      labels:
        app-name: es-exporter # Change the name based on your business requirements. It is recommended to add information about the Elasticsearch instance.
    spec:
      containers:
      - env:
         - name: ES-URI # Use a secret to specify the address information of the Elasticsearch instance.
           valueFrom: 
             secretKeyRef:
               name: es-secret-demo
               key: esURI
         - name: ES-ALL # Specify whether to collect all metrics of Elasticsearch.
           value: "ture"
        image: bitnami/elasticsearch-exporter:latest # Pull the exporter image from Docker Hub.
        imagePullPolicy: IfNotPresent
        name: es-exporter # Specify the container name.
        ports:
        - containerPort: 9114 # Specify the container port number.
          name: metric-port # Specify the container port name.
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      terminationGracePeriodSeconds: 30
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In this example, <code>ES-ALL</code> is used to collect all metrics of Elasticsearch. You can also adjust the collection scope by specifying the appropriate parameters. For details, see <a href="https://github.com/prometheus-community/elasticsearch_exporter">elasticsearch_exporter</a>.</div>


<span id=".5q2l6aqk5LiJ77ya6YWN572u6YeH6ZuG6KeE5YiZ"></span>
### Step 3: Configure a collection rule


1. In the left navigation pane of the cluster details page, click **Workload \> Resource Explorer**.

2. Click **Create with Yaml** to configure a collection rule by using PodMonitor.

   * Select **Custom** from the **Type** list.

   * Enter the YAML configuration in the **Yaml** field.


```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: es-exporter # Specify the name of PodMonitor.
  namespace: volcano-metrics # Specify the namespace of PodMonitor.
  labels: 
    volcengine.vmp: "true" # Configure the labels for PodMonitor to allow the labels to be identified by prometheus-agent.
spec:
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port # Specify the container port name of the exporter.
    path: /metrics # Specify the URI path for metric exposure. The value is /metrics by default if it is not specified.
    relabelings: # Configure metric relabeling. If this parameter is not required, it can be omitted.
    - action: replace
      sourceLabels:
      - instance
      regex: (.*)
      targetLabel: instance
      replacement: 'ES-xxxxxx' # Specify the ID of the Elasticsearch instance.
  namespaceSelector:
    matchNames: 
    - volcano-metrics # Specify the namespace of the exporter.
  selector: 
    matchLabels:
      app-name: es-exporter # Specify the label value of the exporter to locate and select the target pod.
```


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results


1. Execute the following command to configure Grafana port forwarding:


```bash
kubectl port-forward service/grafana 3000:3000 -n volcano-metrics
```



2. Open a browser in your local environment (Linux/Mac), enter **localhost:3000** into the address bar to go to the Grafana login interface. Use the default username `admin`, with the password `admin`, to log in.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76b0d6fc909f3113679be523218ecad5.png) </span>

3. After you log in to Grafana, you can create a dashboard to view the metric information of Elasticsearch.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_783da658a34a3dea2d7476ef726b8087.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed parameters of elasticsearch\-exporter, refer to <a href="https://github.com/prometheus-community/elasticsearch_exporter">elasticsearch_exporter</a>.   </div>
