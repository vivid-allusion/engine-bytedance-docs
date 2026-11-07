---
title: "Integrating applications via VKE"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_applications_with_VKE"
---

Server\-side Monitoring has integrated with VKE, providing end\-to\-end, full\-trace performance monitoring for applications deployed in VKE clusters. This topic describes how to deploy an application in a VKE cluster and integrate the application with Server\-side Monitoring.

<span id="HhGxuCq7"></span>
## Prerequisites


* Server\-side Monitoring has been activated. For details, see [Activating Server-side Monitoring](https://docs.byteplus.com/en/docs/apmplus/Activate_server-side_monitoring).

* A VKE cluster has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The `apmplus-opentelemetry-collector` add\-on has been installed in the VKE cluster. For details, see [Installing the add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).


<span id="AHr3rHnt"></span>
## Limits

Workspaces have independent data reporting credentials. To use workspaces for data management and data isolation, ensure that the `apmplus-opentelemetry-collector` add\-on has been upgraded to v3.1.0 or later.

<span id="fy4Z78d4"></span>
## Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">‌When creating a workload‌ of any type (Deployment, StatefulSet, Job, CronJob, and DaemonSet), you can enable Server\-side Monitoring‌ for the workload. This topic uses the Deployment creation as an example. For information about how to configure a workload of a different type, see <a href="https://docs.byteplus.com/en/docs/vke/Workload-overview">Workloads</a>.</div>


<span id="MJy5s5Or"></span>
### Method 1: Use the console


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview). 

2. In the left navigation pane, select **Cluster**. In the cluster list, click the target cluster name to go to the cluster management page.

3. In the left navigation pane, select **Workload** \> **Deployment**.

