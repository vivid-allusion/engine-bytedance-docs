---
title: "Use Pod to configure a DaemonSet for collecting logs from a container"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Use-Pod-to-configure-a-DaemonSet"
---

When you collect text logs or standard output from containers using a DaemonSet, you can use LogCollector pod environment variables to create a collection rule. This topic describes how to use pod environment variables to create a collection rule for a DaemonSet.

<span id="fc1aaa43"></span>
## Background information

Torch Log Service (TLS) allows you to collect container logs using a DaemonSet and create collection rules through pod environment variables.


* A DaemonSet allows you to collect standard output and text logs from containers. Additionally, it features low resource usage and flexible configurations.

* The method of using LogCollector pod environment variables to create collection rules is simple and convenient.


LogCollector allows you to collect logs from containers in various collection modes, such as single\-line mode and multi\-line mode. Besides the default reserved fields in these collection modes, TLS adds the following reserved fields to container logs collected by LogCollector and creates indexes for them by default.

Reserved fields for container text logs:


|Reserved Field |Description |
|---|---|
|`__image_name__` |Name of an image. |
|`__container_name__` |Name of a container. |
|`__container_ip__` |IP address of a container or Pod. |
|`__pod_name__` |Pod name. |
|`__pod_uid__` |Unique identifier of a Pod. |
|`__namespace__` |Namespace to which a Pod belongs. |


Reserved fields for container standard output:


|Reserved Field |Description |
|---|---|
|`__container_source__` |Type of a data source. Valid values: stdout and stderr. |
|`__image_name__` |Name of an image. |
|`__container_name__` |Name of a container. |
|`__container_ip__` |IP address of a container or Pod. |
|`__pod_name__` |Pod name. |
|`__pod_uid__` |Unique identifier of a Pod. |
|`__namespace__` |Namespace to which a Pod belongs. |


<span id="5f478310"></span>
## Before you begin


* Install LogCollector in a Kubernetes cluster. For more information on the procedure, refer to [Install LogCollector using a DaemonSet](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet).

