---
title: "NGINX exporter integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Integrating-through-Nginx-Exporter"
---

Vital Managed Service for Prometheus (VMP) monitors the operational status of NGINX by using the exporter. This topic describes how to deploy nginx\-exporter in a cluster and monitor NGINX.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The NGINX application exposes some metrics on the stub_status page. Nginx\-exporter collects the metrics of a single NGINX instance and converts the metrics into monitoring data that can be used by Prometheus.

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

<span id=".5q2l6aqk5LiA77ya5byA5ZCvIHN0dWJfc3RhdHVzIOWKn-iDvQ=="></span>
### Step 1: Enable the stub_status feature

NGINX exposes its status data on the [stub_status](http://nginx.org/en/docs/http/ngx_http_stub_status_module.html) page. After you deploy NGINX, you need to first check whether the stub_status feature is enabled.


1. In the environment where NGINX is located, execute the following command to check whether the stub_status feature is enabled in NGINX:


```bash
nginx -V 2>&1 | grep -o with-http_stub_status_module
```


If the command output is `with-http_stub_status_module`, it indicates that the stub_status feature is enabled for NGINX.

2. Modify the nginx.conf configuration file to specify the port number and URL to access the stub_status page.

```bash
server {
 listen  8080;
 location /stub_status {
     stub_status on;
     access_log off;
 }
}
```



3. Reload NGINX to make the configuration take effect.


```bash
nginx -t
nginx -s load
```



4. After the configuration is complete, you can view NGINX metrics by using the URL in your local environment.


```bash
curl http://127.0.0.1:8080/stub_status
```


The following section shows the expected response result.

```bash
Active connections: 45
server accepts handled requests
1056958 1156958 4491319
Reading: 0 Writing: 25 Waiting : 7
```


<span id=".5q2l6aqk5LqM77ya6YOo572yIG5naW54LWV4cG9ydGVy"></span>
### Step 2: Deploy nginx\-exporter


1. Log in to the [VKE](https://console.byteplus.com/vke) console.

2. In the left navigation pane, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the name of the cluster to go to the cluster details page.

4. Click **Workload \> Deployment** in the left navigation pane. Click **Create with Yaml** to deploy nginx\-exporter.


```Yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-exporter # Specify the name of the exporter.
  namespace: volcano-metrics # Specify the namespace of the exporter.
  labels:
    app-name: nginx-exporter # Configure the labels of the exporter.
spec:
  replicas: 1 # Specify the number of replicas for the exporter.
  selector:
    matchLabels:
      app: nginx-exporter
  template:
    metadata:
      labels:
        app: nginx-exporter
    spec:
      containers:
      - args: 
          - "-nginx.scrape-uri=http://<nginx-ip>:8080/stub_status" # Configure the metric scraping page path of the exporter, which must be consistent with the stub_status page path of NGINX.
        name: nginx-exporter # Specify the container name.
        image: nginx/nginx-prometheus-exporter:latest # Pull the exporter image from Docker Hub.
        ports:
        - containerPort: 9113 # Specify the container port number.
          app-name: metric-port # Specify the container port name.
```


<span id=".5q2l6aqk5LiJ77ya6YWN572u5pyN5Yqh5Y-R546w"></span>
### Step 3: Configure service discovery


1. Click **Workload \> Resource Explorer** in the left navigation pane.

2. Click **Create with Yaml** to configure service discovery by using PodMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Enter the YAML configuration in the **Yaml** field.


```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: nginx-exporter # Specify the name of PodMonitor.
  namespace: volcano-metrics # Specify the namespace of PodMonitor.
  labels: 
    volcengine.vmp: "true" # Configure the labels for PodMonitor to allow the labels to be identified by prometheus-agent.
spec:
  podMetricsEndpoints:
  - interval: 30s
    port: metric-port # Specify the container port name of the exporter.
    path: /metrics # Specify the URI path for metric exposure. The value is /metrics by default if it is not specified.
  namespaceSelector:
    matchNames: 
    - volcano-metrics # Specify the namespace where the exporter is located.
  selector: 
    matchLabels:
      app-name: nginx-exporter # Specify the label value of the exporter to locate and select the target pod.
```


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results


1. Execute the following command to configure Grafana port forwarding:


```bash
kubectl port-forward service/grafana 3000:3000 -n volcano-metrics
```



2. Open a browser in your local environment (Linux/Mac), paste **localhost:3000** into the address bar, and then press Enter to go to the Grafana login page. Log in to Grafana by using the default username ` admin` and password `admin`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76b0d6fc909f3113679be523218ecad5.png) </span>

3. After you log in to Grafana, you can create an NGINX dashboard to view information about NGINX.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c6869e38a694ac741dd4f6436bb2df36.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed parameters of nginx\-exporter, refer to <a href="https://github.com/nginxinc/nginx-prometheus-exporter">nginx\-exporter</a>.   </div>
