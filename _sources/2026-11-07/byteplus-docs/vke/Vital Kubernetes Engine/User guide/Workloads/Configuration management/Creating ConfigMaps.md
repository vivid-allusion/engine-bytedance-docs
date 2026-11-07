---
title: "Creating ConfigMaps"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-ConfigMap"
---

A ConfigMap is used to store application configuration data in key\-value pairs. ConfigMaps help implement configuration decoupling, which allows different environments to easily have separate configurations.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="YRpmwsYcrf" title="Use the console">
<TabTitle>Use the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the target cluster.

4. In the left navigation pane of the cluster management page, click **Configurations** \> **ConfigMap**. On the page that appears, click **Create ConfigMap**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |Enter a name that follows the on\-screen naming rules. The name must be unique within the same namespace. |
   |Namespace |Select the namespace to which the ConfigMap belongs. We recommend that you select a custom namespace or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Configuration content |Provide the configuration items. You can manually create configuration items, for example, a `root-cert.pem` item for authentication.<br><br><br>* Click **Add key\-value pair** to add one manually.<br><br>* Click **Upload local file** to upload a configuration file.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For security reasons, uploading binary text via the console is not supported. However, you can use the kubectl command to upload binary text if necessary. For kubectl command details, see <a href="https://kubernetes.io/zh-cn/docs/reference/kubectl/generated/kubectl_create/kubectl_create_configmap/">Kubernetes documentation</a>.   </div><br>    |
   |Tag |Click **Add new** and then enter a key\-value pair that complies with the on\-screen requirements.**** Labels are used to specify identifying attributes of a resource. |
   |Annotation |Click **Add annotation** and then enter a key\-value pair that complies with the on\-screen requirements.**** Create annotations for the ConfigMap. Annotations in Kubernetes are used to attach arbitrary non\-identifying metadata to a resource and can contain characters that are not permitted in labels. They enable efficient metadata retrieval.**** |
   

5. Click **Confirm**.


</Tab>
<Tab zoneid="fkDyGWHS00" title="Create through YAML">
<TabTitle>Create through YAML</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you start, make sure that the following conditions are met:</div>



* <div data-tips="true" data-tips-type="default">The kubectl tool has been installed on your on\-premises computer. For details, see <a href="https://kubernetes.io/docs/tasks/tools/">Installing and configuring kubectl</a>.</div>


* <div data-tips="true" data-tips-type="default">The target cluster has been connected through kubectl. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster">Connecting to clusters</a>.</div>


1. Create the YAML file for the ConfigMap. The following `demo-configmap.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: demo-configmap # The ConfigMap name.
     namespace: default # Namespace of the ConfigMap.
   data:
     key1: value1 # Key-value data in the ConfigMap.
   ```
   

2. Run the following command to create a ConfigMap.

   ```bash
   kubectl apply -f demo-configmap.yaml
   ```
   

3. View the created ConfigMap.

   ```bash
   kubectl get cm
   ```
   

   The expected response is as follows:

   ```bash
   NAME                DATA            AGE
   demo-configmap      2               7m
   ```
   


</Tab>
</Tabs>


<span id="qh9LZF3Z"></span>
## Results

After completing the operation, you can select the target namespace to view the created ConfigMap in the ConfigMap list.
