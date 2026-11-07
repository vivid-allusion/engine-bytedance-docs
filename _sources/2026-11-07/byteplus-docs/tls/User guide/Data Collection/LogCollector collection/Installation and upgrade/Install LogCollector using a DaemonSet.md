---
title: "Install LogCollector using a DaemonSet"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/install_logCollector_use_a_daemonSet"
---

Before you collect text logs or standard output from containers, install LogCollector in a Kubernetes cluster and configure the relevant environment. This topic describes how to install LogCollector using a DaemonSet.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

After installing LogCollector on the Kubernetes cluster in the way of DaemonSet, LogCollector can collect the container text logs or the standard output of containers in other Pods. During the installation process, the following steps are mainly completed.


1. Configure a ServiceAccount, a ClusterRole, and a ClusterRoleBinding to complete the authentication and authorization of LogCollector.

2. Create the ConfigMap of LogCollector.

3. Create a DaemonSet for LogCollector.


<span id="fedc4c55"></span>
## Helm installation method

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Helm 3 client (version after 3.7) has been installed. For specific operations, please refer to <a href="https://helm.sh/">Helm</a>.</div>


<span id="6f34deb7"></span>
### 1 Download the LogCollector Chart package

Log in to the Kubernetes cluster where LogCollector is to be installed, and then execute the corresponding download commands according to the region where the cluster is located to download the LogCollector Chart package.

```Shell
helm pull oci://logcollector-bp-ap-southeast-1.cr.bytepluses.com/logcollector/logcollector --version 0.1.0
```


<span id="977ca6aa"></span>
### 2 Deploy the LogCollector Chart package

Execute the following commands to deploy the LogCollector Chart package.

