---
title: "RabbitMQ exporter integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Integrating-through-RabbitMQ-Exporter"
---

Vital Managed Service for Prometheus (VMP) monitors the operational status of RabbitMQ by using the exporter. This topic describes how to deploy rabbitmq\-exporter in a cluster and monitor RabbitMQ.

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

<span id=".5q2l6aqk5LiA77ya5L2_55SoIFNlY3JldCDphY3nva4gUmFiYml0TVEg5a-G56CB"></span>
### Step 1: Use a secret to configure the RabbitMQ password


1. Log in to the [VKE](https://console.byteplus.com/vke) console.

2. Click **Cluster** in the left navigation pane.

3. On the cluster list page, click the name of the cluster that you want to configure.

4. In the left navigation pane of the cluster details page, click **Configurations** \> **Secret**. On the page that appears, click **Create with Yaml** to configure a secret.


```yaml
apiVersion: v1
kind: Secret
metadata:
  name: rabbitmq-demo
  namespace: volcano-metrics
type: Opaque
stringData:
  username: rabbitmq-username # Specify the login username for RabbitMQ.
  password: rabbitmq-password # Specify the login password for RabbitMQ.
```


<span id=".5q2l6aqk5LqM77ya6YOo572yIHJhYmJpdG1xLWV4cG9ydGVy"></span>
### Step 2: Deploy rabbitmq\-exporter


1. In the left navigation pane of the cluster details page, click **Workload \> Deployment**.

2. Click **Create with Yaml** to deploy rabbitmq\-exporter.


```Yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: rabbitmq-exporter # Specify the name of the exporter.
  namespace: volcano-metrics # Specify the namespace of the exporter.
  labels:
    app-name: rabbitmq-exporter # Configure the labels of the exporter.
spec:
  replicas: 1 # Specify the number of replicas for the exporter.
  selector:
    matchLabels:
      app-name: rabbitmq-exporter # Change the name based on your business requirements. It is recommended to add information about the RabbitMQ instance.
  template:
    metadata:
      labels:
        app-name: rabbitmq-exporter # Change the name based on your business requirements. It is recommended to add information about the RabbitMQ instance.
    spec:
      containers:
      - name: postgres-exporter # Specify the container name.
        image: kbudde/rabbitmq-exporter:latest # Pull the exporter image from Docker Hub.
        env:
          - name: RABBIT_USER # Specify the login username for RabbitMQ by using global variables.
            valueFrom:
              secretKeyRef:
                name: rabbitmq-demo
                key: username
          - name: RABBIT_PASSWORD # Specify the login password for RabbitMQ by using global variables.
            valueFrom:
              secretKeyRef:
                name: rabbitmq-demo
                key: password
          - name: RABBIT_URL # Specify the address and port of RabbitMQ by using global variables.
            value: "x.x.x.x:15672"
        ports:
        - name: metric-port # Specify the container port name.
          containerPort: 9419 # Specify the container port number.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed parameters of rabbitmq\-exporter, refer to <a href="https://github.com/kbudde/rabbitmq_exporter">rabbitmq\-exporter</a>.</div>


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
  name: rabbitmq-exporter # Specify the name of PodMonitor.
  namespace: volcano-metrics # Specify the namespace of PodMonitor.
  labels: 
    volcengine.vmp: "true" # Configure the labels for PodMonitor to allow the labels to be identified by prometheus-agent.
spec:
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port # Specify the container port name of the exporter.
    path: /metrics # Specify the URI path for metric exposure. The value is /metrics by default if it is not specified.
    relabelings: # Configure metric relabeling. This parameter can be omitted if it is not required.
    - action: replace
      sourceLabels:
      - instance
      regex: (.*)
      targetLabel: instance
      replacement: 'rbtmq-xxxxxx' # Specify the ID of the RabbitMQ instance.
  namespaceSelector:
    matchNames: 
    - volcano-metrics # Specify the namespace where the exporter is located.
  selector: 
    matchLabels:
      app-name: rabbitmq-exporter # Specify the label value of the exporter to locate and select the target pod.
```


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results


1. Execute the following command to configure Grafana port forwarding:


```bash
kubectl port-forward service/grafana 3000:3000 -n volcano-metrics
```



2. Open a browser in your local environment (Linux/Mac), paste **localhost:3000** into the address bar, and then press Enter to go to the Grafana login page. Log in to Grafana by using the default username `admin` and password `admin`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76b0d6fc909f3113679be523218ecad5.png) </span>

3. After you log in to Grafana, you can create a dashboard to view the metric information of RabbitMQ.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b4c0ea65b2e949c53a7c028298515892.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed parameters of the rabbitmq\-exporter, refer to <a href="https://github.com/kbudde/rabbitmq_exporter">rabbitmq\-exporter</a>.   </div>
