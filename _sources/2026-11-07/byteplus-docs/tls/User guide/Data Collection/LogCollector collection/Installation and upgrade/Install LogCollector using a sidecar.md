---
title: "Install LogCollector using a sidecar"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/install_logcollector_use_a_sidecar"
---

This topic describes how to install LogCollector in a Kubernetes cluster using a sidecar.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The LogCollector installed in Sidecar mode only supports collecting the text logs of other containers within the Pod where the LogCollector is located, and does not support collecting the standard output of containers. Nor does it support collecting the text logs or standard output of containers in other Pods. The main installation procedure is as follows:


1. Create a ConfigMap for LogCollector.

2. Create a sidecar for LogCollector.


<span id="6a88672d"></span>
## Procedure

Log in to the Kubernetes cluster where you want to install LogCollector. Then, perform the following steps to deploy LogCollector using a sidecar:

<span id="5655cd60"></span>
### 1 Create a Namespace

This step will create a Namespace.


1. Create a YAML file named `logcollector_ns.yaml`.

   ```Bash
   vim logcollector_ns.yaml
   ```
   

2. Edit the YAML file and enter the following content into the YAML file.

   ```Bash
   apiVersion: v1
   kind: Namespace
   metadata:
     name: <namespace>
   ```
   

   The parameter descriptions are as follows:

   
   |Parameter |Example |**Description** |
   |---|---|---|
   |namespace |kube\-system |The Namespace name. |
   

3. Execute the following commands to make the Namespace configuration take effect.

   ```Bash
   kubectl apply -f logcollector_ns.yaml
   ```
   


<span id=".XzEt5Yib5bu6LWNvbmZpZ21hcA=="></span>
### 2 Create a ConfigMap

Create a ConfigMap for LogCollector.


1. Create a YAML file named `logcollector_config.yaml`.

   ```shell
   vim logcollector_config.yaml
   ```
   

2. Edit the YAML file and type the following script into the YAML file.

   Configure the relevant parameters in the script as needed.

   ```yaml
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: logcollector-config
     namespace: <namespace>
   data:
     logcollector.yml: |
       sidecar_mode: true
   
       output:
         tls:
           region: <region>
           endpoint: <endpoint>
           secret_id: <secret_id>
           secret_key: <secret_key>
           label: <label>
   ```
   

   The following table describes the parameters.

   
   |Variable |Example |**Description** |
   |---|---|---|
   |namespace |`test1` |The namespace name. Enter the namespace that you set in [1 Create a Namespace](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar#5655cd60). |
   |region |`ap-southeast-1` |The region where a project is deployed. For more information on TLS Regions and the corresponding IDs, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
   |endpoint |`tls-ap-southeast-1.bytepluses.com` |The endpoint of TLS, that is, the service URL.<br><br>Log on to the [TLS console](https://console.byteplus.com/tls), and view the endpoint on the project details page. For more information on the supported Regions and the corresponding endpoints, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
   |secret_id |AK\*\*\*\*\*\*\*\* |The AccessKey ID of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted. |
   |secret_key |TUdZ\*\*\*\*\*\*\*\* |The AccessKey secret of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted. |
   |label |http_module |The custom label of LogCollector.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to add this LogCollector to a host group of the host identification type, you must set the <code>label</code> parameter. Meanwhile, when you create a host group of the host identification type, you need to set the custom identification as this label. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/tls/host_group_overview">Overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To add the host to a host group of the host label type, set a host label. Separate multiple labels with commas ( , ).</div><br> |
   

3. Run the following command to apply the configuration in the `configmap.yaml` file.

   ```shell
   kubectl apply -f logcollector_config.yaml
   ```
   


<span id=".XzIt5Yib5bu6LXNpZGVjYXIt6YWN572u"></span>
### 3 Create a Sidecar

Create a Sidecar for LogCollector, which is used to collect the text logs of other containers within the same Pod.


1. Create a YAML file named `logcollector_sc.yaml`.

   ```shell
   vim logcollector_sc.yaml
   ```
   

2. Type the following content into the YAML file and set specific parameters as needed.

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: sidecar-demo
     namespace: <namespace>
   spec:
     containers:
       - name: generator
         image: busybox:1.28
         args:
           - /bin/sh
           - -c
           - >
             i=0;
             while true;
             do
               echo "$i: $(date)" >> /var/log/foo.log;
               i=$((i+1));
               sleep 1;
             done
         volumeMounts:
           - name: logs-dir
             mountPath: /var/log
       - name: logcollector
         image: <image>
         imagePullPolicy: Always
         args:
           - /usr/local/container/logcollector/logcollectord
           - -c
           - /usr/local/container/logcollector/etc/logcollector.yml
           - --httpprof
           - 0.0.0.0:6060
         resources:
           limits:
             cpu: '2'
             memory: 2Gi
           requests:
             cpu: '1'
             memory: 1Gi
         volumeMounts:
           - name: logcollector-config
             mountPath: /usr/local/container/logcollector/etc
             readOnly: true
           - name: logcollector-data
             mountPath: /usr/local/container/logcollector/data
           - name: logs-dir
             mountPath: /var/log
         env:
           - name: "LOG_COLLECTOR_ENV_TAGS"
             value: "__pod_name__|__pod_ip__|__namespace__|__node_name__|__node_ip__"
           - name: "__pod_name__"
             valueFrom:
               fieldRef:
                 fieldPath: metadata.name
           - name: "__pod_ip__"
             valueFrom:
               fieldRef:
                 fieldPath: status.podIP
           - name: "__namespace__"
             valueFrom:
               fieldRef:
                 fieldPath: metadata.namespace
           - name: "__node_name__"
             valueFrom:
               fieldRef:
                 fieldPath: spec.nodeName
           - name: "__node_ip__"
             valueFrom:
               fieldRef:
                 fieldPath: status.hostIP
           - name: MAX_MEM
             valueFrom:
               resourceFieldRef:
                 containerName: logcollector
                 resource: limits.memory
           - name: MAX_PROCS
             valueFrom:
               resourceFieldRef:
                 containerName: logcollector
                 resource: limits.cpu
     volumes:
       - name: logcollector-config
         configMap:
           defaultMode: 420
           name: logcollector-config
       - name: logcollector-data
         emptyDir: { }
       - name: logs-dir
         emptyDir: { }
   ```
   

   
   |**Variable** |Example |**Description** |
   |---|---|---|
   |namespace |kube\-system |The namespace name. Enter the namespace that you set in [1 Create a Namespace](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar#5655cd60). |
   |image |logcollector\-ap\-southeast\-1.cr.bytepluses.com/logcollector/logcollector:latest |The LogCollector image URL. For more information on URLs for access to the latest version of LogCollector, refer to [LogCollector image URLs](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar#89454489). |
   

3. Run the following command to apply the configuration in `logcollector_sc.yaml` file.

   ```shell
   kubectl apply -f logcollector_sc.yaml
   ```
   


<span id="89454489"></span>
## LogCollector image URLs

TLS offers the following URLs for access to the LogCollector image of the latest version in different Regions.


|Region |Image URL |
|---|---|
|Asia Pacific (Johor) |```Bash```<br>```logcollector-bp-ap-southeast-1.cr.bytepluses.com/logcollector/logcollector:latest```<br> |