* Install LogCollector CRD in the Kubernetes cluster. For more information on the procedure, refer to [Install LogCollector CRD](https://docs.byteplus.com/docs/tls/install_logCollector_crd).


<span id="d6ad4ef5"></span>
## Limits


* When you collect standard output from containers, pay attention to the following:

   * The Docker container engine only supports JSON log drivers.

   * If a container matches more than one collection rule, only the latest collection rule takes effect on that container.

* When you collect log files from containers, pay attention to the following:

   * Currently, the collection paths of log files within containers support three mounting methods: no mounting, emptyDir mounting, and hostPath mounting.

   * You cannot set a collection path to a symbolic link because LogCollector cannot access symbolic links to log files within containers. Configure a collection path according to the actual path of a log file within a container.

* After a container stops, LogCollector receives the stop event of the container, then stops collecting logs from the container. If latency exists when LogCollector collects logs from the container, some logs generated before the container stops may not be collected.

* The container engines supported by LogCollector include Docker and Containerd. The limits on access paths corresponding to the preceding container engine types are as follows:

   * Docker: LogCollector accesses the Docker container engine through `/run/docker.sock` of the host. Make sure that this path exists and that LogCollector has the access permissions.

   * Containerd: LogCollector accesses the Containerd container engine through `/run/containerd/containerd.sock` of the host. Make sure that this path exists and that LogCollector has the access permissions.


<span id="6c0d35bc"></span>
## Pod environment variables

You can create TLS resources by configuring Pod environment variables when creating an application, and then collect text logs or standard output from containers.

Among them, the parameters of pod environment variables need to be defined according to your business requirements. The parameters are described as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the names of the following environment variables, <code>{rule_name}</code>should be replaced with the actual name of the collection configuration. Note that underscores (_) are not allowed in this name.</div>



|environment variables Name | Data type | Required |Description |**Example** |
|---|---|---|---|---|
|`volc_logs_{rule_name}` |String |Yes |The type of log collected is described as follows:<br><br><br>* When collecting container standard output, set the `value`to `stdout`.<br><br>* When collecting the text log in the log file in the container, set the `value`to the specific path of the log file in the container. |* Container standard output.<br><br>   ```YAML```<br>```   - name: volc_logs_demo```<br>```      value: stdout```<br>```   ```<br>   <br><br>* Log file in container.<br><br>   ```YAML```<br>```   - name: volc_logs_demo```<br>```      value: /var/log/nginx/access.log```<br>```   ```<br>    |
|`volc_logs_{rule_name}_project` |String |Yes |TLS project name. If the specified project does not exist, TLS automatically creates the project. |```YAML```<br>```- name: volc_logs_demo_project```<br>```   value: doc-demo```<br> |
|`volc_logs_{rule_name}_topic` |String |No |TLS topic name. If the specified topic does not exist, TLS automatically creates the topic with the same name as the `{rule_name}` variable. |```YAML```<br>```- name: volc_logs_demo_topic```<br>```   value: pod-log```<br> |
|`volc_logs_{rule_name}_ttl` |Integer |No |When creating a topic, specify the retention period for logs within that topic. Logs older than the retention period will be automatically cleared. The unit is days, with a default value of 30 days. The valid range of values is from 1 to 3650 days, with a value of 3650 days indicating permanent storage. |```YAML```<br>```- name: volc_logs_demo_ttl```<br>```   value: 90```<br> |
|`volc_logs_{rule_name}_shard` |Integer |No |When creating a topic, specify the number of shards. The valid range of values is from 1 to 10. By default, one shard is created. Each shard provides a write capacity of 5MiB/s, 500 times/s, and a read capacity of 20 MiB/s, 100 times/s. Please plan the shard reasonably when creating the topic. Modifying the number of shards is not supported for the time being after creation. |```YAML```<br>```- name: volc_logs_demo_shard```<br>```   value: 4```<br> |
|`volc_logs_{rule_name}_shardautosplit` |Boolean |No |When creating a topic, specify whether to enable the auto\-splitting of shards.<br><br><br>* True (default): When the amount of data written exceeds the capacity of the existing shard service for 5 consecutive minutes, TLS will automatically split shards according to the amount of data to meet business needs, but the number of shards after splitting cannot exceed the maximum number of splits. New shards that have split within the last 15 minutes will not automatically split.<br><br>* False: Does not enable automatic shard splitting. |```YAML```<br>```- name: volc_logs_demo_shardautosplit```<br>```   value: True```<br> |
|`volc_logs_{rule_name}_maxshard` |Integer |No |When creating a topic, specify the maximum number of shards split, that is, the maximum number of shards after shard splitting. The range of values is 1 to 10, and the default is 10. |```YAML```<br>```- name: volc_logs_demo_maxshard```<br>```   value: 5```<br> |
|`volc_logs_{rule_name}_tags` |String |No |Constant fields added for each log. |```YAML```<br>```- name: volc_logs_demo_tags```<br>```   value: app=demo```<br> |


<span id="bc195fa6"></span>
## configuration example

<span id="0466996c"></span>
### Acquisition container standard output

You can capture container standard output by configuring pod environment variables when you create an app.

To create a stateless load as an example, the pod environment variables configuration example is as follows:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: log-app-demo
  namespace: default
spec: 
  replicas: 1
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
          image: nginx:latest
          ports:
            - containerPort: 80
          env: 
            - name: volc_logs_demo # The name of the collection rule is demo, and it collects the standard output of the container.
              value: stdout
            - name: volc_logs_demo_project # The name of the project is doc-demo.
              value: doc-demo
            - name: volc_logs_demo_topic # The name of the topic is pod-log.
              value: pod-log
```


<span id="be0b783d"></span>
### Capture log files in the container

You can capture log files in containers by configuring pod environment variables when creating an app.

To create a stateless load as an example, the pod environment variables configuration example is as follows:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: log-app-demo
  namespace: default
spec: 
  replicas: 1
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
          image: nginx:latest
          ports:
            - containerPort: 80
          env: 
            - name: volc_logs_demo # The collection rule name is demo, and it collects log files within the container.
              value: stdout
            - name: volc_logs_demo_project # The name of the project is doc-demo.
              value: doc-demo
            - name: volc_logs_demo_topic # The name of the topic is pod-log.
              value: pod-log
```


<span id="16c385d0"></span>
## Pod environment variables support from ConfigMap or Secret mount

<span id="c91ac3c8"></span>
### Pod environment variables from ConfigMap mount


* When pod environment variables are mounted from a ConfigMap, if pod environment variables has a prefix set, then the pod environment variables configuration example is as follows:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: log-app-demo
     namespace: default
   spec: 
     replicas: 1
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
             image: nginx:latest
             ports:
               - containerPort: 80
             envFrom:
               - configMapRef:
                   name: nginx-deployment-configmap
                   optional: false
                 prefix: volc_logs_           
   ---
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: nginx-deployment-configmap
     namespace: default
   data:
     logs-demo: stdout
     logs-demo_project: doc-demo
     logs-demo_topic: pod-log
   ```
   

* When the pod environment variables are mounted from the ConfigMap, if the Pod environment variables have no prefix set, then the Pod environment variables configuration example is as follows:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: log-app-demo
     namespace: default
   spec: 
     replicas: 1
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
             image: nginx:latest
             ports:
               - containerPort: 80
             envFrom:
               - configMapRef:
                   name: nginx-deployment-configmap
                   optional: false          
   ---
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: nginx-deployment-configmap
     namespace: default
   data:
     volc_logs_logs-demo: stdout
     volc_logs_logs-demo_project: doc-demo
     volc_logs_logs-demo_topic: pod-log
   ```
   


<span id="36daf9c8"></span>
### Pod environment variables from Secret mount


* When Pod environment variables are mounted from Secret, if Pod environment variables has a prefix set, then the Pod environment variables configuration example is as follows:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: log-app-demo
     namespace: default
   spec: 
     replicas: 1
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
             image: nginx:latest
             ports:
               - containerPort: 80
             envFrom:
               - secretRef:
                   name: nginx-deployment-secret
                   optional: false
                 prefix: volc_logs_   
        
   ---
   apiVersion: v1
   kind: Secret
   metadata:
     name: nginx-deployment-secret
     namespace: default
   type: Opaque
   data:
     logs-demo: c3Rkb3V0 # base64-encoded stdout
     logs-demo_project: ZG9jLWRlbW8= # base64-encoded doc-demo
     logs-demo_topic: cG9kLWxvZw== # base64-encoded pod-log
   ```
   

* When Pod environment variables are mounted from Secret, if Pod environment variables do not have a prefix set, then the Pod environment variables configuration example is as follows:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: log-app-demo
     namespace: default
   spec: 
     replicas: 1
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
             image: nginx:latest
             ports:
               - containerPort: 80
             envFrom:
               - secretRef:
                   name: nginx-deployment-secret
                   optional: false        
   ---
   apiVersion: v1
   kind: Secret
   metadata:
     name: nginx-deployment-secret
     namespace: default
   type: Opaque
   data:
     volc_logs_logs-demo: c3Rkb3V0 # base64-encoded stdout
     volc_logs_logs-demo_project: ZG9jLWRlbW8= # base64-encoded doc-demo
     volc_logs_logs-demo_topic: cG9kLWxvZw== # base64-encoded pod-log
   ```
   


<span id="123b983d"></span>
## Next steps


* After the collection configuration is created, LogCollector will start listening to log files or the standard output within the container according to the specified rules and collecting logs. The log data will be stored in the specified log topic.

* The log index is disabled by default. You need to enable and configure the index for the log topic in order to query and analyze the collected log data in the console.
