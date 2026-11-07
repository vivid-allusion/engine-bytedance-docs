---
title: "Collecting container logs by using environment variables"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Collecting-container-logs-using-environment-variables"
---

Based on TLS, VKE clusters allow you to configure environment variables for containers to quickly collect container logs in the clusters, including standard output logs and file path logs. This topic describes how to collect container logs by configuring environment variables.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Feature overview

VKE allows you to configure the log collection feature for a container by using environment variables when you create the container. This feature collects specified logs into TLS. The following parameters can be specified:


* **Log collection type**: Valid values: **Container standard output** and **Container file path**. When the log collection mode is **Container file path**, you can specify a specific path for log files.

* **Log project**: A log project is the project management unit for log data, which is used for resource isolation and control. You can use a log project to indicate an application, business, or product.

* **Log topic**: A log topic is a unit for collecting, reading, and writing log data. A log project can include multiple log topics, and you can use log topics to further categorize container logs.

* **Maximum log storage time**: The retention period for logs. You can specify an exact retention period or choose to permanently retain logs.

* **Number of log shards**: Log shards are the basic units for reading and writing logs, and all log data is stored in shards. Each shard provides a certain amount of read and write capacity. We recommend that you plan the number of log shards based on your business requirements.

* **Automatic log shard splitting and number of shards after splitting**: Log shards can be automatically split, and you can specify the number of new shards, which expands the overall read and write capacity of a log topic.

