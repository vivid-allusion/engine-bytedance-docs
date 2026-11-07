---
title: "Install LogCollector CRD"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/install_logCollector_crd"
---

When you collect logs using a DaemonSet or sidecar, you can use LogCollector custom resource definition (CRD) to create collection rules. This topic describes how to install LogCollector CRD in a Kubernetes cluster.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

To create collection rules using LogCollector CRD, install the LogCollector component in the Kubernetes cluster, then install LogCollector CRD. The installation process is as follows:


1. Install LogCollectorRule CRD.

2. Install LogCollector Controller.

   1. Configure ServiceAccount, ClusterRole and ClusterRoleBinding to complete the authentication and authorization of the LogCollector Controller.

   2. Create the ConfigMap for the LogCollector Controller.

   3. Create the Deployment of the LogCollector Controller.


<span id="c9ac1811"></span>
## Prerequisite

LogCollector is installed in the Kubernetes cluster. For more information, see [Install LogCollector using a sidecar](https://docs.byteplus.com/docs/tls/install_logcollector_use_a_sidecar), [Install LogCollector using a DaemonSet](https://docs.byteplus.com/docs/tls/install_logCollector_use_a_daemonSet).

<span id="b5406511"></span>
## Helm installation method

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Helm 3 client (version after 3.7) has been installed. For specific operations, please refer to <a href="https://helm.sh/">Helm</a>.</div>


<span id="f02737f3"></span>
### 1 Download the LogCollector Controller Chart package

Log in to the Kubernetes cluster where the LogCollector Controller is to be installed, and then execute the corresponding download commands according to the region where the cluster is located to download the LogCollector Controller Chart installation package to the specified directory.

```Shell
helm pull oci://logcollector-bp-ap-southeast-1.cr.bytepluses.com/logcollector-controller/logcollector-controller --version 0.1.0
```


<span id="d72bf0b7"></span>
### 2 Deploy the LogCollector Controller Chart package

Execute the following commands to deploy the LogCollector Controller Chart package.

```Bash
helm install logcollector-controller logcollector-controller-0.1.0.tgz \
--namespace={namespace} \
--set region={region} \
--set endpoint={endpoint} \
--set secret_id={secret_id} \
--set secret_key={secret_key} \
--set image={image}
```


Among them, `region`, `endpoint`, `secret_id`, `secret_key`, and `image` are required parameters. The detailed descriptions are as follows.


|Parameter |Required |Example |Description |
|---|---|---|---|
|region |Yes |`ap-southeast-1` |The region where a project is deployed.<br><br>For more information on TLS Regions and the corresponding IDs, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
|endpoint |Yes |`tls-ap-southeast-1.bytepluses.com` |The endpoint of TLS, that is, the service URL.<br><br>Log on to the [TLS console](https://console.byteplus.com/tls), and view the endpoint on the project details page. For more information on the supported Regions and the corresponding endpoints, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
|secret_id |Yes |`AK********` |The AccessKey ID of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted. |
|secret_key |Yes |`TUdZ********` |The AccessKey secret of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted. |
|namespace |Yes |`kube-system` |LogCollector Controller namespace.<br><br>The namespace must already exist. If the namespace does not exist, the deployment will fail. |
|image |Yes |`logcollector-bp-ap-southeast-1.cr.bytepluses.com/logcollector-controller/logcollector-controller:latest` |LogCollector image address. For the image address of the latest version, please refer to [LogCollector controller image URLs](https://docs.byteplus.com/docs/tls/install_logCollector_crd#89454489). |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If the error message <strong>Error: INSTALLATION FAILED: Unable to continue with install: CustomResourceDefinition "collectrules.logging.vke.volcengine.com" in namespace, exists and cannot be imported into the current release……</strong> appears, it indicates that a CustomResourceDefinition with the same name as <code>collectrules.logging.vke.volcengine.com</code> has already been installed. That is to say, you need to execute the command <code>kubectl delete crd collectrules.logging.vke.volcengine.com</code> to delete the CustomResourceDefinition.</div>


* <div data-tips="true" data-tips-type="warning">If the error message <strong>Error: INSTALLATION FAILED: Unable to continue with install: ClusterRole "logcollector\-controller" in namespace, exists and cannot be imported into the current release……</strong> appears, it indicates that a ClusterRole with the same name as <code>logcollector-controller</code> has already been installed. In this case, you need to execute the command <code>kubectl delete clusterrole logcollector-controller</code> to delete the ClusterRole first.</div>


* <div data-tips="true" data-tips-type="warning">If the error message <strong>Error: INSTALLATION FAILED: Unable to continue with install: ClusterRoleBinding "logcollector\-controller" in namespace, exists and cannot be imported into the current release……</strong> appears, it indicates that a ClusterRoleBinding with the same name as <code>logcollector-controller</code> has already been installed. Then you need to execute the command <code>kubectl delete clusterrolebinding logcollector-controller</code> to delete the ClusterRoleBinding first.</div>



<span id="ec842992"></span>
## Shell script installation method

<span id="b7679465"></span>
### 1 Download the LogCollector installation package

Log in to the Kubernetes cluster used for installing the LogCollector Controller, and then execute the corresponding download commands according to the region and network type of the cluster to download the LogCollector Controller installation package to the specified directory.

<span id="EI195ey0"></span>
#### VPC network download address

```Shell
wget https://logcollector-bp-ap-southeast-1.tos-ap-southeast-1.ibytepluses.com/logcollector-controller.tgz; tar -xzf logcollector-controller.tgz; chmod 755 ./logcollector-controller/logcollector-controller.sh
```


<span id="I6xBAFjx"></span>
#### Public network download address

```Shell
wget https://logcollector-bp-ap-southeast-1.tos-ap-southeast-1.bytepluses.com/logcollector-controller.tgz; tar -xzf logcollector-controller.tgz; chmod 755 ./logcollector-controller/logcollector-controller.sh
```


<span id="00a79324"></span>
### 2 Install LogCollector Controller

Execute the following commands to install LogCollector Controller.

```Bash
./logcollector-controller/logcollector-controller.sh install --region {region} --endpoint {endpoint} --secret_id {secret_id} --secret_key {secret_key} --namespace {namespace} --image {image}
```


Among them, `region`, `endpoint`, `secret_id`, `secret_key` are required parameters, while `namespace` and `image` are optional parameters. The detailed descriptions are as follows.


|Parameter |Required |Example |Description |
|---|---|---|---|
|region |Yes |`ap-southeast-1` |The region where a project is deployed.<br><br>For more information on TLS Regions and the corresponding IDs, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
|Endpoint |Yes |`tls-ap-southeast-1.bytepluses.com` |The endpoint of TLS, that is, the service URL.<br><br>Log on to the [TLS console](https://console.byteplus.com/tls), and view the endpoint on the project details page. For more information on the supported Regions and the corresponding endpoints, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
|secret_id |Yes |AK\*\*\*\*\*\*\*\* |The AccessKey ID of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted. |
|secret_key |Yes |TUdZ\*\*\*\*\*\*\*\* |The AccessKey secret of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted. |
|namespace |Option |`kube-system` |LogCollector Controller namespace.<br><br>If the namespace is not specified, the kube\-system namespace will be used. If the namespace does not exist, it will be created. |
|image |Option |`logcollector-bp-ap-southeast-1.cr.bytepluses.com/logcollector-controller/logcollector-controller:latest` |The image address of LogCollector Controller. If the image address is not specified, the image address of the latest version corresponding to the region will be used. For the image address of the latest version, please refer to [LogCollector controller image URLs](https://docs.byteplus.com/docs/tls/install_logCollector_crd#89454489). |


<span id="e5357305"></span>
## Manual installation

Log in to the Kubernetes cluster where the LogCollector Controller needs to be installed, and then refer to the following steps to deploy the LogCollector Controller in the form of Deployment.

<span id=".XzEt5Yib5bu6LWxvZ2NvbGxlY3RvcnJ1bGUtY3Jk"></span>
### 1 Create LogCollectorRule CRD

LogCollectorRule CRD is a type of Kubernetes resource that is defined by BytePlus Torch Log Service (TLS) and is used to create collection rules for LogCollector.


1. Log in to the Kubernetes cluster where you want to install LogCollector CRD.

2. Create a YAML file to define LogCollectorRule CRD. This topic uses `crd.yaml` as an example for demonstration.

   ```bash
   vim crd.yaml
   ```
   

3. Edit the YAML file and type the following content into the file.

   ```yaml
   apiVersion: apiextensions.k8s.io/v1
   kind: CustomResourceDefinition
   metadata:
     name: collectrules.logging.vke.volcengine.com
   spec:
     group: logging.vke.volcengine.com
     names:
       kind: CollectRule
       listKind: CollectRuleList
       plural: collectrules
       singular: collectrule
       shortNames:
         - cr
     scope: Cluster
     versions:
       - name: v1alpha1
         served: true
         storage: true
         subresources:
           status: { }
         schema:
           openAPIV3Schema:
             type: object
             properties:
               spec:
                 x-kubernetes-preserve-unknown-fields: true
               status:
                 x-kubernetes-preserve-unknown-fields: true
     conversion:
       strategy: None
   ```
   

4. Run the following command to apply the configuration in the`crd.yaml` file.

   ```bash
   kubectl apply -f crd.yaml
   ```
   


<span id=".XzIt5a6J6KOFLWxvZ2NvbGxlY3Rvci1jb250cm9sbGVy"></span>
### 2 Install LogCollector Controller

LogCollector Controller is a Kubernetes controller that monitors and maintains the status of LogCollectorRule CR in the Kubernetes cluster. When LogCollector Controller detects that LogCollectorRule CR is created, updated, or destroyed, it creates, updates, or destroys the corresponding collection rule in the TLS console.

<span id="ebf0a533"></span>
#### 2.1 Create a Namespace

Create a Namespace for the LogCollector Controller.


1. Create a YAML file named `logcollector_controller_ns.yaml`.

   ```Bash
   vim logcollector_controller_ns.yaml
   ```
   

2. Edit the YAML file and enter the following content into the YAML file.

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
   

3. Execute the following commands to make the Namespace configuration take effect.

   ```Bash
   kubectl apply -f logcollector_controller_ns.yaml
   ```
   


<span id="c1849ae6"></span>
#### 2.2 Create a ServiceAccount

Create a ServiceAccount for LogCollector Controller.


1. Log in to the Kubernetes cluster where you want to install LogCollector Controller.

2. Create a YAML file named `logcollector_controller_sa.yaml`.

   ```bash
   vim logcollector_controller_sa.yaml
   ```
   

3. Edit the YAML file and type the following content into the file.

   ```YAML
   apiVersion: v1
   kind: ServiceAccount
   metadata:
     name: logcollector-controller
     namespace: <namespace>
   ```
   

   The parameter descriptions are as follows:

   
   |Parameter |Example |Description |
   |---|---|---|
   |namespace |kube\-system |The Namespace name. Enter the namespace you set in [2.1 Create a Namespace](https://docs.byteplus.com/docs/tls/install_logCollector_crd#ebf0a533). |
   

4. Execute the following command to make the ServiceAccount configuration take effect.

   ```bash
   kubectl apply -f logcollector_controller_sa.yaml
   ```
   


<span id="4058bed6"></span>
#### 2.3 Create a ClusterRole

Create a ClusterRole for LogCollector Controller.


1. Log in to the Kubernetes cluster where you want to install LogCollector Controller.

2. Create a YAML file named `logcollector__controllercr.yaml`.

   ```json
   vim logcollector__controllercr.yaml
   ```
   

3. Edit the YAML file and type the following content into the file.

   ```go
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRole
   metadata:
     name: logcollector-controller
   rules:
     - apiGroups:
         - logging.vke.volcengine.com
       resources:
         - collectrules
         - collectrules/status
         - collectrules/finalizers
       verbs:
         - get
         - list
         - watch
         - create
         - update
         - patch
         - delete
         - deletecollection
     - apiGroups:
         - ""
       resources:
         - configmaps
         - secrets
         - events
       verbs:
         - watch
         - list
         - get
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
   

4. Execute the following command to make the ClusterRole configuration take effect.

   ```json
   kubectl apply -f logcollector_controller_cr.yaml
   ```
   


<span id="6b072662"></span>
#### 2.4 Create a ClusterRoleBinding


1. Log in to the Kubernetes cluster where you want to install LogCollector Controller.

2. Create a YAML file named `logcollector_controller_crb.yaml`.

   ```json
   vim logcollector_controller_crb.yaml
   ```
   

3. Edit the YAML file and type the following content into the file.

   ```go
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRoleBinding
   metadata:
     name: logcollector-controller
   subjects:
     - kind: ServiceAccount
       name: logcollector-controller
       namespace: <namespace>
   roleRef:
     kind: ClusterRole
     name: logcollector-controller
     apiGroup: rbac.authorization.k8s.io
   ```
   

   The parameter descriptions are as follows:

   
   |Parameter |Example |Description |
   |---|---|---|
   |namespace |kube\-system |The Namespace name. Enter the namespace you set in [2.1 Create a Namespace](https://docs.byteplus.com/docs/tls/install_logCollector_crd#ebf0a533). |
   

4. Execute the following command to make the ClusterRoleBinding configuration take effect.

   ```json
   kubectl apply -f logcollector_controller_crb.yaml
   ```
   


<span id=".XzItMS3liJvlu7otY29uZmlnbWFw"></span>
#### 2.5 Create a ConfigMap

Create a ConfigMap for LogCollector Controller.


1. Log in to the Kubernetes cluster where you want to install LogCollector Controller.

2. Create a YAML file named `logcollector_controller_config.yaml`.

   ```bash
   vim logcollector_controller_config.yaml
   ```
   

3. Edit the YAML file and type the following content into the file.

   ```yaml
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: logcollector-controller-config
     namespace: <namespace>
   data:
     region: "<region>"
     endpoint: "<endpoint>"
     secret_id: "<secret_id>"
     secret_key: "<secret_key>"
   ```
   

   
   |Parameter |Example |Description |
   |---|---|---|
   |namespace |kube\-system |The Namespace name. Enter the namespace you set in [2.1 Create a Namespace](https://docs.byteplus.com/docs/tls/install_logCollector_crd#ebf0a533). |
   |region |`ap-southeast-1` |The region where a project is deployed. |
   |endpoint |`tls-ap-southeast-1.bytepluses.com` |The endpoint of TLS, that is, the service URL.<br><br>Log on to the [TLS console](https://console.byteplus.com/tls), and view the endpoint on the project details page. For more information on the supported Regions and the corresponding endpoints, refer to [Endpoint](https://docs.byteplus.com/docs/tls/endpoint). |
   |secret_id |AK\*\*\*\*\*\*\*\* |The AccessKey ID of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted. |
   |secret_key |TUdZ\*\*\*\*\*\*\*\* |The AccessKey secret of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted. |
   

4. Execute the following command to make the ConfigMap configuration take effect.

   ```bash
   kubectl apply -f logcollector_controller_config.yaml
   ```
   


<span id="b2372548"></span>
#### 2.6 Create a Deployment

Create a Deployment for the LogCollector Controller.


1. Log in to the Kubernetes cluster where you want to install LogCollector Controller.

2. Create a YAML file named `logcollector_controller_ds.yaml` .

   ```json
   vim logcollector_controller_ds.yaml
   ```
   

3. Edit the YAML file and type the following content into the file.

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: logcollector-controller
     namespace: <namespace>
     labels:
       k8s-app: logcollector-controller
       app.kubernetes.io/instance: logcollector-controller
   spec:
     selector:
       matchLabels:
         k8s-app: logcollector-controller
     replicas: 1
     template:
       metadata:
         labels:
           k8s-app: logcollector-controller
       spec:
         serviceAccountName: logcollector-controller
         containers:
           - name: logcollector-controller
             image: <image>
             imagePullPolicy: Always
             resources:
               limits:
                 cpu: 4000m
                 memory: 4000Mi
               requests:
                 cpu: 100m
                 memory: 100Mi
             env:
               - name: "TLS_REGION"
                 valueFrom:
                   configMapKeyRef:
                     name: logcollector-controller-config
                     key: region
               - name: "TLS_HOST"
                 valueFrom:
                   configMapKeyRef:
                     name: logcollector-controller-config
                     key: endpoint
               - name: "VOLC_ACCESSKEY"
                 valueFrom:
                   configMapKeyRef:
                     name: logcollector-controller-config
                     key: secret_id
               - name: "VOLC_SECRETKEY"
                 valueFrom:
                   configMapKeyRef:
                     name: logcollector-controller-config
                     key: secret_key
   ```
   

   
   |Parameter |Example |Description |
   |---|---|---|
   |namespace |`kube-system` |The Namespace name. Enter the namespace you set in [2.1 Create a Namespace](https://docs.byteplus.com/docs/tls/install_logCollector_crd#ebf0a533). |
   |image |`logcollector-bp-ap-southeast-1.cr.bytepluses.com/logcollector-controller/logcollector-controller:latest` |The image address of LogCollector Controller. For the image address of the latest version, please refer to [LogCollector controller image URLs](https://docs.byteplus.com/docs/tls/install_logCollector_crd#89454489). |
   

4. Execute the following command to make the Deployment configuration take effect.

   ```Bash
   kubectl apply -f logcollector_controller_ds.yaml
   ```
   


<span id="89454489"></span>
## LogCollector controller image URLs

TLS offers the following URLs for access to the LogCollector controller image of the latest version in different Regions.


|Region |Image URL |
|---|---|
|Asia Pacific (Johor) |```Plain```<br>```logcollector-bp-ap-southeast-1.cr.bytepluses.com/logcollector-controller/logcollector-controller:latest```<br> |