```Bash
helm install logcollector logcollector-0.1.0.tgz \
--namespace={namespace} \
--set region={region} \
--set endpoint={endpoint} \
--set secret_id={secret_id} \
--set secret_key={secret_key} \
--set label={label} \
--set image={image} \
--set logcollector_data={logcollector_data}
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If the error message <strong>Error: INSTALLATION FAILED: Unable to continue with install: ClusterRole "logcollector" in namespace "" exists and cannot be imported into the current release...</strong> appears, it indicates that the ClusterRole with the same name as Logcollector has already been installed. In this case, you need to execute the command <code>kubectl delete clusterrole logcollector</code> to delete this ClusterRole.</div>


* <div data-tips="true" data-tips-type="warning">If the error message <strong>Error: INSTALLATION FAILED: Unable to continue with install: ClusterRoleBinding "logcollector" in namespace "" exists and cannot be imported into the current release...</strong> appears, it indicates that the ClusterRoleBinding with the same name as Logcollector has already been installed. In this case, you need to execute the command <code>kubectl delete clusterrolebinding logcollector</code> first to delete this ClusterRoleBinding.</div>



Among them, `region`, `endpoint`, `secret_id`, `secret_key`, `label`, `image`, and `logcollector_data` are required parameters. The detailed descriptions are as follows.


|Parameter |Required |Example |Description |
|---|---|---|---|
|region |Yes |`ap-southeast-1` |The region where a project is deployed.<br><br>For more information on TLS Regions and the corresponding IDs, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
|endpoint |Yes |`tls-ap-southeast-1.bytepluses.com` |The endpoint of TLS, that is, the service URL.<br><br>Log on to the [TLS console](https://console.byteplus.com/tls), and view the endpoint on the project details page. For more information on the supported Regions and the corresponding endpoints, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
|secret_id |Yes |`AK********` |The AccessKey ID of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted. |
|secret_key |Yes |`TUdZ********` |The AccessKey secret of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted. |
|label |Yes |`http_module` |The label identifier of LogCollector.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to add this LogCollector to a host group of the host identification type, you must set the <code>label</code> parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To add the host to a host group of the host label type, set a host label. Separate multiple labels with commas ( , ).</div><br> |
|namespace |Yes |`kube-system` |LogCollector namespace. Only one can be specified, and make sure that the namespace already exists.<br><br>If the namespace does not exist, the deployment will fail. |
|image |Yes |`logcollector-bp-ap-southeast-1.cr.bytepluses.com/logcollector/logcollector:latest` |LogCollector image address. For the image address of the latest version, please refer to[LogCollector image URLs](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet#89454489). |
|logcollector_data |Yes |`/var/lib/logcollector_data` |The node directory for storing the checkpoint status of LogCollector, which is used to ensure that LogCollector will not collect logs repeatedly after the LogCollector Pod is restarted. |


<span id="694dea57"></span>
## Shell script installation method

<span id="81301a38"></span>
### 1 Download the LogCollector installation package

Log in to the Kubernetes cluster used for installing LogCollector, and then execute the corresponding download commands according to the region and network type of the cluster to download the LogCollector installation package to the specified directory.

<span id="b25abc65"></span>
#### VPC network download address

```Shell
wget https://logcollector-bp-ap-southeast-1.tos-ap-southeast-1.ibytepluses.com/logcollector.tgz; tar -xzf logcollector.tgz; chmod 755 ./logcollector/logcollector.sh
```


<span id="26ff202e"></span>
#### Internet network download address

```Shell
wget https://logcollector-bp-ap-southeast-1.tos-ap-southeast-1.bytepluses.com/logcollector.tgz; tar -xzf logcollector.tgz; chmod 755 ./logcollector/logcollector.sh
```


<span id="e139d27d"></span>
### 2 Install LogCollector

Execute the following commands to install LogCollector.

```Bash
./logcollector/logcollector.sh install --region {region} --endpoint {endpoint} --secret_id {secret_id} --secret_key {secret_key} --label {label} --namespace {namespace} --image {image} --logcollector_data {logcollector_data}
```


Among them, `region`, `endpoint`, `secret_id`, `secret_key`, `label`, and `logcollector_data` are required parameters, while `namespace` and `image` are optional parameters. The detailed descriptions are as follows.


|Parameter |Required |Example |Description |
|---|---|---|---|
|region |Yes |`ap-southeast-1` |The region where a project is deployed.<br><br>For more information on TLS Regions and the corresponding IDs, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
|endpoint |Yes |`tls-ap-southeast-1.bytepluses.com` |The endpoint of TLS, that is, the service URL.<br><br>Log on to the [TLS console](https://console.byteplus.com/tls), and view the endpoint on the project details page. For more information on the supported Regions and the corresponding endpoints, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
|secret_id |Yes |`AK********` |The AccessKey ID of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted. |
|secret_key |Yes |`TUdZ********` |The AccessKey secret of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted. |
|label |Yes |`http_module` |The label identifier of LogCollector.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to add this LogCollector to a host group of the host identification type, you must set the <code>label</code> parameter. Meanwhile, when you create a host group of the host identification type, you need to set the custom identification as this label. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/tls/host_group_overview">Overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To add the host to a host group of the host label type, set a host label. Separate multiple labels with commas ( , ).</div><br> |
|namespace |Option |`kube-system` |LogCollector namespace. Only one can be specified, and make sure that the namespace already exists.<br><br>If the namespace does not exist, the deployment will fail. |
|image |Option |`logcollector-bp-ap-southeast-1.cr.bytepluses.com/logcollector/logcollector:latest` |LogCollector image address. If the image address is not specified, the latest version of the image address corresponding to the specified region will be used. For the image address of the latest version, please refer to [LogCollector image URLs](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet#89454489). |
|logcollector_data |Yes |`/var/lib/logcollector_data` |The node directory for storing the checkpoint status of LogCollector, which is used to ensure that LogCollector will not collect logs repeatedly after the LogCollector Pod is restarted. |


<span id="779a315e"></span>
## Manual installation

<span id="b9a58cf7"></span>
### 1 Create a Namespace

This step will create a Namespace.


1. Log in to the Kubernetes cluster where LogCollector needs to be installed.

2. Create a YAML file named `logcollector_ns.yaml`.

   ```Bash
   vim logcollector_ns.yaml
   ```
   

3. Edit the YAML file and enter the following content into the YAML file.

   Configure the following parameters according to the actual situation.

   ```Bash
   apiVersion: v1
   kind: Namespace
   metadata:
     name: <namespace>
   ```
   

   The parameter descriptions are as follows:

   
   |Parameter |Example |Description |
   |---|---|---|
   |namespace |kube\-system |The Namespace name. |
   

4. Execute the following commands to make the Namespace configuration take effect.

   ```Bash
   kubectl apply -f logcollector_ns.yaml
   ```
   


<span id="f382f5f4"></span>
### 2 Create a ServiceAccount

Create a ServiceAccount for LogCollector and configure basic identity information.


1. Create a YAML file named `logcollector_sa.yaml`.

   ```shell
   vim logcollector_sa.yaml
   ```
   

2. Type the following content in the YAML file.

   ```yaml
   apiVersion: v1
   kind: ServiceAccount
   metadata:
     name: logcollector
     namespace: <namespace>
   ```
   

   
   |Parameter |Example |Description |
   |---|---|---|
   |namespace |kube\-system |The namespace. You can specify up to one namespace. Make sure the namespace is the same as that specified in [1 Create a Namespace](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet#b9a58cf7). |
   

3. Execute the following command to make the ServiceAccount configuration take effect.

   ```shell
   kubectl apply -f logcollector_sa.yaml
   ```
   


<span id="607d5c82"></span>
### 3 Create a ClusterRole

Create a ClusterRole for LogCollector.


1. Create a YAML file named `logcollector_cr.yaml`.

   ```Bash
   vim logcollector_cr.yaml
   ```
   

2. Enter the following content into the YAML file.

   ```YAML
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRole
   metadata:
     name: logcollector
   rules:
     - apiGroups:
         - ""
       resources:
         - pods
         - nodes
         - namespaces
       verbs:
         - get
         - list
         - watch
     - apiGroups:
         - apps
       resources:
         - replicasets
         - deployments
         - daemonsets
         - statefulsets
       verbs:
         - watch
         - list
         - get
     - apiGroups:
         - batch
       resources:
         - jobs
         - cronjobs
       verbs:
         - watch
         - list
         - get
   ```
   

3. Execute the following commands to make the ClusterRole configuration take effect.

   ```Bash
   kubectl apply -f logcollector_cr.yaml
   ```
   


<span id="0133123f"></span>
### 4 Create a ClusterRoleBinding

Create a ClusterRoleBinding for LogCollector.


1. Create a YAML file named `logcollector_crb.yaml`.

   ```shell
   vim logcollector_crb.yaml
   ```
   

2. Type the following content in the YAML file.

   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRoleBinding
   metadata:
     name: logcollector
   subjects:
     - kind: ServiceAccount
       name: logcollector
       namespace: <namespace>
   roleRef:
     kind: ClusterRole
     name: logcollector
     apiGroup: rbac.authorization.k8s.io
   ```
   

   The following table describes the parameters.

   
   |Parameter |Example |Description |
   |---|---|---|
   |namespace |kube\-system |The namespace. You can specify up to one namespace. Make sure the namespace is the same as that specified in [1 Create a Namespace](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet#b9a58cf7). |
   

3. Execute the following command to make the ClusterRoleBinding configuration take effect.

   ```shell
   kubectl apply -f logcollector_crb.yaml
   ```
   


<span id=".XzEt5Yib5bu6LWNvbmZpZ21hcA=="></span>
### 5 Create a ConfigMap

Create a ConfigMap for LogCollector.


1. Create a YAML file named `logcollector_config.yaml`.

   ```shell
   vim logcollector_config.yaml
   ```
   

2. Edit the YAML file and type the following content into the file.

   ```yaml
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: logcollector-config
     namespace: <namespace>
   data:
     logcollector.yml: |
       daemonset_mode: true
   
       autodiscover:
         providers:
           - type: kubernetes
             node: ${NODE_NAME}
   
       output:
         tls:
           region: <region>
           endpoint: <endpoint>
           secret_id: <secret_id>
           secret_key: <secret_key>
           label: <label>
   ```
   

   The following table describes the parameters.

   
   |Parameter |Example |Description |
   |---|---|---|
   |namespace |kube\-system |The namespace. You can specify up to one namespace. Make sure the namespace is the same as that specified in [1 Create a Namespace](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet#b9a58cf7). |
   |region |`ap-southeast-1` |The region where a project is deployed. |
   |endpoint |`tls-ap-southeast-1.bytepluses.com` |The endpoint of TLS, that is, the service URL.<br><br>Log on to the [TLS console](https://console.byteplus.com/tls), and view the endpoint on the project details page. For more information on the supported Regions and the corresponding endpoints, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
   |secret_id |AK\*\*\*\*\*\*\*\* |The AccessKey ID of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted. |
   |secret_key |TUdZ\*\*\*\*\*\*\*\* |The AccessKey secret of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted. |
   |label |http_module |The custom label of LogCollector.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to add this LogCollector to a host group of the host identification type, you must set the <code>label</code> parameter. Meanwhile, when you create a host group of the host identification type, you need to set the custom identification as this label. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/tls/host_group_overview">Overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To add the host to a host group of the host label type, set a host label. Separate multiple labels with commas ( , ).</div><br> |
   

3. Execute the following command to make the ConfigMap configuration take effect.

   ```shell
   kubectl apply -f logcollector_config.yaml
   ```
   


<span id="672c3fee"></span>
### 6 Create a Daemonset

Create a Daemonset for LogCollector to collect logs from the current node.


1. Create a YAML file named `logcollector_ds.yaml`.

   ```shell
   vim logcollector_ds.yaml
   ```
   

2. Type the following content in the YAML file and replace specific parameters as needed.

   ```yaml
   apiVersion: apps/v1
   kind: DaemonSet
   metadata:
     name: logcollector
     namespace: <namespace>
     labels:
       k8s-app: logcollector
       app.kubernetes.io/instance: logcollector
   spec:
     selector:
       matchLabels:
         k8s-app: logcollector
     template:
       metadata:
         labels:
           k8s-app: logcollector
       spec:
         serviceAccountName: logcollector
         terminationGracePeriodSeconds: 65
         containers:
           - name: logcollector
             image: <image>
             imagePullPolicy: Always
             args:
               - /usr/local/container/logcollector/logcollectord
               - -c
               - /usr/local/container/logcollector/etc/logcollector.yml
               - --httpprof
               - 0.0.0.0:6060
             securityContext:
               runAsUser: 0
               # If using Red Hat OpenShift, uncomment this:
               # privileged: true
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
               - name: logcollector-host
                 mountPath: /logcollector_host
                 mountPropagation: HostToContainer
                 readOnly: true
               - name: logcollector-data
                 mountPath: /usr/local/container/logcollector/data
             env:
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
               - name: NODE_NAME
                 valueFrom:
                   fieldRef:
                     fieldPath: spec.nodeName
               - name: NODE_IP
                 valueFrom:
                   fieldRef:
                     fieldPath: status.hostIP                  
         volumes:
           - name: logcollector-config
             configMap:
               defaultMode: 420
               name: logcollector-config
           - name: logcollector-host
             hostPath:
               path: /
           - name: logcollector-data
             hostPath:
               path: <logcollector_data>
               type: DirectoryOrCreate
   ```
   

   The following table describes the parameters.

   
   |Parameter |Example |**Description** |
   |---|---|---|
   |namespace |kube\-system |The namespace. You can specify up to one namespace. Make sure the namespace is the same as that specified in [1 Create a Namespace](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet#b9a58cf7). |
   |image |logcollector\-ap\-southeast\-1.cr.bytepluses.com/logcollector/logcollector:latest |The LogCollector image URL. For more information on URLs for access to the latest version of LogCollector, refer to [LogCollector image URLs](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet#89454489). |
   |path |/var/lib/logcollector_data |The node directory for storing the checkpoint status of LogCollector, which is used to ensure that LogCollector will not collect logs repeatedly after the LogCollector Pod is restarted. |
   

3. Run the following command to apply the Daemonset settings.

   ```shell
   kubectl apply -f logcollector_ds.yaml
   ```
   


<span id="89454489"></span>
## LogCollector image URLs

TLS offers the following URLs for access to the LogCollector image of the latest version in different Regions.


|Region |Image URL |
|---|---|
|Asia Pacific (Johor) |```Bash```<br>```logcollector-bp-ap-southeast-1.cr.bytepluses.com/logcollector/logcollector:latest```<br> |
