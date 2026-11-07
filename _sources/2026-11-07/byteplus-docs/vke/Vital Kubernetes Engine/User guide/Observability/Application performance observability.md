---
title: "Application performance observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Application_performance_observability"
---

VKE can be integrated with [APMPlus](https://docs.byteplus.com/en/docs/apmplus/Application_Performance_Management_Plus) to provide end\-to\-end application performance monitoring services for applications deployed in clusters. This topic describes how to deploy an application in a cluster and integrate the cluster with APMPlus trace monitoring.

<span id="z7UzKA5p"></span>
## Background

APMPlus is an APM service designed for application service quality, performance, and custom instrumentation. By leveraging advanced data collection and monitoring technologies, APMPlus provides enterprises with end\-to\-end application performance monitoring services. It covers both server\-side monitoring, such as root cause analysis for AI large models, issue identification for LLM chains, and comprehensive monitoring of agents, and client\-side monitoring for the app, WebPro, mini program, PC, and OS. It helps enterprises to enhance the efficiency of troubleshooting.

Application performance observability delivers benefits such as low integration costs and non\-intrusive access. It supports end\-to\-end monitoring capabilities for basic resource performance, service, and code layer, and the health status of online application operations. It can be integrated with Java, Go, Python, and other applications, such as large models, LLMs, and agents, through methods such as a self\-developed agent and OpenTelemetry for end\-to\-end monitoring, which provides richer capabilities for restoring abnormal scenarios. Core features include service monitoring, trace analysis, error analysis, log monitoring, custom monitoring, alerting tasks, and other features.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details about application performance observability, see <a href="https://docs.byteplus.com/en/docs/apmplus/Application_Performance_Management_Plus">What is APMPlus</a>.</div>


<span id="OmZ8QeUs"></span>
## Prerequisites


* The apmplus\-opentelemetry\-collector add\-on has been installed. For details, see [apmplus-opentelemetry-collector](https://docs.byteplus.com/en/docs/vke/apmplus-opentelemetry-collector-add-on).

* APMPlus monitoring has been activated. For details, see [Activating APMPlus monitoring](https://docs.byteplus.com/en/docs/apmplus/Activate_server-side_monitoring).

* (Optional) An AMPlus workspace has been created. For details, see [Workspace management](https://docs.byteplus.com/en/docs/apmplus/Workspace_management).


<span id="NKqEWV2n"></span>
## Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can enable application performance monitoring for different types of workloads when you create workloads, including Deployments, StatefulSets, Jobs, CronJobs, and DaemonSets. This topic provides an example of how to create a Deployment. For configuration methods for other types of workloads, see <a href="https://docs.byteplus.com/en/docs/vke/Workload-overview">Workloads</a>.</div>


<span id="2U9mQtY3"></span>
### Configure through the console


1. Go to the Deployment page.

   1. Log in to [Vital Kubernetes Engine (VKE) console](https://console.byteplus.com/vke/overview) .

   2. In the left navigation bar, click **Cluster**.

   3. On the Cluster page, click the name of the cluster for which you need to create a Deployment.

   4. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

2. On the Deployment page, click **Create Deployment**.

3. In the **Container configuration** step, enable **Full\-chain Application Performance Management**, and specify monitoring\-related parameters.

   
   |Parameter |Description |
   |---|---|
   |Monitor application type |Select the application type to monitor. Currently supported types include **Java**, **Python**, and **Node.js**. |
   |APM workspace |(Optional) Select a workspace to store monitoring data for data management and isolation. Each workspace has its own independent data reporting credentials, allowing unified management of traces, logs, and metrics based on the application affiliation attribute. For more details, see [Workspace management](https://docs.byteplus.com/en/docs/apmplus/Workspace_management).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To configure a workspace, upgrade the ampplus\-opentelemetry\-collector add\-on to v3.1.0 or later. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/apmplus-opentelemetry-collector_component_release_notes">Add\-on release notes</a>.</div><br> |
   |Monitor Service Name |(Optional) Specify the name of the monitoring service. This name will be used as the monitoring task name for the current workload and will be displayed in the service list of the APMPlus console. This makes it easier for you to distinguish between different monitoring tasks.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you do not enter a name, the system will use the workload name as the monitoring service name by default.</div><br> |
   

4. After you specify other workload parameters, click **Confirm** to complete the configuration. For more parameter configurations, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).


<span id="v8fNCL7F"></span>
### Configure through kubectl

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you start, make sure that the following conditions are met:</div>



* <div data-tips="true" data-tips-type="tip">The kubectl tool has been installed on your on\-premises computer. For details, see <a href="https://kubernetes.io/docs/tasks/tools/">Installing and configuring kubectl</a>.</div>


* <div data-tips="true" data-tips-type="tip">The target cluster has been connected through kubectl. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connecting to clusters</a>.</div>



When creating workloads in the cluster using YAML, you can configure application performance observability via annotations. The sample YAML code varies slightly for different application types.


<Tabs>
<Tab zoneid="piPM4c28gT" title="Java">
<TabTitle>Java</TabTitle>

The sample configuration code of the Java application is as follows:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-demo # The Deployment name.
  namespace: default # The namespace where the Deployment resides.
spec: 
  replicas: 1 # The number of replicas for the Deployment.
  selector: 
    matchLabels: 
      app: nginx
  template: 
    metadata: 
      labels: 
        app: nginx
      annotations:
        instrumentation.apmplus.volcengine.com/inject-java: "true" # Enable APMPlus observability injection.
        instrumentation.apmplus.volcengine.com/java-container-names: "nginx,myapp" # (Optional) Specify containers for which you want to implement injection.
        apmplus.volcengine.com/service.name: "doc-pod-demo" # (Optional) Specify the service name of the workload in APMPlus. If you do not specify the name, the pod name is used as the server name by default.
    spec:
      containers:
      - name: nginx # The container name.
        image: cr-cn-beijing.volces.com/demo-namespace/demo-repo:v1 # The container image address and tag.
        ports:
        - containerPort: 80 # Exposed container port number
        env: # Use environment variables to specify the service name of the container in APMPlus. This configuration prevails over the apmplus.volcengine.com/service.name configuration in the annotation.
        - name: OTEL_SERVICE_NAME
          value: "container-demo"
```



</Tab>
<Tab zoneid="SMylSIqqVZ" title="Python">
<TabTitle>Python</TabTitle>

The sample configuration code of the Python application is as follows:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-demo # The Deployment name.
  namespace: default # The namespace where the Deployment resides.
spec: 
  replicas: 1 # The number of replicas for the Deployment.
  selector: 
    matchLabels: 
      app: nginx
  template: 
    metadata: 
      labels: 
        app: nginx
      annotations:
        instrumentation.apmplus.volcengine.com/inject-python: "true" # Enable APMPlus observability injection.
        instrumentation.apmplus.volcengine.com/python-container-names: "nginx,myapp" # (Optional) Specify containers for which you want to implement injection.
        apmplus.volcengine.com/service.name: "doc-pod-demo" # (Optional) Specify the service name of the workload in APMPlus. If you do not specify the name, the pod name is used as the server name by default.
    spec:
      containers:
      - name: nginx # The container name.
        image: cr-cn-beijing.volces.com/demo-namespace/demo-repo:v1 # The container image address and tag.
        ports:
        - containerPort: 80 # Exposed container port number
        env: # Use environment variables to specify the service name of the container in APMPlus. This configuration prevails over the apmplus.volcengine.com/service.name configuration in the annotation.
        - name: OTEL_SERVICE_NAME
          value: "container-demo"
```



</Tab>
<Tab zoneid="e3ufLBc0YG" title="NodeJS">
<TabTitle>NodeJS</TabTitle>

The sample configuration code of the NodeJS application is as follows:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-demo # The Deployment name.
  namespace: default # The namespace where the Deployment resides.
spec: 
  replicas: 1 # The number of replicas for the Deployment.
  selector: 
    matchLabels: 
      app: nginx
  template: 
    metadata: 
      labels: 
        app: nginx
      annotations:
        instrumentation.apmplus.volcengine.com/inject-nodejs: "true" # Enable APMPlus observability injection.
        instrumentation.apmplus.volcengine.com/nodejs-container-names: "nginx,myapp" # (Optional) Specify containers for which you want to implement injection.
        apmplus.volcengine.com/service.name: "doc-pod-demo" # (Optional) Specify the service name of the workload in APMPlus. If you do not specify the name, the pod name is used as the server name by default.
    spec:
      containers:
      - name: nginx # The container name.
        image: cr-cn-beijing.volces.com/demo-namespace/demo-repo:v1 # The container image address and tag.
        ports:
        - containerPort: 80 # Exposed container port number
        env: # Use environment variables to specify the service name of the container in APMPlus. This configuration prevails over the apmplus.volcengine.com/service.name configuration in the annotation.
        - name: OTEL_SERVICE_NAME
          value: "container-demo"
```



</Tab>
</Tabs>


If your workload has containers of different languages, you can inject annotations for different languages at the same time. The example is as follows:

```YAML
  template: 
    metadata: 
      labels: 
        app: nginx
      annotations:
        instrumentation.apmplus.volcengine.com/inject-java: "true" # Enable observability injection for the Java application.
        instrumentation.apmplus.volcengine.com/java-container-names: "myapp" # Implement Java injection for the container named myapp.
        instrumentation.apmplus.volcengine.com/inject-python: "true" # Enable observability injection for the Python application.
        instrumentation.apmplus.volcengine.com/python-container-names: "myapp2" # Implement Python injection for the container named myapp2.
    spec:
...
```


<span id="CmzcZvXC"></span>
## Validate results


1. Log in to the [APMPlus](https://console.byteplus.com/apmplus) console.

2. In the left navigation bar, click **Server\-side monitoring**. On the page that appears, click **Click to go to the service list** to go to the server\-side monitoring page.

3. In the left navigation bar of the Service List page, click **Service monitoring** \> **Services**. In the service list, you can view the name of the workload monitoring service in the cluster.

4. Click the service name to view its detailed monitoring information. For more details, see [Service monitoring](https://docs.byteplus.com/en/docs/apmplus/Service_monitoring).
