---
title: "Autoscaling based on APIG network metrics"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Horizontal_Pod_Autoscaler_based_on_APIG_network_metrics"
---

Vital Kubernetes Engine (VKE) supports workload autoscaling through KEDA, the event\-driven autoscaler add\-on, which helps users reduce costs. This topic describes how to achieve workload autoscaling based on network metrics provided by API Gateway (APIG).

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

KEDA functions as an event\-driven autoscaling add\-on supported by VKE, which can be connected to multiple data sources and scale out workloads from zero and scale in workloads to zero. By leveraging the network request metrics provided by APIG, KEDA can scale in workloads to zero or scale out workloads from zero. This effectively reduces cloud costs during the idle period, enhances elasticity, and improves service competitiveness.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster has been created and needs to be running on Kubernetes v1.24 or later. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The keda add\-on has been installed in the cluster. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.a2VkYS3nu4Tku7Y=).

* The apig\-controller add\-on has been installed in the cluster to connect to APIG. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.YXBpZy1jb250cm9sbGVyLee7hOS7tg==).

* A Vital Managed Service for Prometheus (VMP) workspace has been created, and basic authentication has been enabled. For more information, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* Cloud native observability has been enabled for the cluster. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65bqU55So5ZKM5pyN5Yqh"></span>
### Step 1: Create an application and a service

Deploy an application and a service in the cluster. The following sample code demonstrates how to deploy NGINX.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
  namespace: default
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx
  namespace: default
spec:
  internalTrafficPolicy: Cluster
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - name: http
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: nginx
  sessionAffinity: None
  type: ClusterIP
```


<span id=".5q2l6aqk5LqM77ya5Yib5bu6LWFwaWctaW5ncmVzcw=="></span>
### Step 2: Create an APIG Ingress

Create an APIG Ingress in the cluster in the console. This topic takes the domain name `example.com` as an example. For detailed instructions, see [Creating APIG Ingresses in the console](https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console).

<span id=".5q2l6aqk5LiJ77ya5byA5ZCvLWFwaWct5a6e5L6L6KeC5rWL"></span>
### Step 3: Enable APIG instance monitoring


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. In the left navigation bar, click **Instance management**. On the page that appears, click the name of the target instance to go to the instance details page.

3. Click the **Monitoring data** tab, and click **Bind now**.

4. In the pop\-up dialog box, select the created VMP workspace, and click **Confirm**. Enable APIG instance monitoring and save the monitoring data in the specified VMP workspace.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The APIG instance and the VKE cluster must be bound to the same VMP workspace.   </div>
   

<span id=".5q2l6aqk5Zub77ya5Yib5bu6LWtlZGEt5Ly457yp5a-56LGh"></span>
### Step 4: Create a KEDA scaling object


1. After you install the KEDA add\-on, you need to use a secret to configure the basic authentication information for the VMP workspace. The example is as follows:


```yaml
apiVersion: v1
kind: Secret
metadata:
  name: keda-prom-secret
  namespace: default
data:
  username: "YWRtaW4=" # The VMP workspace username after Base64 encoding. In this example, "YWRtaW4=" indicates admin.
  password: "YWRtaW4xMjM0" # The VMP workspace password after Base64 encoding. In this example, "YWRtaW4xMjM0" indicates admin1234.
```



2. Create an authentication CustomResourceDefinition (CRD) for KEDA to enable KEDA to access the VMP workspace. The example is as follows:


```yaml
apiVersion: keda.sh/v1alpha1
kind: TriggerAuthentication
metadata:
  name: keda-prom-creds
  namespace: default
spec:
  secretTargetRef:
    - parameter: username
      name: keda-prom-secret
      key: username
    - parameter: password
      name: keda-prom-secret
      key: password
```



3. Create a KEDA autoscaling object ScaledObject.

   * `serverAddress` indicates the query address of the VMP workspace. For details, see [Obtaining workspace addresses](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL).

   * `query` indicates the query metric. In this example, the `sum(rate(istio_requests_total[1m]))` metric is selected, which indicates the total number of APIG requests. `request_host` indicates the external access address that corresponds to the APIG Ingress associated with APIG. In this example, `example.com` is used.


```yaml
apiVersion: keda.sh/v1alpha1
kind: ScaledObject
metadata:
  name: apig-scaledobject
  namespace: default
spec:
  scaleTargetRef:
    name: nginx
  pollingInterval: 15
  # The critical definition for scaling from 0 to 1 with KEDA.
  idleReplicaCount: 0
  # The observation window for scaling in replicas from 1 to 0.
  cooldownPeriod: 30
  # The observation window that is triggered after cooldownPeriod is created for the first time.
  initialCooldownPeriod: 0
  # The minimum number of replicas (HPA).
  minReplicaCount: 1
  # The maximum number of replicas (HPA).
  maxReplicaCount: 2
  triggers:
    - type: prometheus
      metadata:
        serverAddress: http://query.prometheus-cn-beijing.ivolces.com/workspaces/5c0***
        threshold: '1'
        query: sum(rate(istio_requests_total{request_host="example.com"}[1m])) by (request_host)
        authModes: "basic"
      authenticationRef:
        name: keda-prom-creds
```


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

<span id=".6aqM6K-B5bel5L2c6LSf6L2957yp5a655YiwLTA="></span>
### Checking whether the workloads decline to zero


1. Log in to [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Monitoring** **center ** \> **Dashboard**.

5. In the dashboard list on the left side, click **Workload monitoring** \> **Deployment monitoring**. After you select a namespace and a workload, you can view the monitoring dashboard for the specified workload.


In the monitoring dashboard, you can see that when the workload is created, two replicas are configured. After the KEDA autoscaling object is created, the scaling metric for the workload is 0. Therefore, the number of replicas is changed to the value of `idleReplicaCount` in the autoscaling object ScaledObject of KEDA, which indicates that the replicas automatically decline to 0.

<span id=".6aqM6K-B5bel5L2c6LSf6L295LuOLTAt5omp5a65"></span>
### Checking whether the workloads are scaled out from zero

Use the following command to access applications in the cluster by using APIG Ingress. `http://14.***.***.***` indicates the external IP address of the APIG instance. To obtain the IP address, see [Obtaining gateway addresses](https://docs.byteplus.com/en/docs/apig/Adding_access_entrance#.6I635Y-W572R5YWz5Zyw5Z2A).

```bash
curl -H "Host: example.com" http://14.***.***.***
```


Expected result: The corresponding application cannot be accessed and the system displays a backend error because the number of replicas for the backend workloads is zero.

```bash
no healthy upstream
```


In addition, when you view the observability dashboard or corresponding metrics in the APIG console or VMP console, you can view request quantity metrics.

When KEDA in the cluster detects an increase in external metrics, it will scale out backend workloads from zero. Scaling from zero to ready incurs a **15\-20 second** delay, during which requests are not served.

After the scale\-out is complete, use the following command to access the applications in the cluster as expected.

```bash
curl -H "Host: example.com" http://14.***.***.***
```


Expected result: Workloads can be accessed as expected through the APIG Ingress.

```html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```


After external requests are handled, the workloads decline to zero again, effectively reducing cloud costs during the idle period.

View the autoscaling monitoring dashboard for information about workload scale\-out and scale\-in.
