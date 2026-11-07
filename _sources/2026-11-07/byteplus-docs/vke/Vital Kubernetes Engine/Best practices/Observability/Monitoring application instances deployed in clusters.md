---
title: "Monitoring application instances deployed in clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Monitoring-MySQL-databases-using-Vital-Managed-Service-for-Prometheus"
---

When you deploy application instances in a VKE cluster, you can use cloud\-native observability to monitor the application instances. This topic describes how to monitor MySQL instances in clusters.

## Background information

MySQL is a commonly used relational database. In Kubernetes, you can use the open source mysqld\-exporter to monitor the running status of MySQL instances deployed in clusters.

## Prerequisites

* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The target cluster has been connected by using kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* Grafana has been deployed in the cluster. For details, see [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

## Procedure

### Step 1: Grant permissions on the database

mysqld\-exporter performs monitoring by querying status data in the target database. Therefore, you need to grant the required permissions on the corresponding database instance. You can run the following command to grant permissions to a user.

```sql
CREATE USER 'exporter'@'localhost' IDENTIFIED BY 'XXXXXXXX' WITH MAX_USER_CONNECTIONS 3;
GRANT PROCESS, REPLICATION CLIENT, SELECT ON *.* TO 'exporter'@'localhost';
```

> **tip**

> We recommend that you specify the maximum number of connections for the user to prevent the database from being affected by monitoring data collection. However, this configuration may not take effect in all database versions. For example, MariaDB v10.1 does not allow you to specify the maximum number of connections.

### Step 2: Create a MySQL connection string Secret

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster to go to the cluster management page.

4. In the left navigation bar, click **Configurations** \> **Secret**. On the Secret page, click **Create with Yaml** to configure a Secret.

   ```yaml
   apiVersion: v1
   kind: Secret
   metadata:
     name: mysql-secret-demo # Specify a name for the Secret.
     namespace: volcano-metrics # Specify a namespace for the Secret.
   type: Opaque
   stringData:
     datasource: "user:password@tcp(ip:port)/" # Specify connection string information for the MySQL instance, including the username, password, address, and port number.
   ```

### Step 3: Deploy mysql\-exporter

In the left navigation bar, click **Workload \> Deployment**. Click **Create with Yaml** to deploy mysql\-exporter.

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-exporter # Specify a name for the exporter.
  namespace: volcano-metrics # Specify a namespace for the exporter.
  labels: 
    app-name: mysql-exporter # Configure exporter labels.
spec: 
  replicas: 1
  selector:
    matchLabels:
      app-name: mysql-exporter # Replace the value with the corresponding name based on your business requirements. You can use MySQL instance information.
  template:
    metadata:
      labels:
        app-name: mysql-exporter # Replace the value with the corresponding name based on your business requirements. You can use MySQL instance information.
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
        name: mysql-exporter # Specify a name for the container.
        ports:
        - containerPort: 9104 # Specify the container port.
          name: metric-port # Specify a name for the container port.
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      terminationGracePeriodSeconds: 30
```

### Step 4: Configure service discovery

1. In the left navigation bar, click **Workload \> Resource Explorer**. Click **Create with Yaml** to configure a collection rule by using a PodMonitor.

   * Select **Custom** from the **Type** drop\-down menu.

   * Edit the configurations in the **Yaml** box.

      ```Yaml
      apiVersion: monitoring.coreos.com/v1
      kind: PodMonitor
      metadata:
        name: mysql-exporter # Specify a name for the PodMonitor.
        namespace: volcano-metrics # Specify a namespace for the PodMonitor.
        labels: 
          volcengine.vmp: "true" # Configure PodMonitor labels to make it discoverable by prometheus-agent.
      spec:
        podMetricsEndpoints:
        - interval: 30s
          port: metric-port # Specify a name for the container port.
          path: /metrics # Specify the container metric path. The default value is /metrics if it is left empty.
          relabelings: # Configure metric relabeling. This can be omitted if not required.
          - action: replace
            sourceLabels:
            - instance
            regex: (.*)
            targetLabel: instance
            replacement: 'mysql-xxxxxx' # Specify the ID of the corresponding MySQL instance.
        namespaceSelector:
          matchNames: 
          - volcano-metrics # Specify the namespace where the container resides.
        selector: 
          matchLabels:
            app-name: mysql-exporter # Specify the container label value to locate and select the target pod.
      ```

## Validating results

1. Run the following command to configure Grafana port mapping.

   ```bash
   kubectl port-forward service/grafana 3000:3000 -n volcano-metrics
   ```

2. Open a browser in the local environment (Linux/Mac), enter **localhost:3000** in the address bar to go to the Grafana login page, and then log in to Grafana by using the default username `admin` and password `admin`.

3. Create a MySQL dashboard to view MySQL metrics.

   > **tip**

   > For detailed parameters of mysql\-exporter, see [mysqld\-exporter](https://github.com/prometheus/mysqld_exporter).
