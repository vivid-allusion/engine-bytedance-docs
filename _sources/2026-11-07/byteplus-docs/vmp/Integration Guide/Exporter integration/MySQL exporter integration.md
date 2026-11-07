---
title: "MySQL exporter integration"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Integrating-through-MySQL-Exporter"
---

VMP monitors the operational status of MySQL by using the exporter. This topic describes how to deploy mysqld\-exporter in a cluster and how to monitor MySQL.

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

<span id=".5q2l6aqk5LiA77ya5pWw5o2u5bqT5o6I5p2D"></span>
### Step 1: Grant permissions on the database

The mysqld\-exporter monitors databases by querying the status data in the databases. Therefore, permissions on the target database instance must be granted. You can execute the following command to grant permissions to a user:

```sql
CREATE USER 'exporter'@'localhost' IDENTIFIED BY 'XXXXXXXX' WITH MAX_USER_CONNECTIONS 3;
GRANT PROCESS, REPLICATION CLIENT, SELECT ON *.* TO 'exporter'@'localhost';
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to set a maximum connection limit for the user to prevent the database from being affected by monitoring data scraping. However, this configuration does not take effect on all versions of databases. For example, MariaDB 10.1 does not support maximum connection settings.</div>


<span id=".5q2l6aqk5LqM77ya5L2_55SoIFNlY3JldCDphY3nva4gTXlTUUwg6L-e5o6l5Liy"></span>
### Step 2: Use a secret to configure the MySQL connection string


1. Log in to the [VKE](https://console.byteplus.com/vke/overview) console.

2. Click **Cluster** in the left navigation pane.

3. On the cluster list page, click the name of the cluster that you want to configure.

4. In the left navigation pane of the cluster details page, click **Configurations** \> **Secret**. On the page that appears, click **Create with Yaml** to configure a secret.


```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret-demo # Specify the secret name.
  namespace: volcano-metrics # Specify the namespace of the secret.
type: Opaque
stringData:
  datasource: "user:password@tcp(ip:port)/" # Configure the connection string of the MySQL instance, which consists of the username, password, address, and port number.
```


<span id=".5q2l6aqk5LiJ77ya6YOo572yIG15c3FsLWV4cG9ydGVy"></span>
### Step 3: Deploy mysql\-exporter


1. In the left navigation pane of the cluster details page, click **Workload \> Deployment**.

2. Click **Create with Yaml** to deploy mysql\-exporter.


```Yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-exporter # Specify the name of the exporter.
  namespace: volcano-metrics # Specify the namespace of the exporter.
  labels: 
    app-name: mysql-exporter # Configure the labels of the exporter.
spec: 
  replicas: 1
  selector:
    matchLabels:
      app-name: mysql-exporter # Change the name based on your business requirements. You can use the information about the MySQL instance.
  template:
    metadata:
      labels:
        app-name: mysql-exporter # Change the name based on your business requirements. You can use the information about the MySQL instance.
    spec:
      containers:
      - env:
        - name: DATA_SOURCE_NAME
          valueFrom: 
            secretKeyRef:
              name: mysql-secret-demo
              key: datasource
        image: prom/mysqld-exporter:latest # Pull the exporter image from Docker Hub.
        imagePullPolicy: IfNotPresent
        name: mysql-exporter # Specify the container name.
        ports:
        - containerPort: 9104 # Specify the container port number.
          name: metric-port # Specify the container port name.
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      terminationGracePeriodSeconds: 30
```


<span id=".5q2l6aqk5Zub77ya6YWN572u6YeH6ZuG6KeE5YiZ"></span>
### Step 4: Configure a collection rule


1. In the left navigation pane of the cluster details page, click **Workload \> Resource Explorer**.

2. Click **Create with Yaml** to configure a collection rule by using PodMonitor.

   * Select **Custom** from the **Type** list.

   * Enter the YAML configuration in the **Yaml** field.


```Yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: mysql-exporter # Specify the name of PodMonitor.
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
      replacement: 'mysql-xxxxxx' # Specify the ID of the MySQL instance.
  namespaceSelector:
    matchNames: 
    - volcano-metrics # Specify the namespace where the exporter is located.
  selector: 
    matchLabels:
      app-name: mysql-exporter # Specify the label value of the exporter to locate and select the target pod.
```


<span id=".57uT5p6c6aqM6K-B"></span>
## Validate results


1. Execute the following command to configure Grafana port forwarding:


```bash
kubectl port-forward service/grafana 3000:3000 -n volcano-metrics
```



2. Open a browser in your local environment (Linux/Mac), enter **localhost:3000** into the address bar to go to the Grafana login interface. Use the default username `admin`, with the password `admin`, to log in. 

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76b0d6fc909f3113679be523218ecad5.png) </span>

3. Create a MySQL dashboard to view the metrics of MySQL.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fa2a31ceab012c59973973cbf1ddafe5.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed parameters of mysql\-exporter, refer to <a href="https://github.com/prometheus/mysqld_exporter">mysql\-exporter</a>.   </div>