* **Log identifier**: Logs can be identified.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* When you configure container logs by using environment variables, the system can automatically create **log projects** and **log topics**. This operation may cause the resource quota to be exceeded during use. Therefore, before you use this feature, we recommend that you first [apply for a resource quota ](https://docs.byteplus.com/en/docs/tls/Apply_for_resource_quota)in the Quota Center of TLS .

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the default resource quota of TLS, see <a href="https://docs.byteplus.com/en/docs/tls/Limits">Usage restrictions</a>.   </div>
   

* When you delete a container, the system does not automatically delete the corresponding **log project** and **log topic** for the container. If you need to delete them, log in to the TLS console and manually delete them. For details, see [Deleting log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Deleting log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics)the .


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* TLS has been activated. If you have not activated it, log in to the [TLS console](https://console.byteplus.com/tls) and activate it based on the on\-screen prompts.

* The log\-collector add\-on has been installed and upgraded to v1.2.4 or later . For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* (Optional) A **log project** and **log topic** have been created in TLS. For detailed operations, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can create a <strong>log project</strong> and <strong>log topic</strong> before you create a container. You can also use environment variables to automatically create a <strong>log project</strong> and <strong>log topic</strong> when you create a container.   </div>
   

<span id=".6YWN572u5pel5b-X6YeH6ZuG"></span>
## Configuring log collection

<span id=".6YeH6ZuG5qCH5YeG6L6T5Ye65pel5b-X"></span>
### Collecting standard output logs

You can collect container standard output logs by configuring environment variables when you create an application. This topic takes the creation of a Deployment as an example. You can perform the following steps to create a Deployment.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the cluster name to go to the cluster configuration page.

4. In the left navigation bar, click **Workload \> Deployment**. Click **Create with Yaml ** to deploy the application.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: log-app-demo # The application name.
     namespace: default # The namespace to which the application belongs.
   spec: 
     replicas: 1 # The number of application replicas.
     selector: 
       matchLabels: 
         app: nginx
     template: 
       metadata: 
         labels: 
           app: nginx
       spec:
         containers:
         - env: 
           - name: volc_logs_demo # Collect container standard output logs.
             value: stdout
           - name: volc_logs_demo_project # Specify a log project.
             value: doc-demo
           - name: volc_logs_demo_topic # Specify a log topic.
             value: pod-log
           name: nginx # The container name.
           image: nginx:latest # The address and version of the application image.
           ports:
           - containerPort: 80 # The container port.
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information about environment variables, see the <strong>Environment variables description</strong> section of this topic.   </div>
   

5. Click **Confirm**.


<span id=".6YeH6ZuG5paH5Lu26Lev5b6E5pel5b-X"></span>
### Collecting file path logs

When you create an application, you can configure environment variables to collect logs from specified paths in the container. This topic takes the creation of a Deployment as an example. You can perform the following steps to create a Deployment.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the cluster list on the right side, find the target cluster.

3. Click the cluster name to go to the cluster configuration page.

4. In the left navigation bar, click **Workload \> Deployment**. Click **Create with Yaml ** to deploy the application.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: log-app-demo # The application name.
     namespace: default # The namespace to which the application belongs.
   spec: 
     replicas: 1 # The number of application replicas.
     selector: 
       matchLabels: 
         app: nginx
     template: 
       metadata: 
         labels: 
           app: nginx
       spec:
         containers:
         - env: 
           - name: volc_logs_demo # Collect logs from the specified file path in the container.
             value: /var/log/nginx/access.log
           - name: volc_logs_demo_project # Specify a log project.
             value: doc-demo
           - name: volc_logs_demo_topic # Specify a log topic.
             value: pod-log
           name: nginx # The container name.
           image: nginx:latest # The address and version of the application image.
           ports:
           - containerPort: 80 # The container port.
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information about environment variables, see the <strong>Environment variables description</strong> section of this topic.   </div>
   

5. Click **Confirm**.


<span id=".5p-l55yL5pel5b-X"></span>
## Viewing logs

After the application is created, you can log in to the TLS console to view and search for logs.


1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the left navigation bar, click **Resource management \> Project**. In the log project list, click the name of the target log project to go to the log project details page.

3. Click the **Topic** tab. Find the target topic in the **log topic** list.

4. Click **Query and analysis** in the Actions column to search and analyze container logs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more methods of searching for and analyzing logs, see <a href="https://docs.byteplus.com/en/docs/tls/Query-and-analysis-process">TLS documentation</a> of .   </div>
   

<span id=".546v5aKD5Y-Y6YeP6K-05piO"></span>
## Environment variables description

The following table describes the environment variables related to container log collection.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you configure container log collection by using environment variables, the default collection method is simple mode. To parse log content, we recommend that you use the <a href="https://console.byteplus.com/tls">TLS console</a>.</div>


* <div data-tips="true" data-tips-type="tip"><code>{key}</code> of the environment variables described in the following table indicates the name of the collection configuration in TLS, which must be unique in the same cluster.</div>




|Environment variable |Description |Example |Considerations |
|---|---|---|---|
|volc_logs_{key} |Required. Configure the log collection mode. Valid values:<br><br><br>* **stdout**: Collect container standard output logs.<br><br>* Configure a specific path for log files, such as `/var/log/nginx/access.log`, to collect logs from the specified path.<br><br><br>The `value` must be a string of 3 to 63 characters. The value can contain only lowercase English letters, digits, and hyphens `(-)`, and cannot start or end with hyphens (`-`). |* Sample standard output log:<br><br><br>```yaml```<br>```- name: volc_logs_demo```<br>```  value: stdout```<br><br><br><br>* Sample file path log:<br><br><br>```yaml```<br>```- name: volc_logs_demo```<br>```  value: /var/log/nginx/access.log```<br> |If the log topic `volc_logs_{key}_topic` does not exist, a log topic named `{key}` will be automatically created. |
|volc_logs_{key}_project |Required. Specify a **log project** of TLS.<br><br>The `value` must be a string of 3 to 63 characters. The value can contain only lowercase English letters, digits, and hyphens `(-)`, and cannot start or end with hyphens (`-`). |```yaml```<br>```- name: volc_logs_demo_project```<br>```  value: doc-demo```<br> |* The log project must be in the same region as the cluster.<br><br>* If a log project already exists, use the existing one.<br><br>* If no log project exists, a project will be automatically created. |
|volc_logs_{key}_topic |Optional. Specify a **log topic** of TLS.<br><br>The `value` must be a string of 3 to 63 characters. It can contain only lowercase English letters, digits, and hyphens `(-)`, and cannot start or end with hyphens (`-`). |```yaml```<br>```- name: volc_logs_demo_topic```<br>```  value: pod-log```<br> |* If a log topic already exists, use the existing log topic.<br><br>* If a log topic does not exist, a log topic will be automatically created. |
|volc_logs_{key}_tags |Optional. Configure log labels to identify logs. |```yaml```<br>```- name: volc_logs_demo_tags```<br>```  value: app=demo```<br> |No |
|volc_logs_{key}_shard |Optional. The number of log shards when you create a log topic.<br><br>The `value` must be an integer. Valid values: 1 to 10. If this environment variable is not configured, the default value is 1. |```yaml```<br>```- name: volc_logs_demo_shard```<br>```  value: 4```<br> |If a log topic already exists, this parameter does not take effect. |
|volc_logs_{key}_shardautosplit |Optional. Whether to automatically split log shards when you create a log topic. Valid values:<br><br><br>* **True**: (default) Automatically splits log shards.<br><br>* **False**: Does not automatically split log shards. |```yaml```<br>```- name: volc_logs_demo_shardautosplit```<br>```  value: True```<br> |If a log topic already exists, this parameter does not take effect. |
|volc_logs_{key}_maxshard |Optional. The maximum number of new shards that a log shard can be split into when you create a log topic.<br><br>The `value` must be an integer. Valid values: 1 to 10. If this environment variable is not configured, the default value is 10.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <code>volc_logs_{key}_shardautosplit</code> is <code>False</code>, this parameter does not take effect.</div><br> |```yaml```<br>```- name: volc_logs_demo_maxshard```<br>```  value: 5```<br> |If a log topic already exists, this parameter does not take effect. |
|volc_logs_{key}_ttl |Optional. Specify a log retention period when you create a log topic.<br><br>The `value` must be an integer. Valid values: 1 to 3650. Unit: **days**. A value of 3650 indicates logs are permanently stored. If this environment variable is not configured, the default value is 30. |```yaml```<br>```- name: volc_logs_demo_ttl```<br>```  value: 90```<br> |If a log topic already exists, this parameter does not take effect. |