4. Click **Create Deployment**. In the **Container configuration** step, check **End\-to\-end Application Performance Management** and configure monitoring parameters.

   The key parameters in this feature scenario are as follows. For instructions on configuring other parameters, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   
   |Parameter |Description |
   |---|---|
   |Monitor application type |Specify the type of application to monitor. Currently supported types include **Java**, **Python**, and **Node.js**. |
   |Server\-side Monitoring workspace |Select the workspace to which the service belongs. The workspace is used for data management and data isolation. For more details, see [Managing workspaces](https://docs.byteplus.com/en/docs/apmplus/Workspace_management). |
   |Monitor Service Name |(Optional) Configure a name for the monitoring service. This name will be used as the name of the monitoring task for the workload and displayed in the service list in the Server\-side Monitoring console. The name helps you easily distinguish between different monitoring tasks.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this name is not specified, the system will use the workload name as the monitoring service name.</div><br> |
   

5. After configuring other parameters, click **Confirm**.


<span id="e33VNdV5"></span>
### Method 2: Use kubectl

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before creating a Deployment via the kubectl tool, ensure that the following conditions are met:</div>



* <div data-tips="true" data-tips-type="tip">The kubectl tool has been installed locally. For detailed instructions, see <a href="https://kubernetes.io/docs/tasks/tools/">Installing and configuring kubectl</a>.</div>


* <div data-tips="true" data-tips-type="tip">kubectl has been used to connect to the target cluster. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connecting to clusters</a>.</div>



When you create a workload in the cluster using YAML, you can configure the application performance observability feature via annotations. The sample YAML code for different workload types varies slightly.


<Tabs>
<Tab zoneid="cACVdHWP" title="Java">
<TabTitle>Java</TabTitle>

The sample configuration for Java applications is as follows:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-demo # The Deployment name.
  namespace: default # The owning namespace of the Deployment.
spec: 
  replicas: 1 # The Deployment replica count.
  selector: 
    matchLabels: 
      app: nginx
  template: 
    metadata: 
      labels: 
        app: nginx
      annotations:
        instrumentation.apmplus.volcengine.com/inject-java: "true" # Enable APMPlus observability injection.
        instrumentation.apmplus.volcengine.com/workspace: default  # Specify the workspace to which the service belongs.
        instrumentation.apmplus.volcengine.com/java-container-names: "nginx,myapp" # (Optional) Specify containers to which injection applies.
        apmplus.volcengine.com/service.name: "doc-pod-demo" # (Optional) Specify a name for the service corresponding to the workload in APMPlus. If it is not configured, the Pod name is used as the server name by default.
    spec:
      containers:
      - name: nginx # The container name.
        image: cr-cn-beijing.volces.com/demo-namespace/demo-repo:v1 # The container image address and tag.
        ports:
        - containerPort: 80 # The container port number.
        env: # Use an environment variable to define the service name of the container in APMPlus. This configuration takes precedence over the apmplus.volcengine.com/service.name annotation.
        - name: OTEL_SERVICE_NAME
          value: "container-demo"
```





</Tab>
<Tab zoneid="cKoDlqfP" title="Python">
<TabTitle>Python</TabTitle>

The sample configuration for Python applications is as follows:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-demo # The Deployment name.
  namespace: default # The owning namespace of the Deployment.
spec: 
  replicas: 1 # The Deployment replica count.
  selector: 
    matchLabels: 
      app: nginx
  template: 
    metadata: 
      labels: 
        app: nginx
      annotations:
        instrumentation.apmplus.volcengine.com/inject-python: "true" # Enable APMPlus observability injection.
        instrumentation.apmplus.volcengine.com/workspace: default  # Specify the workspace to which the service belongs.
        instrumentation.apmplus.volcengine.com/python-container-names: "nginx,myapp" # (Optional) Specify containers to which injection applies.
        apmplus.volcengine.com/service.name: "doc-pod-demo" # (Optional) Specify a name for the service corresponding to the workload in APMPlus. If it is not configured, the Pod name is used as the server name by default.
    spec:
      containers:
      - name: nginx # The container name.
        image: cr-cn-beijing.volces.com/demo-namespace/demo-repo:v1 # The container image address and tag.
        ports:
        - containerPort: 80 # The container port number.
        env: # Use an environment variable to define the service name of the container in APMPlus. This configuration takes precedence over the apmplus.volcengine.com/service.name annotation.
        - name: OTEL_SERVICE_NAME
          value: "container-demo"
```





</Tab>
<Tab zoneid="rqPkMxEx" title="NodeJS">
<TabTitle>NodeJS</TabTitle>

The sample configuration for NodeJS applications is as follows:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-demo # The Deployment name.
  namespace: default # The owning namespace of the Deployment.
spec: 
  replicas: 1 # The Deployment replica count.
  selector: 
    matchLabels: 
      app: nginx
  template: 
    metadata: 
      labels: 
        app: nginx
      annotations:
        instrumentation.apmplus.volcengine.com/inject-nodejs: "true" # Enable APMPlus observability injection.
        instrumentation.apmplus.volcengine.com/workspace: default  # Specify the workspace to which the service belongs.
        instrumentation.apmplus.volcengine.com/nodejs-container-names: "nginx,myapp" # (Optional) Specify containers to which injection applies.
        apmplus.volcengine.com/service.name: "doc-pod-demo" # (Optional) Specify a name for the service corresponding to the workload in APMPlus. If it is not configured, the Pod name is used as the server name by default.
    spec:
      containers:
      - name: nginx   # The container name.
        image: cr-cn-beijing.volces.com/demo-namespace/demo-repo:v1   # The container image address and tag.
        ports:
        - containerPort: 80    # The container port number.
        env:    # Use an environment variable to define the service name of the container in APMPlus. This configuration takes precedence over the apmplus.volcengine.com/service.name annotation.
        - name: OTEL_SERVICE_NAME
          value: "container-demo"
```





</Tab>
</Tabs>


If your workload has containerized applications in different languages, you can inject annotations for these applications simultaneously. Example:

```YAML
  template: 
    metadata: 
      labels: 
        app: nginx
      annotations:
        instrumentation.apmplus.volcengine.com/workspace: default  # Specify the workspace to which the service belongs.
        instrumentation.apmplus.volcengine.com/inject-java: "true"                 # Enable observability injection for the Java application.
        instrumentation.apmplus.volcengine.com/java-container-names: "myapp"       # Specify the container named myapp to implement Java injection.
        instrumentation.apmplus.volcengine.com/inject-python: "true"               # Enable observability injection for the Python application.
        instrumentation.apmplus.volcengine.com/python-container-names: "myapp2"    # Specify the container named myapp2 to implement Python injection.
    spec:
...
```


<span id="SbOoFjBw"></span>
## Validate results


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Click the **Click to go to service list** link to access the server\-side monitoring page.

3. In the left\-side navigation pane of server\-side monitoring, click **Service Monitoring** \> **Service List**. In the service list, you can view the name of the monitoring service for the workload in the cluster.

4. Click the service name to view the detailed monitoring information. For details, see [Service monitoring](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring).
